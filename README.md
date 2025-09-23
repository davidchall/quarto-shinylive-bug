This gist contains a quarto website that demonstrates the use of the shinylive extension to run Shiny apps in the browser. A single webpage contains two Shiny apps, each in its own code block.

The bug is encountered when the two Shiny apps import from modules with conflicting names. For example, both apps import from a module named `helper.py`, but the contents of `helper.py` are different for each app. When the webpage is rendered, only one of the `helper.py` modules is loaded, causing import errors in the other app. The error message demonstrates the app is looking for a source file in the wrong location:

```sh
  File "/home/pyodide/app_0wpouot7xx0ufdvibcl1/app.py", line 1, in <module>
    from helper import helper1
ImportError: cannot import name 'helper1' from 'helper' (/home/pyodide/app_uwgf7rt7kak5fn8bus6x/helper.py). Did you mean: 'helper2'?
```

The Shiny apps are expected to run independently, each using its own version of `helper.py`. However, due to the naming conflict, they interfere with each other when loaded in the same webpage.
