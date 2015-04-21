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

Let's clean it up...

```bash
$ npm install clean-html
```

```javascript
var cleaner = require('clean-html'),
    fs = require('fs'),
    file = process.argv[2];

fs.readFile(file, 'utf-8', function (err, data) {
    process.stdout.write(cleaner.clean(data) + '\n');
});
```

Sanity restored!

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

## Options

### attr-to-remove

Attributes to remove from markup.

Type: Array  
Default: `['align', 'valign', 'bgcolor', 'color', 'width', 'height', 'border', 'cellpadding', 'cellspacing']`

### block-tags

Block level element tags. Line breaks are added before and after, and nested content is indented. Note: this option has no effect unless pretty print is enabled.

Type: Array  
Default: `['div', 'p', 'table', 'tr', 'td', 'blockquote', 'hr']`

### break-after-br

Adds line breaks after br tags. Note: this option has no effect unless pretty print is enabled.

Type: Boolean  
Default: `true`

### close-empty-tags

If set to true, adds trailing slashes to empty tags. Otherwise removes trailing slashes.

Type: Boolean  
Default: `false`

### empty-tags

Empty element tags. Used in combination with `close-empty-tags` option.

Type: Array  
Default: `['br', 'hr', 'img']`

### indent

The string to use for indentation. e.g., a tab character or one or more spaces. A falsy value indicates that the output should not be indented.

Type: String  
Default: `  `

### pretty

Pretty prints the output by adding line breaks and indentation.

Type: Boolean  
Default: `true`

### remove-comments

Removes comments.

Type: Boolean  
Default: `false`

### tags-to-remove

Tags to remove from markup.

Type: Array  
Default: `['font']`

## Adding values to option lists

These options are added for your convenience.

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

Type; Array  
Default: `null`

### add-tags-to-remove

Additional tags to remove from markup.

Type; Array  
Default: `null`