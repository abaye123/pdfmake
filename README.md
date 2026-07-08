# @abaye123/pdfmake [![npm][npm_img]][npm_url]

[npm_img]: https://img.shields.io/npm/v/@abaye123/pdfmake.svg?colorB=0E7FBF
[npm_url]: https://www.npmjs.com/package/@abaye123/pdfmake


> **This is a fork of [pdfmake](https://github.com/bpampuch/pdfmake) v0.3.11 that adds bidirectional (RTL) text support.**
>
> All credit for pdfmake itself goes to [@bpampuch](https://github.com/bpampuch) and [@liborm85](https://github.com/liborm85).
> This fork tracks upstream and only adds the bidi layer described below.
>
> ```
> npm install @abaye123/pdfmake
> ```
>
> ```js
> const pdfmake = require('@abaye123/pdfmake');
> ```

## RTL / bidirectional text

Implements [UAX #9](https://www.unicode.org/reports/tr9/) visual reordering at the line level, so
Hebrew content renders in correct visual right-to-left order. Glyph shaping and per-run character
reversal are left to fontkit (already inside pdfkit); this fork handles what fontkit cannot see
across: inline ordering, bracket mirroring, RTL-only inlines, and per-script segmentation.

Set `rtl: true` on a text node, table, list, or in `defaultStyle`:

```js
const docDefinition = {
  defaultStyle: { font: 'Heebo', rtl: true },
  content: [
    'שלום עולם',
    { text: 'טקסט עם English באמצע ומספר 12345', rtl: true }
  ]
};
```

* When `rtl: true` and no explicit `alignment`, alignment defaults to `'right'`.
* Mixed Hebrew/Latin paragraphs **without** an explicit `rtl` flag still auto-reorder via bidi.
* In RTL mode, `margin: [left, top, right, bottom]` mirrors, so `margin[0]` is the visual-right margin.
* Tables with `rtl: true` reverse column order (colSpan-aware); lists put bullets/numbers on the right.
* Currency symbols (`₪ € £ ¥ $ ¢`) group with adjacent digits, so `₪3.50` stays one LTR run.

You must supply a font containing Hebrew glyphs — the bundled Roboto has none.
See [`examples/rtl_hebrew.js`](examples/rtl_hebrew.js) for a complete runnable demo.

**Not supported:** Arabic shaping (contextual/joining forms — needs HarfBuzz), and bidi explicit
embedding controls (LRE/RLE/PDF/LRI/RLI/FSI/PDI).

---

PDF document generation library for server-side and client-side in pure JavaScript.

Check out [the playground](http://bpampuch.github.io/pdfmake/playground.html) and [examples](https://github.com/bpampuch/pdfmake/tree/master/examples).

### Features

* line-wrapping,
* text-alignments (left, right, centered, justified),
* numbered and bulleted lists,
* tables and columns
  * auto/fixed/star-sized widths,
  * col-spans and row-spans,
  * headers automatically repeated in case of a page-break,
  * snaking columns (newspaper-style layout where content flows column-to-column),
* images and vector graphics,
* convenient styling and style inheritance,
* page headers and footers:
  * static or dynamic content,
  * access to current page number and page count,
* background-layer,
* page dimensions and orientations,
* margins,
* document sections,
* custom page breaks,
* font embedding,
* support for complex, multi-level (nested) structures,
* table of contents,
* helper methods for opening/printing/downloading the generated PDF,
* setting of PDF metadata (e.g. author, subject).

## Documentation

**Documentation URL: https://pdfmake.github.io/docs/**

Source of documentation: https://github.com/pdfmake/docs **Improvements are welcome!**

## Building from sources

using npm:
```
git clone https://github.com/bpampuch/pdfmake.git
cd pdfmake
npm install
npm run build
```

using yarn:
```
git clone https://github.com/bpampuch/pdfmake.git
cd pdfmake
yarn
yarn run build
```

## License
MIT

## Authors
* [@bpampuch](https://github.com/bpampuch) (founder)
* [@liborm85](https://github.com/liborm85)

pdfmake is based on a truly amazing library [pdfkit](https://github.com/devongovett/pdfkit) (credits to [@devongovett](https://github.com/devongovett)).

Thanks to all contributors.
