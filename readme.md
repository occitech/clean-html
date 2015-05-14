## HTML cleaner and beautifier

[![NPM Stats](https://nodei.co/npm/clean-html.png?downloads=true&downloadRank=true)](https://npmjs.org/packages/clean-html/)

Do you have crappy HTML? I do!

```html
<table width="100%" border="0" cellspacing="0" cellpadding="0">
        <tr>
          <td height="31"><b>Currently we have these articles available:</b>

        <blockquote>
              <p><a href="foo.html">The History of Foo</a><br />    
                An <span color="red">informative</span> piece  of <FONT FACE="ARIAL">information</FONT>.</p>
              <p><a href="bar.html">A Horse Walked Into a Bar</a><br/> The bartender said
                "Why the long face?"</p>
	</blockquote>
          </td>
        </tr>
      </table>
```

Just look at those blank lines and random line breaks, trailing spaces, mixed tabs, deprecated tags - it's outrageous!

Let's clean it up:

```javascript
var cleaner = require('clean-html'),
    fs = require('fs'),
    filename = process.argv[2];

fs.readFile(filename, function (err, data) {
    cleaner.clean(data, function (html) {
        console.log(html);
    });
});
```

Running this script on the file above produces the following output:

```html
<table>
  <tr>
    <td>
      <b>Currently we have these articles available:</b>
      <blockquote>
        <p>
          <a href="foo.html">The History of Foo</a><br>
          An <span>informative</span> piece of information.
        </p>
        <p>
          <a href="bar.html">A Horse Walked Into a Bar</a><br>
          The bartender said "Why the long face?"
        </p>
      </blockquote>
    </td>
  </tr>
</table>
```

You can pass additional options to the `clean` function like this:

```javascript
var options = {
    'add-tags-to-remove': ['table', 'tr', 'td', 'blockquote']
};

cleaner.clean(data, options, function (html) {
    console.log(html);
});
```

In this case, it produces:

```html
<b>Currently we have these articles available:</b>
<p>
  <a href="foo.html">The History of Foo</a><br>
  An <span>informative</span> piece of information.
</p>
<p>
  <a href="bar.html">A Horse Walked Into a Bar</a><br>
  The bartender said "Why the long face?"
</p>
```

Sanity restored!

## Options

### attr-to-remove

Attributes to remove from markup.

Type: Array  
Default: `['align', 'bgcolor', 'border', 'cellpadding', 'cellspacing', 'color', 'disabled', 'height', 'target', 'valign', 'width']`

### block-tags

Block level element tags. Line breaks are added before and after.

Type: Array  
Default: `['blockquote', 'div', 'h1', 'h2', 'h3', 'h4', 'h5', 'h6', 'hr', 'p', 'table', 'td', 'tr']`

### break-after-br

Adds line breaks after br tags.

Type: Boolean  
Default: `true`

### break-around-comments

Adds line breaks before and after comments.

Type: Boolean  
Default: `true`

### empty-tags

Empty element tags.

Type: Array  
Default: `['br', 'hr', 'img']`

### indent

The string to use for indentation. e.g., a tab character or one or more spaces.

Type: String  
Default: `'  '` (two spaces)

### remove-comments

Removes comments.

Type: Boolean  
Default: `false`

### remove-empty-paras

Removes empty paragraph tags.

Type: Boolean  
Default: `false`

### replace-nbsp

Replaces non-breaking white space entities (`&nbsp;`) with regular spaces.

Type: Boolean  
Default: `false`

### tags-to-remove

Tags to remove from markup. Nested content is not removed.

Type: Array  
Default: `['center', 'font']`

## Adding values to option lists

These options exist for your convenience.

### add-attr-to-remove

Additional attributes to remove from markup.

Type: Array  
Default: `null`

### add-block-tags

Additional block level element tags.

Type: Array  
Default: `null`

### add-empty-tags

Additional empty element tags.

Type: Array  
Default: `null`

### add-tags-to-remove

Additional tags to remove from markup.

Type: Array  
Default: `null`

## Global installation

If this package is installed globally, it can be used from the command line:

```bash
$ cat crappy.html | clean-html
```

Instead of piping the input from another program, you can supply a filename as the first argument:

```bash
$ clean-html crappy.html
```

You can redirect the output to another file:

```bash
$ clean-html crappy.html > clean.html
```

Or you can edit the file in place:

```bash
$ clean-html crappy.html --in-place
```

All of the options above can be used from the command line. Array option values should be separated by commas:

```bash
$ clean-html crappy.html --add-tags-to-remove b,i,u
```

Boolean options can be set to true like this:

```bash
$ clean-html crappy.html --break-after-br
```

Or like this

```bash
$ clean-html crappy.html --break-after-br true
```

They can be set to false like this:

```bash
$ clean-html crappy.html --break-after-br false
```
