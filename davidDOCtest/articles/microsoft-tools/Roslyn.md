### Resources
- [Roslyn Source and GitHub Page](https://github.com/dotnet/roslyn)
- [Build Talk](https://www.youtube.com/watch?v=Ip6wrpYFHhE&index=9&list=WL): Shows how to build rules
- [MSDN Magazine Overview of Roslyn](https://msdn.microsoft.com/en-us/magazine/dn879356): Using Roslyn to write a live code analyzer for an API

### Questions
- Can I use Rosyln to analyze code based on rules I write around documentation?
- What version of VS is required?
- Does Rosyln ONLY work in VS or can I use Roslyn rules in other IDEs?
- What is [this](http://source.roslyn.io/) and can it help us? See [investigation issue](https://github.com/OfficeCompliance/vNext-Investigations/issues/34)

### Notes
- Deploy as NuGet or VSIX
- Code Aware Library that provides guidance on correct use through ebedded tooling and operates on the user's code in real time
- Code analyzer
    - Symbols
        - Language Agnostic
        - FxCop uses this
    - Code Specific
    - Can create rules that are activated at various events in coding
    - Could provide specific instructions, questions, rules, etc. when a particular type of protocol is created
- Code Fix Provider
- Custom fix suggestions can be provided based on error context
    - Developer runs code analyzer based on custom rules
    - Possible fix is presented to developer when they hover over a piece of code identified as an having an issue or suggestion in analyzer
    - Developer can right click and apply.
    - Different types of analysis actions
        - Codeblock
        - Syntax node
        - Compilation
