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
[Premise :Version 3.4.αlpha :Build 20260914.1745 :OS "Microsoft Windows 10.0.19045" :Edition Community]

Enter expressions then press the [Enter] key twice. Type (grok "path/file") to read a file.
For general information type (about), (copyright), (license).  For general help type (help).
Use [Page Up] and [Page Down] to scroll through prior entries. Type (bye) to exit.

Email premise.ai@gmail.com for support.

> (copyright)

.: "Copyright (c) 2013-2026 SubThought Corporation, All Rights Reserved."

>
```

To read and evaluate a file and then exit, name it on the command line:

```text
C:\projects\SubThought\> premise eg/mandelbrot.theory
```

Premise groks the file, runs it to completion, and exits — either when all
processes are done or when the source reaches `(bye)`.

## Command Line Options

```text
url
        Reads and evaluates the contents of the URL, then exits when the
        work is done or the source reaches (bye).

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

--version
        Prints the Premise version banner and exits.
```

## Installation Folder Layout

```text

premise /            ← Premise installation folder
 │
 │   premise.exe
 │
 ├── cfg /           ← configuration
 │    ├── premise.grimoire   (grammar)
 │    └── premise.daicho     (settings)
 │     
 ├── doc /           ← documentation 
 │
 ├── eg  /           ← examples
 │
 ├── ken /           ← knowledge: gnosis checkpoints and backups
 │
 ├── lib /           ← modules: Apex, Base, IO, KB, Math, Peer, Rules, Tasks, User
 │    │
 │    ├── apex /
 │    │    ├── apex.help
 │    │    └── apex.module
 │    │
 │    ├── base /
 │    │    ├── base.help
 │    │    └── base.module
 │    │
 │    ├── io /
 │    │    ├── io.help
 │    │    └── io.module
 │    │
 │    ├── kb /
 │    │    ├── kb.help
 │    │    └── kb.module
 │    │
 │    ├── math /
 │    │    ├── math.help
 │    │    └── math.module
 │    │
 │    ├── peer /
 │    │    ├── peer.help
 │    │    └── peer.module
 │    │
 │    ├── rules /
 │    │    ├── rules.help
 │    │    └── rules.module
 │    │
 │    ├── tasks /
 │    │    ├── tasks.help
 │    │    └── tasks.module
 │    │
 │    └── user /
 │         ├── user.help
 │         └── user.module
 │
 ├── log /           ← session logging folder
 │ 
 ├── pkg /           ← packages: knowledge-base and I/O adapters,
 │    │                and third-party, user-installed packages
 │    │
 │    └── ephemeral-kb /    ← the default in-memory knowledge base
 │
 └── qed /           ← test suites
 
```

## Configuration

To configure itself, Premise groks the `premise.daicho` file for settings and
the `premise.grimoire` file for grammar, both located in the `cfg/` subfolder
of the home folder. Foundational modules are located in the `lib/` subfolder,
knowledge-base and I/O adapters together with third-party packages are located
in the `pkg/` subfolder, and knowledge persists to the `ken/` subfolder.

See the user manual for more details.


## What's New in 3.4

- **Beat** — an unsigned 128-bit ordinal time value, written `\@b{n}`, for a
  position in a narrative sequence or a musical piece. A beat combines and
  compares only with another beat; convert a number with `(beat n)` first.

- **`%%` (script)** — performs many operating system commands in one shell, so
  a directory change, an exported variable, or an activated environment
  persists from one command to the next. Execution stops at the first command
  returning a non-zero result.

- **Bare url on the command line** — `premise file.theory` groks the file and
  exits, without entering the REPL.

- **`--version`** — prints the version banner and exits.



## CONTACT

For comments on the SubThought Premise Language contact:   premise.ai@gmail.com

For electronic inquiries or permissions contact:      subthought@hotmail.com.

by mail:  SubThought Corporation,  311 N. Robertson Blvd #301, Beverly Hills, CA 90211 USA


To report issues, problems, or bugs with the software, please email  premise.ai@gmail.com.

We will do our best to respond in a timely fashion. 

Watch this space for important updates:  https://github.com/subthought/Premise




Copyright(c) 2013-2026 SubThought Corporation. All Rights Reserved.



----  end of document  ---- 
