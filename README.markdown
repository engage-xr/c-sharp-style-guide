# The [Un]Official Immersive VR Education C# Style Guide

This style guide is based heavily on the raywenderlich.com style guide. As such, it may be a bit different from ones that you are used to, as it focuses on code legibility.   

Our overarching goals are **conciseness**, **readability** and **simplicity**. Also, this guide is written to keep **Unity** in mind. 

## Inspiration

This style guide is based on C# and Unity conventions. 

## Table of Contents

- [Nomenclature](#nomenclature)
  + [Namespaces](#namespaces)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Parameters](#parameters--parameters)
  + [Delegates](#delegates--delegates)
  + [Events](#events--events)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Interfaces](#interfaces)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Language](#language)
- [Copyright Statement](#copyright-statement)
- [Smiley Face](#smiley-face)
- [Credit](#credits)


## Nomenclature

On the whole, naming should follow C# standards.

### Namespaces

Namespaces are all **PascalCase**, multiple words concatenated together, without hyphens ( - ) or underscores ( \_ ). The exception to this rule are acronyms like GUI or HUD, which can be uppercase:

**AVOID**:

```csharp
com.engage.fpsgame.hud.healthbar
```

**PREFER**:

```csharp
Engage.FPSGame.HUD.Healthbar
```

On the whole, namespaces should be introduced and used throughout the Engage code base. 

**AVOID**:

```csharp
public class LVR_UI_IGM_Keyboard : MonoBehaviour
```

**PREFER**:

```csharp
namespace Engage.UI.Input
{
	public class Keyboard : Monobehaviour
```

We could even start to use namespaces to separate functionality for different platforms. 

### Classes & Interfaces

Classes and interfaces are written in **PascalCase**. For example `RadialSlider`. 

### Methods

Methods are written in **PascalCase**. For example `DoSomething()`. 

### Fields

All non-static fields are written **camelCase**. Per Unity convention, this includes **public fields** as well.

For example:

```csharp
public class MyClass 
{
    public int publicField;
    int packagePrivate;
    private int myPrivate;
    protected int myProtected;
}
```

**AVOID:**

```csharp
private int _myPrivateVariable;
public RectTransform rect_transform;
```

**PREFER:**

```csharp
private int myPrivateVariable;
public RectTransform rectTransform;
```

Static fields are the exception and should be written in **PascalCase**:

```csharp
public static int TheAnswer = 42;
```
### Properties

All properties are written in **PascalCase**. For example:

```csharp
public int PageNumber 
{
    get { return pageNumber; }
    set { pageNumber = value; }
}
```

### Parameters

Parameters are written in **camelCase**.

**AVOID:**

```csharp
void DoSomething(Vector3 Location)
```

**PREFER:**

```csharp
void DoSomething(Vector3 location)
```

Single character values are to be avoided except for temporary looping variables. As are nondescript parameters such as `arg0`

### Actions & Events

Actions and Events are written in **PascalCase**, and should be in an `OnEvent` format. For example:

```csharp
public event Action<int> OnValueChanged;
public UnityEvent OnUserLoggedIn;
```

### Misc

In code, acronyms should be treated as words. For example:

**AVOID:**

```csharp
XMLHTTPRequest
String URL
findPostByID
```  

**PREFER:**

```csharp
XmlHttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line. [I leave this one open to debate. I don't actually mind single line declarations where they make sense.]

**AVOID:**

```csharp
string username, twitterHandle;
```

**PREFER:**

```csharp
string username;
string twitterHandle;
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

### Interfaces

All interfaces should be prefaced with the letter **I**. 

**AVOID:**

```csharp
RadialSlider
```

**PREFER:**

```csharp
IRadialSlider
```

## Brace Style

All braces get their own line as it is a C# convention. This is the number one thing for making code more legible:

**AVOID:**

```csharp
class MyClass {
    void DoSomething() {
        if (someTest) {
          // ...
        } else {
          // ...
        }
    }
}
```

**PREFER:**

```csharp
class MyClass
{
    void DoSomething()
    {
        if (someTest)
        {
          // ...
        }
        else
        {
          // ...
        }
    }
}
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

**AVOID:**

```csharp
if (someTest)
    doSomething();  

if (someTest) doSomethingElse();
```

**PREFER:**

```csharp
if (someTest) 
{
    DoSomething();
}  

if (someTest)
{
    DoSomethingElse();
}
```
## Switch Statements

Switch-statements come with `default` case by default (heh). If the `default` case is never reached, be sure to remove it.

**AVOID:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
    default:
        break;
}
```

**PREFER:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
}
```

## Spacing

Spacing is another nice addition for legibility. This can be set in your IDE. 

### Indentation

Indentation should preferably be done using **spaces** — not tabs.  

#### Blocks

Indentation for blocks uses **4 spaces** for optimal readability:

**AVOID:**

```csharp
for (int i = 0; i < 10; i++) 
{
  Debug.Log("index=" + i);
}
```

**PREFER:**

```csharp
for (int i = 0; i < 10; i++) 
{
    Debug.Log("index=" + i);
}
```

#### Line Wraps

Indentation for line wraps should use **4 spaces** (not the default 8):

**AVOID:**

```csharp
CoolUiWidget widget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

**PREFER:**

```csharp
CoolUiWidget widget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

### Line Length

Lines should be no longer than **100** characters long. Break up long methods or expressions sensibly. For example:

```csharp
if (ENG_IGM_SharedIFXController.instance.sharedIFXModules.Count <= index || 
    ENG_IGM_SharedIFXController.instance.sharedIFXModules[index] == null ||
    !ENG_IGM_SharedIFXController.instance.sharedIFXModules[index].enabled)
{
	return null;
}
```

### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods.


## Language

This one's for Mike! Use US English spelling.

**AVOID:**

```csharp
string colour = "red";
```

**PREFER:**

```csharp
string color = "red";
```

The exception here is `MonoBehaviour` as that's what the class is actually called.

## Standard Header and the C# Template

Unity uses templates for when you generate a new script in the Editor. It's not a commonly known fact that these are editable! No more unnecessary `using System.Collections.Generic`

And not only is the template configurable, but you can use an editor script to manipulate your template, thanks to the `UnityEditor.AssetModificationProcessor` Below is the template I use. This is also included in the repo, along with the Editor file **KeywordReplace**, which replaces the variables inside **##** at import. 

```csharp
// /*-------------------------------------------
// ---------------------------------------------
// Creation Date: #CREATIONDATE#
// Author: #DEVELOPER#
// Description: #PROJECTNAME#
// Immersive VR Education
// ---------------------------------------------
// -------------------------------------------*/

using UnityEngine;

public class #SCRIPTNAME# : MonoBehaviour 
{


}
```

The template needs to replace the one saved at **Program Files\Unity\Hub\Editor\ [EDITOR_VERSION]\Editor\Data\Resources\ScriptTemplates**. Then **KeywordReplace** just needs to be within a folder called **Editor** inside your project. (I've already added it to ENGAGE_Main).

## Credits

As mentioned, this style guide is based on the one used by the raywenderlich.com Unity tutorial team members. Check out these cool guys on GitHub:

- [Darryl Bayliss](https://github.com/DarrylBayliss)
- [Sam Davies](https://github.com/sammyd)
- [Mic Pringle](https://github.com/micpringle)
- [Brian Moakley](https://github.com/VegetarianZombie)
- [Ray Wenderlich](https://github.com/rwenderlich)
- [Eric Van de Kerckhove](https://github.com/BlackDragonBE)

