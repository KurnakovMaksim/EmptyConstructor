[![Chat on Gitter](https://img.shields.io/gitter/room/fody/fody.svg)](https://gitter.im/Fody/Fody)
[![NuGet Status](https://img.shields.io/nuget/v/EmptyConstructor.Fody.svg)](https://www.nuget.org/packages/EmptyConstructor.Fody/)

![Icon](https://raw.githubusercontent.com/Fody/EmptyConstructor/master/package_icon.png)


## This is an add-in for [Fody](https://github.com/Fody/Home/)

Adds an empty constructor to classes even if you have a non-empty one defined.


## Usage

See also [Fody usage](https://github.com/Fody/Home/blob/master/pages/usage.md).


### NuGet installation

Install the [EmptyConstructor.Fody NuGet package](https://nuget.org/packages/EmptyConstructor.Fody/) and update the [Fody NuGet package](https://nuget.org/packages/Fody/):

```powershell
PM> Install-Package Fody
PM> Install-Package EmptyConstructor.Fody
```

The `Install-Package Fody` is required since NuGet always defaults to the oldest, and most buggy, version of any dependency.


### Add to FodyWeavers.xml

Add `<EmptyConstructor/>` to [FodyWeavers.xml](https://github.com/Fody/Home/blob/master/pages/usage.md#add-fodyweaversxml)

```xml
<Weavers>
  <EmptyConstructor/>
</Weavers>
```


## Configuration Options


### Exclude types with an Attribute

If for some reason you want to skip a specific class you can mark it with a `DoNotVirtualizeAttribute`. 

Since no reference assembly is shipped with Virtuosity. Just add the below class to your assembly. Namespace does not matter.

```csharp
public class DoNotVirtualizeAttribute : Attribute
{
}
```

So your class will look like this

```csharp
[DoNotVirtualize]
public class ClassToSkip
{
    ...
}
```


### Include or exclude namespaces
 
These config options are access by modifying the `EmptyConstructor` node in FodyWeavers.xml 


### Visibility

The visibility to use when injecting constructors.

Can not be defined with `Visibility`.

Allowed values: `public` or `family` (aka `protected`)

Defaults to `public`.

For example

```xml
<EmptyConstructor Visibility='family'/>
```


### Making Existing Empty Constructors Visible

Optionally the visibility of already existing constructors can be increased.
If this feature is enabled, the visibility of empty-constructors of non-abstract types will be increased to the same visibility as defined by the `Visibility` configuration (see above).

For example

```xml
<EmptyConstructor MakeExistingEmptyConstructorsVisible='True'/>
```

Will ensure all constructors on non-abstract types will be `public`.


### ExcludeNamespaces

A list of namespaces to exclude.

Can not be defined with `IncludeNamespaces`.

Can take two forms. 

As an element with items delimited by a newline.

```xml
<EmptyConstructor>
    <ExcludeNamespaces>
        Foo
        Bar
    </ExcludeNamespaces>
</EmptyConstructor>
```

Or as a attribute with items delimited by a pipe `|`.

```xml
<EmptyConstructor ExcludeNamespaces='Foo|Bar'/>
```


### IncludeNamespaces

A list of namespaces to include.

Can not be defined with `ExcludeNamespaces`.

Can take two forms. 

As an element with items delimited by a newline.

```xml
<EmptyConstructor>
    <IncludeNamespaces>
        Foo
        Bar
    </IncludeNamespaces>
</EmptyConstructor>
```

Or as a attribute with items delimited by a pipe `|`.

```xml
<EmptyConstructor IncludeNamespaces='Foo|Bar'/>
```


## Icon

Icon courtesy of [The Noun Project](https://thenounproject.com)