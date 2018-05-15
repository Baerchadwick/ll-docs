# MARKDOWN BASICS

You should probably just check out [THIS guide](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#emphasis), but we'll create an **EXTREMELY** short version here with just the basics.

## Headings
To insert a heading, just add one or more `#` characters (followed by a space) at the beginning of the line. `#` will give you an `h1`, `##` will give you an `h2`, etc. For instance, at the beginning of this section we typed
```
## Headings
```
Go ahead and view the [raw text](https://raw.githubusercontent.com/learninglab-dev/ll-docs/master/workflow/instructions/markdown_basics.md) for this doc to verify if you'd like.

## Lists
To insert a list, just add an `*` or a `-` plus a space for an unordered list or a number for an ordered list.  For instance:
```
  - element 1
  - element two
  - three
```
Will give you

- element 1
- element two
- three  

And  
```
  1. element 1
  2. element two
  3. three
```

Will give you

1. element 1
2. element two  
3. three  

## Emphasis

In order to italicize text, surround it in `_` characters: `_text_` will give you _text_.
In order to make text bold, surround it in `**` characters: `**text**` will give you **text**.

## Code

To mark text as code, surround it in \` tags if it is a single word or two in the flow of the text. Or, if it's a block, use \`\`\` at the beginning and end of the block.

## Links

For links, surround the text you want the viewer to click with `[ ]` and surround the link itself with `( )`.  For instance to get a link that says "[click here for cats](https://giphy.com/explore/cat)" you would type:
```
  [click here for cats](https://giphy.com/explore/cat)
```

## Images

Images are extremely similar to links.  Just add
1. `!`
2. the text you'd like screenreaders or bandwidth-constrained users to get surrounded by `[ ]`
3. the link to the image surrounded by `( )`

For instance, to get
 ![random-cat](https://upload.wikimedia.org/wikipedia/commons/b/bb/Kittyply_edit1.jpg)
  you would type:
```
  ![random-cat](https://upload.wikimedia.org/wikipedia/commons/b/bb/Kittyply_edit1.jpg)
```
