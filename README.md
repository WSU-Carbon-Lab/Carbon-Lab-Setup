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
These should all be simple, short, all lowercase names. These will be frequently included at the start of any program you write, so underscores should be avoided. If you must distinguish between similarly names modules written in different languages, use `Py_`, `Ipf_`, `C_` as a prefix in the file name. 

#### Variable Naming Conventions
