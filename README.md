# Setup
A set of instructions for standardizing the code base used by the Brian Collins research group at Washington State University

## Software Installation
The group works with four main programming languages 
1. Igor Pro / Wave Metrics 
2. Python
3. C++/C/C#
4. MATLAB

In general, you should not install every one of these languages; only install the ones you will be working on and using. 

### Igor Pro 
For a detailed description of Igor Pro on-boarding, see the [Igor-Standard-Procs](https://github.com/WSU-Carbon-Lab/Igor-Standard-Procs) repository. For the basic installation, download [Igor Pro 8](https://www.wavemetrics.com/downloads/current) and follow the installation setup guide. 

 
### Python
Our group uses python versions 3+ and makes heavy use of virtual environments issuing the Anaconda package manager. To get started with python, go to the [Anaconda](https://www.anaconda.com/) website and download the version for your current operating system. A more detailed description of onboarding for python development can be found in the [Python-Standard-Procs](https://github.com/WSU-Carbon-Lab/Python-Standard-Procs) repository. 


### C Languages
There is little code written in the C/C++/C# ecosystem, and as such we have no standard on-boarding procedures for it's development. It is recommended instead that you instead follow the installation directions provided by [Microsoft Visual Studios Code](https://code.visualstudio.com/docs/cpp/introvideos-cpp) in getting started with C programming. 


### MATLAB
Similarly so, MATLAB is rarely used in our code base. As you need a license for installing MATLAB, you must download the application though the [WSU MATLAB Portal](https://its.wsu.edu/software-site-licenses/).

# Style Guidelines
## Introduction
The Remainder of this document gives coding conventions for the code located in all other repositories developed by the Collins Lab Group. Many projects have their own coding style guidelines. In the event of any conflicts, such projects-specific guides take precedence for that project. Additionally, language specific guidelines such as the [Python PEP 8](https://peps.python.org/pep-0008/#introduction) Style Guide take priority for codes developed in their language. 

As a general philosophy these guidelines exist to improve readability of code. Thus, there are many points where developers should ignore particular guidelines. Some good reasons to ignore a particular guideline: 
- When applying the guideline would make the code less readable, even for someone who is used to reading the code. 
- To be consistent with surrounding code that breaks the guide (Though you could be nice and fix someone elses code).
- Because the code is historic and it would be a waste of time to modify it.
- When there is a general compatibility issue preventing the change. 

## Code Lay-Out
### White Space and Indentation
- Use 4 spaces for indentation (You can configure most IDEs to map the tab key to 4-spaces)
- Lines should in generally be limited to 79 characters long. 
- Where possible, functions should use indentation and white space as opposed to more compact layouts. 

## Naming Conventions
The naming conventions across each repository are a bit of a mess, so things will never be entirely consistent, but this still contains the recommended naming schemes. 
### Naming Styles
There are allot of different naming styles that could be used in any one project. The following styles are the most frequent, and preferred naming conventions:
- `b` (single lower case letter)
- `B` (single upper case letter)
- `lowercase` 
- `lowercase_with_underscores` (Called pothole case of snake case)
- `UPPERCASE`
- `UPPERCASE_WITH_UNDERSCORES`
- `CapitalizedWords` (Called CapWords or CamelCase; Note: all letters in an acronym should be capitalized)
- `mixedCase` (Like CamelCase but with lowercase first word)
- `Capitalized_Words_With_Underscores` (ugly! don't use this)

Any of these naming schemes can be augmented with the addition of a prefix in any other naming convention such as `PyRSOXS_lowercase` or with a single underscore such as `_lowercase` (You should reserve the single underscore to use as a weak internal use indicator). Similarly, suffixes can be applied in the same manors. In all cases double underscore `__` should be avoided.

### Naming Conventions
#### Things to Avoid
Never use characters such as 'O' (confused for 0), or 'l' (confused for 1) as these can be indistinguishable in some fonts. 

#### Packages, Modules, Libraries
These variable names should all be simple, short, all lowercase names. These will be frequently included at the start of any program you write, so underscores should be avoided. If you must distinguish between similarly names modules written in different languages, use `Py_`, `Ipf_`, `C_`, etc. as a prefix in the file name. 
#### Variable Naming Conventions
Exact naming for variables is generally left for individual repositories. 

Some general guidelines for variable naming:
- Single lowercase letters `b` are generally only suitable as index variables. There are some exceptions to this such as, `c` defining the speed of light, but explicit variable names such as `SpeedOfLight` should never hurt the readability of code. 
- Single uppercase letters `B` should generally be avoided.
- `UPPERCASE`, and `UPPERCASE_WITH_UNDERSCORES` variable names should be used on static global constants that are never altered in any functions.
- `Capitalized_Words_With_Underscores` Should be avoided at all cost as it is ugly and simply adds more characters to an already long variable name. 

This leaves `lowercase`, `snake_case`, `CamelCase`, and `mixedCase` variable names free for use in functions, variables, classes and methods.

#### Functions, Classes, Methods, etc
While Object oriented programming is prolific in the computer science world, objects should be avoided like the plague. Badly written objects are a nightmare to debug, especially when the original author has since left the project. In the case that objects are needed for a program to function, composition is favorable to inheritance. 

In general, functions will be interacted with more frequently when processing data making it easier if they use `mixedCase` or `CamelCase` names. This leaves variables to use `lower_case` and `snake_case` naming schemes. If objects are needed in the program, `mixedCase` and `CamelCase` names should be used in their invention. Methods should then follow the naming scheme used by the functions in the remainder of the script.

#### Types
In Python and other interpreted languages, variable types are dynamically evaluated at run time. This can lead to bugs when functions expect to be passed specific data types that has since been altered. An example of this can be seen here. 
```
A = 10
B = 20

...

A = '10'

def add(x, y):
    return x + y

print(add(A,B))
```
This issue exists because variable types are not explicit. To fix this in all languages, variable types should be explicitly defined in the code. This improves readability and prevents errors. In C languages, the `auto` type should be avoided at all cost. An example of this fixed is 
```
A : int= 10
B : int= 20

...

def add(x : int, y : int) -> int:
    return x + y

print(add(A,B))
```
## Documentation and Comments
### Comments
Comments should be used to describe the process the code is taking, not what each line is doing. For example,
```
i++ // increments i by 1
```
is a do nothing comment that only serves to clutter the code. Instead, doc strings should be implemented wherever possible to document what operations a function preforms. For example:
```
def sample_dir(data_dir: Path, destination: Path | None = None) -> None:
    """
    Collects the sample name from the file name for each fits file in 
    the data_dir path. Generates a new subfolder at the destination 
    path.
    Parameters
    ----------
    data_dir : Path
        Directory with the data located in it
    destination : Path, optional
        Destination folder where each sub directory will be generated, 
        by default None signifying the destination path as
            >>> destination = data_dir / 'Sorted'
    """
```
This doc string defines the procedure that the function takes, It describes the input variables, their data types, and their default values. 

Side comments still have a place, in highlighting important points in an algorithm. For example:
```
hc = 12000      // This conversion uses Angstroms instead of nanometers
```

Note that good variable names can go a long way to replace code commenting.
### Documentation
Much of our code is left without documentation, as much of out development time is spend testing, using, writing, and debugging. The industry standard uses [Doxygen](https://www.doxygen.nl/) to automate the documentation of any code. 