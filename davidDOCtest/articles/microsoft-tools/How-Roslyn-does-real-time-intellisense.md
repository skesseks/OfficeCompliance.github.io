[Source](http://stackoverflow.com/questions/9556026/a-new-and-full-implementation-of-generic-intellisense)

How (in detail) do Microsoft implement their as-you-type Intellisense?

I can describe it to any level of detail you care to name, but I don't have the time for more than a brief explanation. I'll explain how we do it in Roslyn.

First, we build an immutable model of the token stream using a data structure that can efficiently represent edits, since obviously edits are precisely what there are going to be a lot of. 

The key insight to making it efficient for persistent reuse is to represent the character lengths of the tokens but not their character positions in the edit buffer; remember, a token at the end of the file is going to change position on every edit but the length of the token does not change. You must at all costs minimize the number of total re-lexings if you want to be efficient on extremely large files.

Once you have an immutable model that can handle inserts and deletions to build up an immutable token stream without re-lexing the entire file every time, you then have to do the same thing, but for grammatical analysis. This is in practice a considerably harder problem. I recommend that you obtain an undergraduate or graduate degree in computer science with an emphasis on parser theory if you have not already. We obtained the help of people with PhDs who did their theses on parser theory to design this particular bit of the algorithm.

Then, obviously, build a grammatical analyzer that can analyze C#. Remember, it has to analyze broken C#, not correct C#; IntelliSense has to work while the program is in a non-compiling state. So start by coming up with modifications to the grammar that have good error-recovery characteristics.

OK, so now you've got a parser that can efficiently do grammatical analysis without re-lexing or re-parsing anything but the edited region, most of the time, which means that you can do the work between keystrokes. I forgot to mention, of course you will need to come up with some mechanism to not block the UI thread while doing all of these analyses should the analysis happen to take longer than the time between two keystrokes. The new "async/await" feature of C# 5 should help with that. (I can tell you from personal experience: be careful with the proliferation of tasks and cancellation tokens. If you are careless, it is possible to get into a state where there are tens of thousands of cancelled tasks pending, and that is not fast.)

Now that you've got a grammatical analysis you need to build a semantic analyzer. Since you are only doing IntelliSense, it does not need to be a particularly sophisticated semantic analyzer. (Our semantic analyzer must do an analysis suitable for generating code from correct programs and correct error analysis from incorrect programs.) But of course, again it has to do good semantic analysis on broken programs, which does increase the complexity considerably.

My advice is to start by building a "top level" semantic analyzer, again using an immutable model that can persist the state of the declared-in-source-code types from edit to edit. The top level analyzer deals with anything that is not a statement or expression: type declarations, directives, namespaces, method declarations, constructors, destructors, and so on. The stuff that makes up the "shape" of the program when the compiler generates metadata.

Metadata! I forgot about metadata. You'll need a metadata reader. You need to be able to produce IntelliSense on expressions that refer to types in libraries, obviously. I recommend using the CCI libraries as your metadata reader, and not Reflection. Since you are only doing IntelliSense, obviously you don't need a metadata writer.

Anyway, once you have a top-level semantic analyzer, then you can write a statement-and-expression semantic analyzer that analyzes the types of the expressions in a given statement. Pay particular attention to name lookup and overload resolution algorithms. Method type inference will be particularly tricky, especially inside LINQ queries.

Once you've got all that, an IntelliSense engine should be easy; just work out the type of the expression at the current cursor position and display a dropdown appropriately.


how hard would it be for me to create my own of the same standard?

Well, we've got a team of, call it ten people, and it'll probably take, call it five years all together to get the whole thing done from start to finish. But we have lots more to do than just the IntelliSense engine. That's maybe only 40% of the work. Oh, and half those people work on VB, now that I think about it. But those people have on average probably five or ten years experience in doing this sort of work, so they're faster at it than you will be if you've never done this before.

So let's say it should take you about ten to twenty years of full time work, working alone, to build a Roslyn-quality IntelliSense engine for C# that can do acceptably-close-to-correct analysis of large programs in the time between keystrokes.

Longer if you need to do that PhD first, obviously.

Or, you could simply use Roslyn, since that's what it's for. That'll take you probably a few hours, but you don't get the fun of doing it yourself. And it is fun!
