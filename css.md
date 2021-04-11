# CSS

## Margin collapse
Just read [this article](https://www.joshwcomeau.com/css/rules-of-margin-collapse/)

**Key facts:**
- margins control space between sibling elements
- padding controls space between a child and its parent

**Margins can collapse when:**
- elements are vertical
- element has a parent 
- multiple margins can collapse
- margins can collapse in the same direcrtion

**Margins can not collapse when:**
- element is not in flow but is `flex` or `grid` or float.
- parent has a blocking property such as padding or border or a height
- there is a blocking element in between siblings (e.g. `<br />` between paragraphs)

```html
<!-- margins will collapse unless the div has a height, border, or padding -->
<p>hello</p>
<div>
  <p>Margins will collapse</p>
</div>

<!-- if header, h1, and section all have margin of 10px but p.first has margin of 40px -->
<!-- there will be 40px between the word Hello and World because all collapse. -->
<header>
  <h1>Hello</h1>
</header>
<section>
  <p class="first">World!</p>
</section>
```
