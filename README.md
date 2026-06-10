# The Premise Language

Premise is both a programming language and a platform. The Premise Abstract Machine (PAM) provides a REPL, compiler, module system, integrated knowledge-base, and a multi-tasking runtime supporting distributed agency via messaging across varied internet protocols.

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
 │   premise.grimoire
 │   premise.daicho
 │
 ├── doc /           ← documentation 
 │
 ├── lib /           ← modules: Apex, Base, IO, KB, Math, Peer, Rules, Tasks, User
 │    │
 │    ├── Apex /
 │    │    ├── apex.help
 │    │    └── apex.module
 │    │
 │    ├── Base /
 │    │    ├── base.help
 │    │    └── base.module
 │    │
 │    ├── IO /
 │    │    ├── io.help
 │    │    └── io.module
 │    │
 │    ├── KB /
 │    │    ├── kb.help
 │    │    └── kb.module
 │    │
 │    ├── Math /
 │    │    ├── math.help
 │    │    └── math.module
 │    │
 │    ├── Peer /
 │    │    ├── peer.help
 │    │    └── peer.module
 │    │
 │    ├── Rules /
 │    │    ├── rules.help
 │    │    └── rules.module
 │    │
 │    ├── Tasks /
 │    │    ├── tasks.help
 │    │    └── tasks.module
 │    │
 │    └── User /
 │         ├── user.help
 │         └── user.module
 │
 ├── log /           ← session logging folder
 │ 
 ├── pkg /           ← external third-party, user-installed packages
 │
 └── qed /           ← test suites
 
```

## Configuration

To configure itself, Premise groks the `premise.grimoire` file located in the home folder. Foundational modules are located in the `lib/` subfolder and third-party packages are located in the `pkg/` subfolder.

See the user manual for more details.



## CONTACT

For comments on the SubThought Premise Language contact:   premise.ai@gmail.com

For electronic inquiries or permissions contact:      subthought@hotmail.com.

by mail:  SubThought Corporation,  311 N. Robertson Blvd #301, Beverly Hills, CA 90211 USA


To report issues, problems, or bugs with the software, please email  premise.ai@gmail.com.

We will do our best to respond in a timely fashion. 

Watch this space for important updates:  https://github.com/subthought/Premise




Copyright(c) 2013-2026 SubThought Corporation. All Rights Reserved.



----  end of document  ---- 
