# Premise Language

Premise is a language and runtime for the Premise Abstract Machine (PAM). It provides a REPL, module system, knowledge-base integration, task runtime, and support for distributed agency.

## COPYRIGHT

 Copyright(c) 2013-2026 SubThought Corporation. All Rights Reserved.


  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
  OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.

  IN NO EVENT SHALL THE AUTHOR(S) OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM,
  DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
  ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE, ITS USE, OR OTHER
  DEALINGS IN THE SOFTWARE.

## DISCLAIMER 


The installation package, applications, source code examples, and user documentation and specifications are provided as is, without warranty of any kind, neither expressed nor implied that the applications, and source code examples work or are fit for a particular purpose. The authors and publisher, and creators assume no responsibility or liability for damages or losses, neither incidental nor consequential,  incurred as a result of using the provided specifications or source code, up to and including loss of business, injury, or death.  


Furthermore, the consequences of creating an artificial intelligence are unpredictable and unforeseeable and the user or developer assumes any and all responsibilities and associated risks if they undertake such an endeavor.  The user of this software holds harmless SubThought Corporation and its associates from any and all liability. "

## Getting Started

To use the Premise Language, download the Premise executable to a folder on your computer, then extract the file using standard decompression software.

To run the Premise evaluator, type the following at your operating system command line:

```text
premise
```

Example:

```text
C:\projects\SubThought\> premise
```

```text
[Premise :Version 3.3 :Build 20260301.0001 :OS Windows 11 :Edition Community]

Enter expressions followed by a blank line. For help type (help), (modules),
or (functions). To read files type (grok "url") or (grok "path/file.theory").
For legal information type (copyright) or (license). Type (bye) to exit.

> (copyright)

.: "Copyright (c) 2013-2026 SubThought Corporation, All Rights Reserved."

>
```

## Command Line Options

```text
--home url
        Sets the session start folder.

--repl yes | no
        If no, processes the command line and exits.
        If yes, displays the read evaluate print loop (REPL) console.

--eval "expression"
        Evaluates the expression in double quotes and emits the result.

--grok url
        Reads and evaluates the contents of the URL.

--use url
        Attaches to a knowledge base for the session.

--help
        Displays the man page.

--logs yes | no
        Toggles session logging. yes is default.
```

## Installation Folder Layout

```text
premise /            ← Premise installation folder
 │
 │   premise.exe
 │   premise.theory
 │
 ├── doc /           ← user documentation 
 │
 ├── lib /           ← modules: Apex, Base, IO, KB, Math, Peer, Rules, Tasks, User
 │    │
 │    ├── Apex /
 │    │    ├── apex.help
 │    │    └── apex.theory
 │    │
 │    ├── Base /
 │    │    ├── base.help
 │    │    └── base.theory
 │    │
 │    ├── IO /
 │    │    ├── io.help
 │    │    └── io.theory
 │    │
 │    ├── KB /
 │    │    ├── kb.help
 │    │    └── kb.theory
 │    │
 │    ├── Math /
 │    │    ├── math.help
 │    │    └── math.theory
 │    │
 │    ├── Peer /
 │    │    ├── peer.help
 │    │    └── peer.theory
 │    │
 │    ├── Rules /
 │    │    ├── rules.help
 │    │    └── rules.theory
 │    │
 │    └── Tasks /
 │         ├── tasks.help
 │         └── tasks.theory
 │
 ├── log /           ← session logging folder
 │ 
 ├── pkg /           ← external third-party, user-installed packages
 │    │
 │    └── User /
 │         └── user.theory
 │
 └── qed /           ← test suites
```

## Configuration

To configure itself, Premise groks the `premise.theory` file located in the home folder. Foundational libraries are located in the `lib/` subfolder and third-party packages are located in the `pkg/` subfolder.

See the user manual for more details.
