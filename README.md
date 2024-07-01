# TypeUniverseErrorPOC

This is a small reproducible example made for this Stack Overflow question: [TypeUniverse Cannot Resolve Assembly Exception (in UWP app with transitive references)](https://stackoverflow.com/questions/78690569/typeuniverse-cannot-resolve-assembly-exception-in-uwp-app-with-transitive-refer?noredirect=1#comment138738359_78690569).

I have a UWP app, App1, and two .NET Standard libraries, ClassLibrary1 and ClassLibrary2.

ClassLibrary1 includes ISampleInterface and SampleClass. ClassLibrary2 references ClassLibrary1 and includes Class1, which can implement either the interface or SampleClass from ClassLibrary1.

When I reference ClassLibrary2 in my UWP App1, a TypeUniverse exception is thrown:
```
Cannot resolve Assembly or Windows Metadata file 'Type universe cannot resolve assembly: ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null.' App1 D:\0624\POC2\App1\App1.csproj
```

The build succeeds when Class1 only implements the interface. ClassLibrary2 also builds successfully on its own.

Adding a direct reference to ClassLibrary1 in the UWP app resolves this issue. However, this workaround feels unnecessary since there's already a transitive dependency on ClassLibrary1.

In our multi-project solution, this forces us to add what seems like redundant references across projects.

Reproducible Example: [TypeUniverseErrorPOC](https://github.com/sanjaymaniam/TypeUniverseErrorPOC/tree/master/POC2)

Can anyone explain why this issue occurs specifically in a UWP root project? Thanks in advance for any help.
