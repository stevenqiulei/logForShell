# logForShell

Used for Shell scripts. Focus on :

1. Fast problems locating.
2. Using "Caller" to generate calling stack of Shell source code.
3. Format of logs.
4. Clearly understand scripts step by step.

## Usage & Examples

**Import** logForShell in your first shell script:

```language-shell
source ./logForShell.sh
Show "Hello World"

2018-09-11 [10:07:21] Hello World
```

**If** you want some tag for logs, you can use:

```language-shell
source ./logForShell.sh [Shell]
Show "Using TAG to LOG"

2018-09-11 [10:08:26] [Shell] Using TAG to LOG
```

**If** you are running a group of shell scripts, please call `CleanFlagBeforeStart` in the first script. This can clean the failure flag which may be generated by the last execution or other scripts. If there is a failure flag, the method `Show` will not print anything.

```language-shell
CleanFlagBeforeStart
```

**In** the beginning of a shell script before doing something you can call `BeforeShell $@` This will print the running script's name and all the input parameters.

```language-shell
BeforeShell $@

2018-09-05 [17:52:21]
2018-09-05 [17:52:21]    +   test.sh  BEGIN   +
2018-09-05 [17:52:21]    +   test.sh -n -r -android 90   +
2018-09-05 [17:52:21]
```

**Also** you can call `AfterShell` to tell the ending of a script.

```language-shell
AfterShell

2018-09-05 [17:52:21]
2018-09-05 [17:52:21]    +   test.sh  FINISH   +
```

**When** running a new step, you can call `Step` function and input a *step number* and *step name*. This will print format logs for steps

```language-shell
Step 1 "Copy Unity Resource"

2018-09-05 [17:52:21]
2018-09-05 [17:52:21] ========== test.sh  STEP 1 : Copy Unity Resource ==========
2018-09-05 [17:52:21]
```

**When** you detect some steps succeed, you should call `ReportSuccess` to tell the success.

```language-shell
ReportSuccess "Build Dynamic Framework Project"	

****     Build Dynamic Framework Project SUCCESS      ****
```

**Also** when you find a failure or wrong conditions, you should call `ReportFailure`. This will automatically print the calling stack for you to locate the problem source code easily. And this will generate failure flag to stop the incoming `Show` method's output. In another word, logs will end here.

```language-shell
ReportFailure

****     line 10 test.sh REPORTED FAILURE     ****


    CALLER LIST
    - line 10 a test.sh
    - line 14 b test.sh
    - line 17 main test.sh

```

<font size="4">*contact author please email me 子博 : tingsven@163.com*</font>
