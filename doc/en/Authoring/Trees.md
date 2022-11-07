# Trees

It is sometime very useful to display the tree structure of an algebraic expression to a student.

For example, the HTEM code for the tree of \(1+2x^3\) is given below.

```
<figure>
<ul class='tree'>
  <li><code>+</code>
  <ul>
    <li><codeatom>\(1\)</codeatom></li>
    <li><codeatom>\(2\)</codeatom></li>
    <li><code>*</code>
    <ul>
      <li><codeatom>\(\pi\)</codeatom></li>
      <li><code>^</code>
      <ul>
        <li><codeatom>\(x\)</codeatom></li>
        <li><codeatom>\(3\)</codeatom></li>
      </ul></li>
    </ul></li>
  </ul></li>
</ul>
</figure>
```
This is displayed as follows (note LaTeX does not display correctly here).

<p>
<figure>
<ul class='tree'>
  <li><code>+</code>
  <ul>
    <li><codeatom>\(1\)</codeatom></li>
    <li><codeatom>\(2\)</codeatom></li>
    <li><code>*</code>
    <ul>
      <li><codeatom>\(\pi\)</codeatom></li>
      <li><code>^</code>
      <ul>
        <li><codeatom>\(x\)</codeatom></li>
        <li><codeatom>\(3\)</codeatom></li>
      </ul></li>
    </ul></li>
  </ul></li>
</ul>
</figure>
</p>


The tree is displayed in pure HTML using CSS via the `<ul class='tree'>`.  Such trees could be written in HTML by hand.

STACK provides a function `disptree` to generate the above tree diagram from a Maxima expression.  For example, use `{@disptree(1+2+pi*x^3)@}` in castext.  This function generates a string representing the tree of that expression, and is not an inert function.

STACK provides a function `treestop` to stop traversing the tree, and use the LaTeX of the subexpression instead.  For example in `disptree(1/treestop(1+x^2)=4)` STACK produces a tree but one node has \(1+x^2\), rather than also showing the subtree of this expression as well.  This gives the user some control over the complexity of tree and what to display.

<p>
<figure>
<ul class='tree'>
  <li><code>=</code>
  <ul>
    <li><code>/</code>
    <ul>
      <li><codeatom>\(1\)</codeatom></li>
      <li><codeatom>\(1+x^2\)</codeatom></li>
    </ul></li>
    <li><codeatom>\(4\)</codeatom></li>
  </ul></li>
</ul>
</figure>
</p>


Note, because of the HTML generated, and the LaTeX inside the tree HTML, you cannot embed these trees inside displayed LaTeX using `\[ ... \]`.  The only way to display a tree is using `{@disptree(....)@}` as an isolated mathematical expression.

## Examples

To see the tree structure of the binomial theorem (with `simp:false`)

`{@disptree(apply("+",map(lambda([ex],binomial(n,ex)*x^ex), ev(makelist(k,k,0,5),simp))))@}`

## Educational value of trees

Seeing the explicit tree structure of an expression has significant educational value at certain moments.  E.g. students want to type `x=a or b` as an answer. The following illustrates why they need to write `x=(a or b)` or `x=a or x=b` instead!

```
p1:x=a nounor b;
p2:x=(a nounor b);
```
with the following castext: `{@p1@}: {@disptree(p1)@}  <br/> {@p2@}: {@disptree(p2)@}` (with `simp:false`).


