[![Chat on Miaou][s4]][l4]

[s4]: https://miaou.dystroy.org/static/shields/room.svg
[l4]: https://miaou.dystroy.org/8?Javascript

# dom-doll

A nano Javascript lib to enchant the HTML DOM.

:warning: While the doll character (`$`) looks a lot like the dollar character (`$`), dom-doll doesn't try to mimic jQuery.
It makes jQuery useless in some new small projects but is neither a viable replacement in an already working application nor an alternative designed to please jQuery users or be easy to learn knowing jQuery.

## Usage: `$`

The doll function is designed to be used in a hierarchical and variadic way, each argument being either a CSS selector, an element, a collection of elements, some pseudo HTML for element creation, a function to apply to the previous collection, or a map of properties to change the previous element(s).

Here are a few introductory examples:

### Add elements to an existing one

```js
$("#content",
	$("<#infos.light",
		$("<a.big-link>Click Here!", {
			href: "https://github.com/Canop/glassbench",
			target: "_blank",
		}),
	),
	$("<#selectors"),
	$("<#view",
		$("<.tabs"),
		$("<.pages"),
	)
)
```

This add 3 elements in `#content`, giving them ids and or classes or text content.

The first of those elements is a `<div>` with id `infos` and class `light`. It contains a `<a>` element with class `big-link`.

The second added element is a `<div>` with id `selectors`.

The third element is a  ̀ <div>` with id `view`, containing two divs.

### Create an element, with children and callback

```js
let bench_name_select = $("<select.bench",
	{ change: update_task_name_select },
	bench_names.map(bn => $(`<option>${bn}`))
)
```

This create a `<select>`, with a callback for `change` events, and `<option>` elements created from a collection of names.

### Implementing a tab mechanism

```js
function unselect() {
	$("#view .tabs .tab, #view .pages .page", e => {
		e.classList.remove("selected")
	})
}
;["Table", "Graph"].forEach(name => {
	unselect()
	let page = $("<.page.selected", { id: name })
	let tab = $("<span.tab.selected", {
		textContent: name,
		click: () => {
			unselect()
			tab.classList.add("selected")
			page.classList.add("selected")
		}
	})
	$("#view .tabs", tab)
	$("#view .pages", page)
})
```

This adds two `.tab` elements in `#view .tabs` and two `.page` elements in `#view .pages`, and coordinates the `selected` class given to the clicked tab and its page.

### `$$`

The doll-doll function is a small convenience binding for ̀`document.querySelectorAll`.

