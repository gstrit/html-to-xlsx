#phantom-html-to-pdf
[![Build Status](https://travis-ci.org/pofider/html-to-xlsx.png?branch=master)](https://travis-ci.org/pofider/html-to-xlsx)

> **node.js phantom wrapper for converting html to pdf in scale**

Yet another implementation of html to pdf conversion in node.js using phantomjs. This one differs from others in performance and scalability. Unlike others it allocates predefined number of phantomjs worker processes which are then managed and reused using FIFO strategy. This eliminates phantomjs process startup time and it also doesn't flood the system with dozens of phantomjs process under load.

```js
var conversion = require("phantom-html-to-pdf")();
conversion({ html: "<h1>Hello World</h1>" }, function(err, pdf) {
  console.log(pdf.numberOfPages);
  pdf.stream.pipe(res);
});
```

##Global options
```js
var conversion = require("phantom-html-to-pdf")({
    /* number of allocated phantomjs processes */
	numberOfWorkers: 2,
	/* timeout in ms for html conversion, when the timeout is reached, the phantom process is recycled */
	timeout: 5000,
	/* directory where are stored temporary html and pdf files, use something like npm package reaper to clean this up */
	tmpDir: "os/tmpdir"
});
```

##Local options

```js
conversion({
	html: "<h1>Hello world</h1>",
	header: "<h2>foo</h2>",
	footer: "<h2>foo</h2>",
	url: "http://jsreport.net",//set direct url instead of html
	printDelay: 0,//time in ms to wait before printing into pdf
	allowLocalFilesAccess: false,//set to true to allow request starting with file:///
	paperSize: {
		format, orientation, margin, width, height, headerHeight, footerHeight
	},
	customHeaders: [],
	settings: {
		javascriptEnabled : true
	},
	viewportSize: {
		width: 600,
		height: 600
	}
}, cb);
```

##License
See [license](https://github.com/pofider/phantom-html-to-pdf/blob/master/LICENSE)