# What is different in this fork? 

1. Fix for an infinite loop that occurs. This is documented in this bug (https://github.com/olifolkerd/tabulator/issues/2974 - It is not fully fixed yet, although it is closed there because we can't get a reproducible example yet). 

1. Unnecessary scroll bar appears. This is documented in this bug (https://github.com/olifolkerd/tabulator/issues/2975) - For this, I did a +1 for the pixel in the same routine as documented above. 

1. When I add an empty row, sometimes, the height of the row contents turns out to be very low (like 8px). I couldn't figure out the root-cause of this one yet. So, for now, an ugly workaround in `cell.js`:

``` js
Cell.prototype.getHeight = function(){
	// J:-> Ugly hack. Couldn't figure out why offsetHeight is so low (8px)
	// sometimes. 
	if (this.height) 
		return this.height;
	let h = Math.max(this.element.offsetHeight, 25);
	return h;
	//return this.height || this.element.offsetHeight;
};
```

