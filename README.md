# Use several prose linters for better text-quality

There are several prose linters available, which check your text and give some
useful advices how to optimize your language style.

This project uses `vale`, which uses these linters and provides nice
configuration options and extensions to make customizable for your needs:

![demo.mp4](demo.mp4)

## Configuration

All you need is in `vale.ini`. There you can specify the files, which should be checked (e.g. all `*.tex`-files).

You can add additional rules to specify a common language throughout all
publications. For example we use the spelling "D-BAS" and want it to be all the
same in our publications. These configurations can be set in an own configuration file, which can be found [styles/dbas/replacements.yml](styles/dbas/replacements.yml)

## Usage

You have to install `vale` (see [.gitlab-ci.yml](.gitlab-ci.yml)). Then given a file:

```tex
\documentclass{article}
\usepackage[parfill]{parskip}
\usepackage[utf8]{inputenc}

\begin{document}

\section*{Part a}

This is is a sample text.

dialog based

dbas

She is foo.

\end{document}
```

Call `vale` from the command line:

    vale .

produces the following output:

```bash
 master.tex
 9:6   warning  'is' is repeated!               write-good.Illusions 
 11:1  warning  Consider using 'dialog-based'   dbas.replacements    
                instead of 'dialog based'                            
 13:1  warning  Consider using 'D-BAS' instead  dbas.replacements    
                of 'dbas'                                            
 15:1  error    Avoid using 'She'               Joblint.Gendered     

✖ 1 error, 3 warnings and 0 suggestions in 1 file.

```