# Converting to HTML with pandoc

basic command:

```shell
pandoc inputfile.md -o outputfile.html
```

The pitfall with this approach is that it does not include the header information, just an html block that would go inside the `<body>` tags.  So we need to do this instead:

```shell
pandoc -s inputfile.md -o outputfile.html
```

the `-s` option stands for `stand-alone` which is different than `self-contained` and creates a complete html document

Furthermore, the output looks pretty dry with these options.  There are some nice stylesheets that can be included to make the output much more readable and pleasant.  Currently I have ripped off a css file from the internet.  Include that CSS file in the same directory and linek with this:

```shell
pandoc -s -c pandoc.css inputfile.md -o outputfile.html
```
The one word of caution is this can cause some conflicts with any styling you might have for other things like code blocks so just watch out for that.

## using Math

When using latex expressions and converting to html it is required to specify which math engine will do the conversion

* `--mathml`
* `--webtex`
* `--mathjax`
* `--katex`

```shell
pandoc -s --mathjax -c pandoc.css inputfile.md -o outputfile.html
```

## Creating Self-Contained html files

using the `--self-contained` option embeds images as hex encoded byte-strings, and css files also embedded in the file so that everything is contained within the html file itself.

the `--mathjax` option conflicts with this as the mathjax script dynamically loads things and cannot be embedded as a self-contained file.  The html file must be manually altered in this case