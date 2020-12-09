# CSS

## Margin collapse
Just read [this article](https://www.joshwcomeau.com/css/rules-of-margin-collapse/)

**Key facts:**
- margins control space between sibling elements
- padding controls space between a child and its parent

**Margins can collapse when:**
- margins only collapse between vertical elements
- margins can collapse even if an element has a parent
- multiple margins can collapse

**Margins can not collapse when:**
- element is not in flow but is `flex` or `grid` or float.
- parent has a blocking property such as padding or border
- there is a blocking element in between siblings (e.g. `<br />` between paragraphs)
