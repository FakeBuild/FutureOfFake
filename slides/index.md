- title : Debugging & Root Cause Analysis
- description : debugging
- author : Matthias Dittrich
- theme : league
- transition : default

***

## Debugging & Root Cause Analysis

<img style="border-style: none" border="0" src="images/AIT-Logo_small.jpg" />

### **Matthias Dittrich**, AIT GmbH <br /> [@matthi\_\_d](http://twitter.com/matthi__d) | [github matthid](https://github.com/matthid) | [aitgmbh.de](http://www.aitgmbh.de/)

***

### Roadmap

- **Meta**

---

### Meta

- <s>why?</s>
- personal opinion
- your mileage may vary
- attention to details

---

### General considerations

- Removing Scope/Components
- Verifying results
- Zoom in
- Repeat

***


### Roadmap

- Meta
- **Environment/Overview**

---

### Get an overview

- What happens?
- Components/software involved?
- technical understanding
- Protocols?

---

### Duplicate & Reproduce

***


### Roadmap

- Meta
- Environment/Overview
- **Logs/Traces**

---

### Demo msbuild

' aa0d6ae8a20bbdcecb8502909544672b813aa0b0
' fake build
' fake build -s target BuildInstaller
' /c/Program\ Files\ \(x86\)/Microsoft\ Visual\ Studio/2017/Enterprise/MSBuild/15.0/Bin/MSBuild.exe source/{project}.sln "//t:Build" "//m" "//nodeReuse:False" "//p:RestorePackages=False" "//p:Optimize=True" "//p:DebugSymbols=True" "//p:Configuration=WiX" "//p:SolutionDir=C:\proj\{project}\source\\" "//v:d"

***

### Roadmap

- Meta
- Environment/Overview
- Logs/Traces
- **Last resort tricks & tools**
- Code

---

### Collect everything

- procexp - process tree and involved processes
- procmon
  - started processes and command line arguments
    (fast processes)
  - basic network access
  - Read files and registry values
- F12 Browser debugger -> network
- fiddler
- wireshark

***

### Roadmap

- Meta
- Environment/Overview
- Logs/Traces
- Last resort tricks & tools
- **Code**

---

### Reproducable?

- No?
- Can you add something to make the error/log useful next time?

---

### Learn to read logs/stacktraces

```
at Controllers.ValuesController.<GetValue2>d__3.MoveNext() --- End ... --- 
at System.Runtime.CompilerServices.TaskAwaiter.ThrowForNonSuccess(Task task) 
at System.Runtime.CompilerServices.TaskAwaiter.HandleNonSuccessAndDebuggerNotification(Task task) 
at System.Runtime.CompilerServices.ConfiguredTaskAwaitable`1.ConfiguredTaskAwaiter.GetResult()
at Controllers.ValuesController.<GetValue>d__0.MoveNext()
```

```
ConsoleApplication1.exe!Program.bazz@6-1.Invoke(System.String unitVar = null)
```


```
.ctor
.cctor
.get_Is64Bit()
<>
$
@
```

---

### Inner Exception

> "Exception has been thrown by the target of an invocation"

famous last words

---

### "Translate" Windows error codes

> 2147942405 or ‭-2147024891‬

Hex value?

> 0x80070005 

https://msdn.microsoft.com/en-us/library/cc231198.aspx

---

### "Translate" Windows error codes

> 0x00000005

https://msdn.microsoft.com/en-us/library/cc231199.aspx

-> `ERROR_ACCESS_DENIED`

-> What does that mean in my scenario?

---

### Understand HTTP status codes

---

### Simplify reproducing the problem

(Ideally in a test-case)

- Makes you faster
- Reduces the scope
- Makes debugging easier

---

### Learn to use the debugger

- Breakpoints
- Breakpoint on first chance exceptions
- Conditional breakpoints
- Working with symbol files (or decompile on demand)

> If you get a reproducable problem into the debugger it's basically solved.

---

### Debugging intractable code

- Your architecture might be the problem
- Reduce shared-state
- same input -> same output
- reduce side-effects

> If you can't follow/explain why a variable has a particular value, reconsider your implementation.

---

### Heisenbugs?

- Reduce
- Work without debugger, `printf` debugging
- If problem disappears when adding `printf` it might be a timing problem right there
- Move the `printf` around and note the results
- Verify results!

---

### Spy

- ILSpy
- DotPeek

---




### Thank you!

Further reading

- https://www.codementor.io/mattgoldspink/how-to-debug-code-efficiently-and-effectively-du107u9jh
