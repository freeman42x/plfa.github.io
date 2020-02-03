---
src       : "src/plfa/part1/Connectives.lagda.md"
title     : "Connectives: Conjunction, disjunction, and implication"
layout    : page
prev      : /Isomorphism/
permalink : /Connectives/
next      : /Negation/
---

{% raw %}<pre class="Agda"><a id="175" class="Keyword">module</a> <a id="182" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}" class="Module">plfa.part1.Connectives</a> <a id="205" class="Keyword">where</a>
</pre>{% endraw %}
<!-- The ⊥ ⊎ A ≅ A exercise requires a (inj₁ ()) pattern,
     which the reader will not have seen. Restore this
     exercise, and possibly also associativity? Take the
     exercises from the final sections on distributivity
     and exponentials? -->

This chapter introduces the basic logical connectives, by observing a
correspondence between connectives of logic and data types, a
principle known as _Propositions as Types_:

  * _conjunction_ is _product_,
  * _disjunction_ is _sum_,
  * _true_ is _unit type_,
  * _false_ is _empty type_,
  * _implication_ is _function space_.


## Imports

{% raw %}<pre class="Agda"><a id="821" class="Keyword">import</a> <a id="828" href="https://agda.github.io/agda-stdlib/v1.1/Relation.Binary.PropositionalEquality.html" class="Module">Relation.Binary.PropositionalEquality</a> <a id="866" class="Symbol">as</a> <a id="869" class="Module">Eq</a>
<a id="872" class="Keyword">open</a> <a id="877" href="https://agda.github.io/agda-stdlib/v1.1/Relation.Binary.PropositionalEquality.html" class="Module">Eq</a> <a id="880" class="Keyword">using</a> <a id="886" class="Symbol">(</a><a id="887" href="Agda.Builtin.Equality.html#125" class="Datatype Operator">_≡_</a><a id="890" class="Symbol">;</a> <a id="892" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a><a id="896" class="Symbol">)</a>
<a id="898" class="Keyword">open</a> <a id="903" href="https://agda.github.io/agda-stdlib/v1.1/Relation.Binary.PropositionalEquality.Core.html#2499" class="Module">Eq.≡-Reasoning</a>
<a id="918" class="Keyword">open</a> <a id="923" class="Keyword">import</a> <a id="930" href="https://agda.github.io/agda-stdlib/v1.1/Data.Nat.html" class="Module">Data.Nat</a> <a id="939" class="Keyword">using</a> <a id="945" class="Symbol">(</a><a id="946" href="Agda.Builtin.Nat.html#165" class="Datatype">ℕ</a><a id="947" class="Symbol">)</a>
<a id="949" class="Keyword">open</a> <a id="954" class="Keyword">import</a> <a id="961" href="https://agda.github.io/agda-stdlib/v1.1/Function.html" class="Module">Function</a> <a id="970" class="Keyword">using</a> <a id="976" class="Symbol">(</a><a id="977" href="https://agda.github.io/agda-stdlib/v1.1/Function.html#1099" class="Function Operator">_∘_</a><a id="980" class="Symbol">)</a>
<a id="982" class="Keyword">open</a> <a id="987" class="Keyword">import</a> <a id="994" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}" class="Module">plfa.part1.Isomorphism</a> <a id="1017" class="Keyword">using</a> <a id="1023" class="Symbol">(</a><a id="1024" href="plfa.part1.Isomorphism.html#4365" class="Record Operator">_≃_</a><a id="1027" class="Symbol">;</a> <a id="1029" href="plfa.part1.Isomorphism.html#9186" class="Record Operator">_≲_</a><a id="1032" class="Symbol">;</a> <a id="1034" href="plfa.part1.Isomorphism.html#2684" class="Postulate">extensionality</a><a id="1048" class="Symbol">)</a>
<a id="1050" class="Keyword">open</a> <a id="1055" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#8421" class="Module">plfa.part1.Isomorphism.≃-Reasoning</a>
</pre>{% endraw %}

## Conjunction is product

Given two propositions `A` and `B`, the conjunction `A × B` holds
if both `A` holds and `B` holds.  We formalise this idea by
declaring a suitable inductive type:
{% raw %}<pre class="Agda"><a id="1290" class="Keyword">data</a> <a id="_×_"></a><a id="1295" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1295" class="Datatype Operator">_×_</a> <a id="1299" class="Symbol">(</a><a id="1300" href="plfa.part1.Connectives.html#1300" class="Bound">A</a> <a id="1302" href="plfa.part1.Connectives.html#1302" class="Bound">B</a> <a id="1304" class="Symbol">:</a> <a id="1306" class="PrimitiveType">Set</a><a id="1309" class="Symbol">)</a> <a id="1311" class="Symbol">:</a> <a id="1313" class="PrimitiveType">Set</a> <a id="1317" class="Keyword">where</a>

  <a id="_×_.⟨_,_⟩"></a><a id="1326" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨_,_⟩</a> <a id="1332" class="Symbol">:</a>
      <a id="1340" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1300" class="Bound">A</a>
    <a id="1346" class="Symbol">→</a> <a id="1348" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1302" class="Bound">B</a>
      <a id="1356" class="Comment">-----</a>
    <a id="1366" class="Symbol">→</a> <a id="1368" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1300" class="Bound">A</a> <a id="1370" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="1372" href="plfa.part1.Connectives.html#1302" class="Bound">B</a>
</pre>{% endraw %}Evidence that `A × B` holds is of the form `⟨ M , N ⟩`, where `M`
provides evidence that `A` holds and `N` provides evidence that `B`
holds.

Given evidence that `A × B` holds, we can conclude that either
`A` holds or `B` holds:
{% raw %}<pre class="Agda"><a id="proj₁"></a><a id="1611" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1611" class="Function">proj₁</a> <a id="1617" class="Symbol">:</a> <a id="1619" class="Symbol">∀</a> <a id="1621" class="Symbol">{</a><a id="1622" href="plfa.part1.Connectives.html#1622" class="Bound">A</a> <a id="1624" href="plfa.part1.Connectives.html#1624" class="Bound">B</a> <a id="1626" class="Symbol">:</a> <a id="1628" class="PrimitiveType">Set</a><a id="1631" class="Symbol">}</a>
  <a id="1635" class="Symbol">→</a> <a id="1637" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1622" class="Bound">A</a> <a id="1639" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="1641" href="plfa.part1.Connectives.html#1624" class="Bound">B</a>
    <a id="1647" class="Comment">-----</a>
  <a id="1655" class="Symbol">→</a> <a id="1657" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1622" class="Bound">A</a>
<a id="1659" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1611" class="Function">proj₁</a> <a id="1665" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="1667" href="plfa.part1.Connectives.html#1667" class="Bound">x</a> <a id="1669" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="1671" href="plfa.part1.Connectives.html#1671" class="Bound">y</a> <a id="1673" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="1675" class="Symbol">=</a> <a id="1677" href="plfa.part1.Connectives.html#1667" class="Bound">x</a>

<a id="proj₂"></a><a id="1680" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1680" class="Function">proj₂</a> <a id="1686" class="Symbol">:</a> <a id="1688" class="Symbol">∀</a> <a id="1690" class="Symbol">{</a><a id="1691" href="plfa.part1.Connectives.html#1691" class="Bound">A</a> <a id="1693" href="plfa.part1.Connectives.html#1693" class="Bound">B</a> <a id="1695" class="Symbol">:</a> <a id="1697" class="PrimitiveType">Set</a><a id="1700" class="Symbol">}</a>
  <a id="1704" class="Symbol">→</a> <a id="1706" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1691" class="Bound">A</a> <a id="1708" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="1710" href="plfa.part1.Connectives.html#1693" class="Bound">B</a>
    <a id="1716" class="Comment">-----</a>
  <a id="1724" class="Symbol">→</a> <a id="1726" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1693" class="Bound">B</a>
<a id="1728" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1680" class="Function">proj₂</a> <a id="1734" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="1736" href="plfa.part1.Connectives.html#1736" class="Bound">x</a> <a id="1738" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="1740" href="plfa.part1.Connectives.html#1740" class="Bound">y</a> <a id="1742" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="1744" class="Symbol">=</a> <a id="1746" href="plfa.part1.Connectives.html#1740" class="Bound">y</a>
</pre>{% endraw %}If `L` provides evidence that `A × B` holds, then `proj₁ L` provides evidence
that `A` holds, and `proj₂ L` provides evidence that `B` holds.

Equivalently, we could also declare conjunction as a record type:
{% raw %}<pre class="Agda"><a id="1965" class="Keyword">record</a> <a id="_×′_"></a><a id="1972" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1972" class="Record Operator">_×′_</a> <a id="1977" class="Symbol">(</a><a id="1978" href="plfa.part1.Connectives.html#1978" class="Bound">A</a> <a id="1980" href="plfa.part1.Connectives.html#1980" class="Bound">B</a> <a id="1982" class="Symbol">:</a> <a id="1984" class="PrimitiveType">Set</a><a id="1987" class="Symbol">)</a> <a id="1989" class="Symbol">:</a> <a id="1991" class="PrimitiveType">Set</a> <a id="1995" class="Keyword">where</a>
  <a id="2003" class="Keyword">field</a>
    <a id="_×′_.proj₁′"></a><a id="2013" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#2013" class="Field">proj₁′</a> <a id="2020" class="Symbol">:</a> <a id="2022" href="plfa.part1.Connectives.html#1978" class="Bound">A</a>
    <a id="_×′_.proj₂′"></a><a id="2028" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#2028" class="Field">proj₂′</a> <a id="2035" class="Symbol">:</a> <a id="2037" href="plfa.part1.Connectives.html#1980" class="Bound">B</a>
<a id="2039" class="Keyword">open</a> <a id="2044" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1972" class="Module Operator">_×′_</a>
</pre>{% endraw %}Here record construction

    record
      { proj₁′ = M
      ; proj₂′ = N
      }

corresponds to the term

    ⟨ M , N ⟩

where `M` is a term of type `A` and `N` is a term of type `B`.

When `⟨_,_⟩` appears in a term on the right-hand side of an equation
we refer to it as a _constructor_, and when it appears in a pattern on
the left-hand side of an equation we refer to it as a _destructor_.
We may also refer to `proj₁` and `proj₂` as destructors, since they
play a similar role.

Other terminology refers to `⟨_,_⟩` as _introducing_ a conjunction, and
to `proj₁` and `proj₂` as _eliminating_ a conjunction; indeed, the
former is sometimes given the name `×-I` and the latter two the names
`×-E₁` and `×-E₂`.  As we read the rules from top to bottom,
introduction and elimination do what they say on the tin: the first
_introduces_ a formula for the connective, which appears in the
conclusion but not in the hypotheses; the second _eliminates_ a
formula for the connective, which appears in a hypothesis but not in
the conclusion. An introduction rule describes under what conditions
we say the connective holds---how to _define_ the connective. An
elimination rule describes what we may conclude when the connective
holds---how to _use_ the connective.

(The paragraph above was adopted from "Propositions as Types", Philip Wadler,
_Communications of the ACM_, December 2015.)

In this case, applying each destructor and reassembling the results with the
constructor is the identity over products:
{% raw %}<pre class="Agda"><a id="η-×"></a><a id="3562" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#3562" class="Function">η-×</a> <a id="3566" class="Symbol">:</a> <a id="3568" class="Symbol">∀</a> <a id="3570" class="Symbol">{</a><a id="3571" href="plfa.part1.Connectives.html#3571" class="Bound">A</a> <a id="3573" href="plfa.part1.Connectives.html#3573" class="Bound">B</a> <a id="3575" class="Symbol">:</a> <a id="3577" class="PrimitiveType">Set</a><a id="3580" class="Symbol">}</a> <a id="3582" class="Symbol">(</a><a id="3583" href="plfa.part1.Connectives.html#3583" class="Bound">w</a> <a id="3585" class="Symbol">:</a> <a id="3587" href="plfa.part1.Connectives.html#3571" class="Bound">A</a> <a id="3589" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="3591" href="plfa.part1.Connectives.html#3573" class="Bound">B</a><a id="3592" class="Symbol">)</a> <a id="3594" class="Symbol">→</a> <a id="3596" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="3598" href="plfa.part1.Connectives.html#1611" class="Function">proj₁</a> <a id="3604" href="plfa.part1.Connectives.html#3583" class="Bound">w</a> <a id="3606" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="3608" href="plfa.part1.Connectives.html#1680" class="Function">proj₂</a> <a id="3614" href="plfa.part1.Connectives.html#3583" class="Bound">w</a> <a id="3616" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="3618" href="Agda.Builtin.Equality.html#125" class="Datatype Operator">≡</a> <a id="3620" href="plfa.part1.Connectives.html#3583" class="Bound">w</a>
<a id="3622" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#3562" class="Function">η-×</a> <a id="3626" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="3628" href="plfa.part1.Connectives.html#3628" class="Bound">x</a> <a id="3630" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="3632" href="plfa.part1.Connectives.html#3632" class="Bound">y</a> <a id="3634" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="3636" class="Symbol">=</a> <a id="3638" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
</pre>{% endraw %}The pattern matching on the left-hand side is essential, since
replacing `w` by `⟨ x , y ⟩` allows both sides of the
propositional equality to simplify to the same term.

We set the precedence of conjunction so that it binds less
tightly than anything save disjunction:
{% raw %}<pre class="Agda"><a id="3921" class="Keyword">infixr</a> <a id="3928" class="Number">2</a> <a id="3930" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1295" class="Datatype Operator">_×_</a>
</pre>{% endraw %}Thus, `m ≤ n × n ≤ p` parses as `(m ≤ n) × (n ≤ p)`.

Given two types `A` and `B`, we refer to `A × B` as the
_product_ of `A` and `B`.  In set theory, it is also sometimes
called the _Cartesian product_, and in computing it corresponds
to a _record_ type. Among other reasons for
calling it the product, note that if type `A` has `m`
distinct members, and type `B` has `n` distinct members,
then the type `A × B` has `m * n` distinct members.
For instance, consider a type `Bool` with two members, and
a type `Tri` with three members:
{% raw %}<pre class="Agda"><a id="4478" class="Keyword">data</a> <a id="Bool"></a><a id="4483" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4483" class="Datatype">Bool</a> <a id="4488" class="Symbol">:</a> <a id="4490" class="PrimitiveType">Set</a> <a id="4494" class="Keyword">where</a>
  <a id="Bool.true"></a><a id="4502" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4502" class="InductiveConstructor">true</a>  <a id="4508" class="Symbol">:</a> <a id="4510" href="plfa.part1.Connectives.html#4483" class="Datatype">Bool</a>
  <a id="Bool.false"></a><a id="4517" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4517" class="InductiveConstructor">false</a> <a id="4523" class="Symbol">:</a> <a id="4525" href="plfa.part1.Connectives.html#4483" class="Datatype">Bool</a>

<a id="4531" class="Keyword">data</a> <a id="Tri"></a><a id="4536" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4536" class="Datatype">Tri</a> <a id="4540" class="Symbol">:</a> <a id="4542" class="PrimitiveType">Set</a> <a id="4546" class="Keyword">where</a>
  <a id="Tri.aa"></a><a id="4554" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4554" class="InductiveConstructor">aa</a> <a id="4557" class="Symbol">:</a> <a id="4559" href="plfa.part1.Connectives.html#4536" class="Datatype">Tri</a>
  <a id="Tri.bb"></a><a id="4565" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4565" class="InductiveConstructor">bb</a> <a id="4568" class="Symbol">:</a> <a id="4570" href="plfa.part1.Connectives.html#4536" class="Datatype">Tri</a>
  <a id="Tri.cc"></a><a id="4576" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4576" class="InductiveConstructor">cc</a> <a id="4579" class="Symbol">:</a> <a id="4581" href="plfa.part1.Connectives.html#4536" class="Datatype">Tri</a>
</pre>{% endraw %}Then the type `Bool × Tri` has six members:

    ⟨ true  , aa ⟩    ⟨ true  , bb ⟩    ⟨ true ,  cc ⟩
    ⟨ false , aa ⟩    ⟨ false , bb ⟩    ⟨ false , cc ⟩

For example, the following function enumerates all
possible arguments of type `Bool × Tri`:
{% raw %}<pre class="Agda"><a id="×-count"></a><a id="4841" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4841" class="Function">×-count</a> <a id="4849" class="Symbol">:</a> <a id="4851" href="plfa.part1.Connectives.html#4483" class="Datatype">Bool</a> <a id="4856" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="4858" href="plfa.part1.Connectives.html#4536" class="Datatype">Tri</a> <a id="4862" class="Symbol">→</a> <a id="4864" href="Agda.Builtin.Nat.html#165" class="Datatype">ℕ</a>
<a id="4866" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4841" class="Function">×-count</a> <a id="4874" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="4876" href="plfa.part1.Connectives.html#4502" class="InductiveConstructor">true</a>  <a id="4882" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="4884" href="plfa.part1.Connectives.html#4554" class="InductiveConstructor">aa</a> <a id="4887" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>  <a id="4890" class="Symbol">=</a>  <a id="4893" class="Number">1</a>
<a id="4895" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4841" class="Function">×-count</a> <a id="4903" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="4905" href="plfa.part1.Connectives.html#4502" class="InductiveConstructor">true</a>  <a id="4911" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="4913" href="plfa.part1.Connectives.html#4565" class="InductiveConstructor">bb</a> <a id="4916" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>  <a id="4919" class="Symbol">=</a>  <a id="4922" class="Number">2</a>
<a id="4924" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4841" class="Function">×-count</a> <a id="4932" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="4934" href="plfa.part1.Connectives.html#4502" class="InductiveConstructor">true</a>  <a id="4940" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="4942" href="plfa.part1.Connectives.html#4576" class="InductiveConstructor">cc</a> <a id="4945" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>  <a id="4948" class="Symbol">=</a>  <a id="4951" class="Number">3</a>
<a id="4953" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4841" class="Function">×-count</a> <a id="4961" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="4963" href="plfa.part1.Connectives.html#4517" class="InductiveConstructor">false</a> <a id="4969" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="4971" href="plfa.part1.Connectives.html#4554" class="InductiveConstructor">aa</a> <a id="4974" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>  <a id="4977" class="Symbol">=</a>  <a id="4980" class="Number">4</a>
<a id="4982" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4841" class="Function">×-count</a> <a id="4990" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="4992" href="plfa.part1.Connectives.html#4517" class="InductiveConstructor">false</a> <a id="4998" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="5000" href="plfa.part1.Connectives.html#4565" class="InductiveConstructor">bb</a> <a id="5003" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>  <a id="5006" class="Symbol">=</a>  <a id="5009" class="Number">5</a>
<a id="5011" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4841" class="Function">×-count</a> <a id="5019" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="5021" href="plfa.part1.Connectives.html#4517" class="InductiveConstructor">false</a> <a id="5027" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="5029" href="plfa.part1.Connectives.html#4576" class="InductiveConstructor">cc</a> <a id="5032" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>  <a id="5035" class="Symbol">=</a>  <a id="5038" class="Number">6</a>
</pre>{% endraw %}
Product on types also shares a property with product on numbers in
that there is a sense in which it is commutative and associative.  In
particular, product is commutative and associative _up to
isomorphism_.

For commutativity, the `to` function swaps a pair, taking `⟨ x , y ⟩` to
`⟨ y , x ⟩`, and the `from` function does the same (up to renaming).
Instantiating the patterns correctly in `from∘to` and `to∘from` is essential.
Replacing the definition of `from∘to` by `λ w → refl` will not work;
and similarly for `to∘from`:
{% raw %}<pre class="Agda"><a id="×-comm"></a><a id="5577" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#5577" class="Function">×-comm</a> <a id="5584" class="Symbol">:</a> <a id="5586" class="Symbol">∀</a> <a id="5588" class="Symbol">{</a><a id="5589" href="plfa.part1.Connectives.html#5589" class="Bound">A</a> <a id="5591" href="plfa.part1.Connectives.html#5591" class="Bound">B</a> <a id="5593" class="Symbol">:</a> <a id="5595" class="PrimitiveType">Set</a><a id="5598" class="Symbol">}</a> <a id="5600" class="Symbol">→</a> <a id="5602" href="plfa.part1.Connectives.html#5589" class="Bound">A</a> <a id="5604" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="5606" href="plfa.part1.Connectives.html#5591" class="Bound">B</a> <a id="5608" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4365" class="Record Operator">≃</a> <a id="5610" href="plfa.part1.Connectives.html#5591" class="Bound">B</a> <a id="5612" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="5614" href="plfa.part1.Connectives.html#5589" class="Bound">A</a>
<a id="5616" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#5577" class="Function">×-comm</a> <a id="5623" class="Symbol">=</a>
  <a id="5627" class="Keyword">record</a>
    <a id="5638" class="Symbol">{</a> <a id="5640" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4405" class="Field">to</a>       <a id="5649" class="Symbol">=</a>  <a id="5652" class="Symbol">λ{</a> <a id="5655" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="5657" href="plfa.part1.Connectives.html#5657" class="Bound">x</a> <a id="5659" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="5661" href="plfa.part1.Connectives.html#5661" class="Bound">y</a> <a id="5663" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="5665" class="Symbol">→</a> <a id="5667" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="5669" href="plfa.part1.Connectives.html#5661" class="Bound">y</a> <a id="5671" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="5673" href="plfa.part1.Connectives.html#5657" class="Bound">x</a> <a id="5675" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="5677" class="Symbol">}</a>
    <a id="5683" class="Symbol">;</a> <a id="5685" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4422" class="Field">from</a>     <a id="5694" class="Symbol">=</a>  <a id="5697" class="Symbol">λ{</a> <a id="5700" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="5702" href="plfa.part1.Connectives.html#5702" class="Bound">y</a> <a id="5704" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="5706" href="plfa.part1.Connectives.html#5706" class="Bound">x</a> <a id="5708" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="5710" class="Symbol">→</a> <a id="5712" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="5714" href="plfa.part1.Connectives.html#5706" class="Bound">x</a> <a id="5716" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="5718" href="plfa.part1.Connectives.html#5702" class="Bound">y</a> <a id="5720" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="5722" class="Symbol">}</a>
    <a id="5728" class="Symbol">;</a> <a id="5730" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4439" class="Field">from∘to</a>  <a id="5739" class="Symbol">=</a>  <a id="5742" class="Symbol">λ{</a> <a id="5745" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="5747" href="plfa.part1.Connectives.html#5747" class="Bound">x</a> <a id="5749" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="5751" href="plfa.part1.Connectives.html#5751" class="Bound">y</a> <a id="5753" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="5755" class="Symbol">→</a> <a id="5757" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="5762" class="Symbol">}</a>
    <a id="5768" class="Symbol">;</a> <a id="5770" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4481" class="Field">to∘from</a>  <a id="5779" class="Symbol">=</a>  <a id="5782" class="Symbol">λ{</a> <a id="5785" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="5787" href="plfa.part1.Connectives.html#5787" class="Bound">y</a> <a id="5789" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="5791" href="plfa.part1.Connectives.html#5791" class="Bound">x</a> <a id="5793" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="5795" class="Symbol">→</a> <a id="5797" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="5802" class="Symbol">}</a>
    <a id="5808" class="Symbol">}</a>
</pre>{% endraw %}
Being _commutative_ is different from being _commutative up to
isomorphism_.  Compare the two statements:

    m * n ≡ n * m
    A × B ≃ B × A

In the first case, we might have that `m` is `2` and `n` is `3`, and
both `m * n` and `n * m` are equal to `6`.  In the second case, we
might have that `A` is `Bool` and `B` is `Tri`, and `Bool × Tri` is
_not_ the same as `Tri × Bool`.  But there is an isomorphism between
the two types.  For instance, `⟨ true , aa ⟩`, which is a member of the
former, corresponds to `⟨ aa , true ⟩`, which is a member of the latter.

For associativity, the `to` function reassociates two uses of pairing,
taking `⟨ ⟨ x , y ⟩ , z ⟩` to `⟨ x , ⟨ y , z ⟩ ⟩`, and the `from` function does
the inverse.  Again, the evidence of left and right inverse requires
matching against a suitable pattern to enable simplification:
{% raw %}<pre class="Agda"><a id="×-assoc"></a><a id="6664" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#6664" class="Function">×-assoc</a> <a id="6672" class="Symbol">:</a> <a id="6674" class="Symbol">∀</a> <a id="6676" class="Symbol">{</a><a id="6677" href="plfa.part1.Connectives.html#6677" class="Bound">A</a> <a id="6679" href="plfa.part1.Connectives.html#6679" class="Bound">B</a> <a id="6681" href="plfa.part1.Connectives.html#6681" class="Bound">C</a> <a id="6683" class="Symbol">:</a> <a id="6685" class="PrimitiveType">Set</a><a id="6688" class="Symbol">}</a> <a id="6690" class="Symbol">→</a> <a id="6692" class="Symbol">(</a><a id="6693" href="plfa.part1.Connectives.html#6677" class="Bound">A</a> <a id="6695" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="6697" href="plfa.part1.Connectives.html#6679" class="Bound">B</a><a id="6698" class="Symbol">)</a> <a id="6700" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="6702" href="plfa.part1.Connectives.html#6681" class="Bound">C</a> <a id="6704" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4365" class="Record Operator">≃</a> <a id="6706" href="plfa.part1.Connectives.html#6677" class="Bound">A</a> <a id="6708" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="6710" class="Symbol">(</a><a id="6711" href="plfa.part1.Connectives.html#6679" class="Bound">B</a> <a id="6713" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="6715" href="plfa.part1.Connectives.html#6681" class="Bound">C</a><a id="6716" class="Symbol">)</a>
<a id="6718" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#6664" class="Function">×-assoc</a> <a id="6726" class="Symbol">=</a>
  <a id="6730" class="Keyword">record</a>
    <a id="6741" class="Symbol">{</a> <a id="6743" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4405" class="Field">to</a>      <a id="6751" class="Symbol">=</a> <a id="6753" class="Symbol">λ{</a> <a id="6756" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="6758" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="6760" href="plfa.part1.Connectives.html#6760" class="Bound">x</a> <a id="6762" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6764" href="plfa.part1.Connectives.html#6764" class="Bound">y</a> <a id="6766" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6768" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6770" href="plfa.part1.Connectives.html#6770" class="Bound">z</a> <a id="6772" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6774" class="Symbol">→</a> <a id="6776" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="6778" href="plfa.part1.Connectives.html#6760" class="Bound">x</a> <a id="6780" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6782" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="6784" href="plfa.part1.Connectives.html#6764" class="Bound">y</a> <a id="6786" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6788" href="plfa.part1.Connectives.html#6770" class="Bound">z</a> <a id="6790" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6792" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6794" class="Symbol">}</a>
    <a id="6800" class="Symbol">;</a> <a id="6802" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4422" class="Field">from</a>    <a id="6810" class="Symbol">=</a> <a id="6812" class="Symbol">λ{</a> <a id="6815" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="6817" href="plfa.part1.Connectives.html#6817" class="Bound">x</a> <a id="6819" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6821" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="6823" href="plfa.part1.Connectives.html#6823" class="Bound">y</a> <a id="6825" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6827" href="plfa.part1.Connectives.html#6827" class="Bound">z</a> <a id="6829" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6831" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6833" class="Symbol">→</a> <a id="6835" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="6837" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="6839" href="plfa.part1.Connectives.html#6817" class="Bound">x</a> <a id="6841" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6843" href="plfa.part1.Connectives.html#6823" class="Bound">y</a> <a id="6845" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6847" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6849" href="plfa.part1.Connectives.html#6827" class="Bound">z</a> <a id="6851" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6853" class="Symbol">}</a>
    <a id="6859" class="Symbol">;</a> <a id="6861" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4439" class="Field">from∘to</a> <a id="6869" class="Symbol">=</a> <a id="6871" class="Symbol">λ{</a> <a id="6874" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="6876" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="6878" href="plfa.part1.Connectives.html#6878" class="Bound">x</a> <a id="6880" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6882" href="plfa.part1.Connectives.html#6882" class="Bound">y</a> <a id="6884" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6886" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6888" href="plfa.part1.Connectives.html#6888" class="Bound">z</a> <a id="6890" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6892" class="Symbol">→</a> <a id="6894" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="6899" class="Symbol">}</a>
    <a id="6905" class="Symbol">;</a> <a id="6907" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4481" class="Field">to∘from</a> <a id="6915" class="Symbol">=</a> <a id="6917" class="Symbol">λ{</a> <a id="6920" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="6922" href="plfa.part1.Connectives.html#6922" class="Bound">x</a> <a id="6924" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6926" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="6928" href="plfa.part1.Connectives.html#6928" class="Bound">y</a> <a id="6930" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="6932" href="plfa.part1.Connectives.html#6932" class="Bound">z</a> <a id="6934" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6936" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="6938" class="Symbol">→</a> <a id="6940" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="6945" class="Symbol">}</a>
    <a id="6951" class="Symbol">}</a>
</pre>{% endraw %}
Being _associative_ is not the same as being _associative
up to isomorphism_.  Compare the two statements:

    (m * n) * p ≡ m * (n * p)
    (A × B) × C ≃ A × (B × C)

For example, the type `(ℕ × Bool) × Tri` is _not_ the same as `ℕ ×
(Bool × Tri)`. But there is an isomorphism between the two types. For
instance `⟨ ⟨ 1 , true ⟩ , aa ⟩`, which is a member of the former,
corresponds to `⟨ 1 , ⟨ true , aa ⟩ ⟩`, which is a member of the latter.

#### Exercise `⇔≃×` (recommended)

Show that `A ⇔ B` as defined [earlier]({{ site.baseurl }}/Isomorphism/#iff)
is isomorphic to `(A → B) × (B → A)`.

{% raw %}<pre class="Agda"><a id="7559" class="Comment">-- Your code goes here</a>
</pre>{% endraw %}

## Truth is unit

Truth `⊤` always holds. We formalise this idea by
declaring a suitable inductive type:
{% raw %}<pre class="Agda"><a id="7697" class="Keyword">data</a> <a id="⊤"></a><a id="7702" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#7702" class="Datatype">⊤</a> <a id="7704" class="Symbol">:</a> <a id="7706" class="PrimitiveType">Set</a> <a id="7710" class="Keyword">where</a>

  <a id="⊤.tt"></a><a id="7719" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#7719" class="InductiveConstructor">tt</a> <a id="7722" class="Symbol">:</a>
    <a id="7728" class="Comment">--</a>
    <a id="7735" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#7702" class="Datatype">⊤</a>
</pre>{% endraw %}Evidence that `⊤` holds is of the form `tt`.

There is an introduction rule, but no elimination rule.
Given evidence that `⊤` holds, there is nothing more of interest we
can conclude.  Since truth always holds, knowing that it holds tells
us nothing new.

The nullary case of `η-×` is `η-⊤`, which asserts that any
value of type `⊤` must be equal to `tt`:
{% raw %}<pre class="Agda"><a id="η-⊤"></a><a id="8101" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#8101" class="Function">η-⊤</a> <a id="8105" class="Symbol">:</a> <a id="8107" class="Symbol">∀</a> <a id="8109" class="Symbol">(</a><a id="8110" href="plfa.part1.Connectives.html#8110" class="Bound">w</a> <a id="8112" class="Symbol">:</a> <a id="8114" href="plfa.part1.Connectives.html#7702" class="Datatype">⊤</a><a id="8115" class="Symbol">)</a> <a id="8117" class="Symbol">→</a> <a id="8119" href="plfa.part1.Connectives.html#7719" class="InductiveConstructor">tt</a> <a id="8122" href="Agda.Builtin.Equality.html#125" class="Datatype Operator">≡</a> <a id="8124" href="plfa.part1.Connectives.html#8110" class="Bound">w</a>
<a id="8126" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#8101" class="Function">η-⊤</a> <a id="8130" href="plfa.part1.Connectives.html#7719" class="InductiveConstructor">tt</a> <a id="8133" class="Symbol">=</a> <a id="8135" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
</pre>{% endraw %}The pattern matching on the left-hand side is essential.  Replacing
`w` by `tt` allows both sides of the propositional equality to
simplify to the same term.

We refer to `⊤` as the _unit_ type. And, indeed,
type `⊤` has exactly one member, `tt`.  For example, the following
function enumerates all possible arguments of type `⊤`:
{% raw %}<pre class="Agda"><a id="⊤-count"></a><a id="8479" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#8479" class="Function">⊤-count</a> <a id="8487" class="Symbol">:</a> <a id="8489" href="plfa.part1.Connectives.html#7702" class="Datatype">⊤</a> <a id="8491" class="Symbol">→</a> <a id="8493" href="Agda.Builtin.Nat.html#165" class="Datatype">ℕ</a>
<a id="8495" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#8479" class="Function">⊤-count</a> <a id="8503" href="plfa.part1.Connectives.html#7719" class="InductiveConstructor">tt</a> <a id="8506" class="Symbol">=</a> <a id="8508" class="Number">1</a>
</pre>{% endraw %}
For numbers, one is the identity of multiplication. Correspondingly,
unit is the identity of product _up to isomorphism_.  For left
identity, the `to` function takes `⟨ tt , x ⟩` to `x`, and the `from`
function does the inverse.  The evidence of left inverse requires
matching against a suitable pattern to enable simplification:
{% raw %}<pre class="Agda"><a id="⊤-identityˡ"></a><a id="8849" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#8849" class="Function">⊤-identityˡ</a> <a id="8861" class="Symbol">:</a> <a id="8863" class="Symbol">∀</a> <a id="8865" class="Symbol">{</a><a id="8866" href="plfa.part1.Connectives.html#8866" class="Bound">A</a> <a id="8868" class="Symbol">:</a> <a id="8870" class="PrimitiveType">Set</a><a id="8873" class="Symbol">}</a> <a id="8875" class="Symbol">→</a> <a id="8877" href="plfa.part1.Connectives.html#7702" class="Datatype">⊤</a> <a id="8879" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="8881" href="plfa.part1.Connectives.html#8866" class="Bound">A</a> <a id="8883" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4365" class="Record Operator">≃</a> <a id="8885" href="plfa.part1.Connectives.html#8866" class="Bound">A</a>
<a id="8887" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#8849" class="Function">⊤-identityˡ</a> <a id="8899" class="Symbol">=</a>
  <a id="8903" class="Keyword">record</a>
    <a id="8914" class="Symbol">{</a> <a id="8916" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4405" class="Field">to</a>      <a id="8924" class="Symbol">=</a> <a id="8926" class="Symbol">λ{</a> <a id="8929" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="8931" href="plfa.part1.Connectives.html#7719" class="InductiveConstructor">tt</a> <a id="8934" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="8936" href="plfa.part1.Connectives.html#8936" class="Bound">x</a> <a id="8938" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="8940" class="Symbol">→</a> <a id="8942" href="plfa.part1.Connectives.html#8936" class="Bound">x</a> <a id="8944" class="Symbol">}</a>
    <a id="8950" class="Symbol">;</a> <a id="8952" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4422" class="Field">from</a>    <a id="8960" class="Symbol">=</a> <a id="8962" class="Symbol">λ{</a> <a id="8965" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#8965" class="Bound">x</a> <a id="8967" class="Symbol">→</a> <a id="8969" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="8971" href="plfa.part1.Connectives.html#7719" class="InductiveConstructor">tt</a> <a id="8974" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="8976" href="plfa.part1.Connectives.html#8965" class="Bound">x</a> <a id="8978" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="8980" class="Symbol">}</a>
    <a id="8986" class="Symbol">;</a> <a id="8988" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4439" class="Field">from∘to</a> <a id="8996" class="Symbol">=</a> <a id="8998" class="Symbol">λ{</a> <a id="9001" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="9003" href="plfa.part1.Connectives.html#7719" class="InductiveConstructor">tt</a> <a id="9006" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="9008" href="plfa.part1.Connectives.html#9008" class="Bound">x</a> <a id="9010" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="9012" class="Symbol">→</a> <a id="9014" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="9019" class="Symbol">}</a>
    <a id="9025" class="Symbol">;</a> <a id="9027" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4481" class="Field">to∘from</a> <a id="9035" class="Symbol">=</a> <a id="9037" class="Symbol">λ{</a> <a id="9040" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#9040" class="Bound">x</a> <a id="9042" class="Symbol">→</a> <a id="9044" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="9049" class="Symbol">}</a>
    <a id="9055" class="Symbol">}</a>
</pre>{% endraw %}
Having an _identity_ is different from having an identity
_up to isomorphism_.  Compare the two statements:

    1 * m ≡ m
    ⊤ × A ≃ A

In the first case, we might have that `m` is `2`, and both
`1 * m` and `m` are equal to `2`.  In the second
case, we might have that `A` is `Bool`, and `⊤ × Bool` is _not_ the
same as `Bool`.  But there is an isomorphism between the two types.
For instance, `⟨ tt , true ⟩`, which is a member of the former,
corresponds to `true`, which is a member of the latter.

Right identity follows from commutativity of product and left identity:
{% raw %}<pre class="Agda"><a id="⊤-identityʳ"></a><a id="9641" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#9641" class="Function">⊤-identityʳ</a> <a id="9653" class="Symbol">:</a> <a id="9655" class="Symbol">∀</a> <a id="9657" class="Symbol">{</a><a id="9658" href="plfa.part1.Connectives.html#9658" class="Bound">A</a> <a id="9660" class="Symbol">:</a> <a id="9662" class="PrimitiveType">Set</a><a id="9665" class="Symbol">}</a> <a id="9667" class="Symbol">→</a> <a id="9669" class="Symbol">(</a><a id="9670" href="plfa.part1.Connectives.html#9658" class="Bound">A</a> <a id="9672" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="9674" href="plfa.part1.Connectives.html#7702" class="Datatype">⊤</a><a id="9675" class="Symbol">)</a> <a id="9677" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4365" class="Record Operator">≃</a> <a id="9679" href="plfa.part1.Connectives.html#9658" class="Bound">A</a>
<a id="9681" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#9641" class="Function">⊤-identityʳ</a> <a id="9693" class="Symbol">{</a><a id="9694" href="plfa.part1.Connectives.html#9694" class="Bound">A</a><a id="9695" class="Symbol">}</a> <a id="9697" class="Symbol">=</a>
  <a id="9701" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#8497" class="Function Operator">≃-begin</a>
    <a id="9713" class="Symbol">(</a><a id="9714" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#9694" class="Bound">A</a> <a id="9716" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="9718" href="plfa.part1.Connectives.html#7702" class="Datatype">⊤</a><a id="9719" class="Symbol">)</a>
  <a id="9723" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#8581" class="Function Operator">≃⟨</a> <a id="9726" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#5577" class="Function">×-comm</a> <a id="9733" href="plfa.part1.Isomorphism.html#8581" class="Function Operator">⟩</a>
    <a id="9739" class="Symbol">(</a><a id="9740" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#7702" class="Datatype">⊤</a> <a id="9742" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="9744" href="plfa.part1.Connectives.html#9694" class="Bound">A</a><a id="9745" class="Symbol">)</a>
  <a id="9749" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#8581" class="Function Operator">≃⟨</a> <a id="9752" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#8849" class="Function">⊤-identityˡ</a> <a id="9764" href="plfa.part1.Isomorphism.html#8581" class="Function Operator">⟩</a>
    <a id="9770" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#9694" class="Bound">A</a>
  <a id="9774" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#8700" class="Function Operator">≃-∎</a>
</pre>{% endraw %}Here we have used a chain of isomorphisms, analogous to that used for
equality.


## Disjunction is sum

Given two propositions `A` and `B`, the disjunction `A ⊎ B` holds
if either `A` holds or `B` holds.  We formalise this idea by
declaring a suitable inductive type:
{% raw %}<pre class="Agda"><a id="10055" class="Keyword">data</a> <a id="_⊎_"></a><a id="10060" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10060" class="Datatype Operator">_⊎_</a> <a id="10064" class="Symbol">(</a><a id="10065" href="plfa.part1.Connectives.html#10065" class="Bound">A</a> <a id="10067" href="plfa.part1.Connectives.html#10067" class="Bound">B</a> <a id="10069" class="Symbol">:</a> <a id="10071" class="PrimitiveType">Set</a><a id="10074" class="Symbol">)</a> <a id="10076" class="Symbol">:</a> <a id="10078" class="PrimitiveType">Set</a> <a id="10082" class="Keyword">where</a>

  <a id="_⊎_.inj₁"></a><a id="10091" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10091" class="InductiveConstructor">inj₁</a> <a id="10096" class="Symbol">:</a>
      <a id="10104" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10065" class="Bound">A</a>
      <a id="10112" class="Comment">-----</a>
    <a id="10122" class="Symbol">→</a> <a id="10124" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10065" class="Bound">A</a> <a id="10126" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="10128" href="plfa.part1.Connectives.html#10067" class="Bound">B</a>

  <a id="_⊎_.inj₂"></a><a id="10133" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10133" class="InductiveConstructor">inj₂</a> <a id="10138" class="Symbol">:</a>
      <a id="10146" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10067" class="Bound">B</a>
      <a id="10154" class="Comment">-----</a>
    <a id="10164" class="Symbol">→</a> <a id="10166" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10065" class="Bound">A</a> <a id="10168" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="10170" href="plfa.part1.Connectives.html#10067" class="Bound">B</a>
</pre>{% endraw %}Evidence that `A ⊎ B` holds is either of the form `inj₁ M`, where `M`
provides evidence that `A` holds, or `inj₂ N`, where `N` provides
evidence that `B` holds.

Given evidence that `A → C` and `B → C` both hold, then given
evidence that `A ⊎ B` holds we can conclude that `C` holds:
{% raw %}<pre class="Agda"><a id="case-⊎"></a><a id="10464" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10464" class="Function">case-⊎</a> <a id="10471" class="Symbol">:</a> <a id="10473" class="Symbol">∀</a> <a id="10475" class="Symbol">{</a><a id="10476" href="plfa.part1.Connectives.html#10476" class="Bound">A</a> <a id="10478" href="plfa.part1.Connectives.html#10478" class="Bound">B</a> <a id="10480" href="plfa.part1.Connectives.html#10480" class="Bound">C</a> <a id="10482" class="Symbol">:</a> <a id="10484" class="PrimitiveType">Set</a><a id="10487" class="Symbol">}</a>
  <a id="10491" class="Symbol">→</a> <a id="10493" class="Symbol">(</a><a id="10494" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10476" class="Bound">A</a> <a id="10496" class="Symbol">→</a> <a id="10498" href="plfa.part1.Connectives.html#10480" class="Bound">C</a><a id="10499" class="Symbol">)</a>
  <a id="10503" class="Symbol">→</a> <a id="10505" class="Symbol">(</a><a id="10506" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10478" class="Bound">B</a> <a id="10508" class="Symbol">→</a> <a id="10510" href="plfa.part1.Connectives.html#10480" class="Bound">C</a><a id="10511" class="Symbol">)</a>
  <a id="10515" class="Symbol">→</a> <a id="10517" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10476" class="Bound">A</a> <a id="10519" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="10521" href="plfa.part1.Connectives.html#10478" class="Bound">B</a>
    <a id="10527" class="Comment">-----------</a>
  <a id="10541" class="Symbol">→</a> <a id="10543" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10480" class="Bound">C</a>
<a id="10545" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10464" class="Function">case-⊎</a> <a id="10552" href="plfa.part1.Connectives.html#10552" class="Bound">f</a> <a id="10554" href="plfa.part1.Connectives.html#10554" class="Bound">g</a> <a id="10556" class="Symbol">(</a><a id="10557" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="10562" href="plfa.part1.Connectives.html#10562" class="Bound">x</a><a id="10563" class="Symbol">)</a> <a id="10565" class="Symbol">=</a> <a id="10567" href="plfa.part1.Connectives.html#10552" class="Bound">f</a> <a id="10569" href="plfa.part1.Connectives.html#10562" class="Bound">x</a>
<a id="10571" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10464" class="Function">case-⊎</a> <a id="10578" href="plfa.part1.Connectives.html#10578" class="Bound">f</a> <a id="10580" href="plfa.part1.Connectives.html#10580" class="Bound">g</a> <a id="10582" class="Symbol">(</a><a id="10583" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="10588" href="plfa.part1.Connectives.html#10588" class="Bound">y</a><a id="10589" class="Symbol">)</a> <a id="10591" class="Symbol">=</a> <a id="10593" href="plfa.part1.Connectives.html#10580" class="Bound">g</a> <a id="10595" href="plfa.part1.Connectives.html#10588" class="Bound">y</a>
</pre>{% endraw %}Pattern matching against `inj₁` and `inj₂` is typical of how we exploit
evidence that a disjunction holds.

When `inj₁` and `inj₂` appear on the right-hand side of an equation we
refer to them as _constructors_, and when they appear on the
left-hand side we refer to them as _destructors_.  We also refer to
`case-⊎` as a destructor, since it plays a similar role.  Other
terminology refers to `inj₁` and `inj₂` as _introducing_ a
disjunction, and to `case-⊎` as _eliminating_ a disjunction; indeed
the former are sometimes given the names `⊎-I₁` and `⊎-I₂` and the
latter the name `⊎-E`.

Applying the destructor to each of the constructors is the identity:
{% raw %}<pre class="Agda"><a id="η-⊎"></a><a id="11264" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#11264" class="Function">η-⊎</a> <a id="11268" class="Symbol">:</a> <a id="11270" class="Symbol">∀</a> <a id="11272" class="Symbol">{</a><a id="11273" href="plfa.part1.Connectives.html#11273" class="Bound">A</a> <a id="11275" href="plfa.part1.Connectives.html#11275" class="Bound">B</a> <a id="11277" class="Symbol">:</a> <a id="11279" class="PrimitiveType">Set</a><a id="11282" class="Symbol">}</a> <a id="11284" class="Symbol">(</a><a id="11285" href="plfa.part1.Connectives.html#11285" class="Bound">w</a> <a id="11287" class="Symbol">:</a> <a id="11289" href="plfa.part1.Connectives.html#11273" class="Bound">A</a> <a id="11291" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="11293" href="plfa.part1.Connectives.html#11275" class="Bound">B</a><a id="11294" class="Symbol">)</a> <a id="11296" class="Symbol">→</a> <a id="11298" href="plfa.part1.Connectives.html#10464" class="Function">case-⊎</a> <a id="11305" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="11310" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="11315" href="plfa.part1.Connectives.html#11285" class="Bound">w</a> <a id="11317" href="Agda.Builtin.Equality.html#125" class="Datatype Operator">≡</a> <a id="11319" href="plfa.part1.Connectives.html#11285" class="Bound">w</a>
<a id="11321" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#11264" class="Function">η-⊎</a> <a id="11325" class="Symbol">(</a><a id="11326" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="11331" href="plfa.part1.Connectives.html#11331" class="Bound">x</a><a id="11332" class="Symbol">)</a> <a id="11334" class="Symbol">=</a> <a id="11336" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
<a id="11341" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#11264" class="Function">η-⊎</a> <a id="11345" class="Symbol">(</a><a id="11346" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="11351" href="plfa.part1.Connectives.html#11351" class="Bound">y</a><a id="11352" class="Symbol">)</a> <a id="11354" class="Symbol">=</a> <a id="11356" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
</pre>{% endraw %}More generally, we can also throw in an arbitrary function from a disjunction:
{% raw %}<pre class="Agda"><a id="uniq-⊎"></a><a id="11448" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#11448" class="Function">uniq-⊎</a> <a id="11455" class="Symbol">:</a> <a id="11457" class="Symbol">∀</a> <a id="11459" class="Symbol">{</a><a id="11460" href="plfa.part1.Connectives.html#11460" class="Bound">A</a> <a id="11462" href="plfa.part1.Connectives.html#11462" class="Bound">B</a> <a id="11464" href="plfa.part1.Connectives.html#11464" class="Bound">C</a> <a id="11466" class="Symbol">:</a> <a id="11468" class="PrimitiveType">Set</a><a id="11471" class="Symbol">}</a> <a id="11473" class="Symbol">(</a><a id="11474" href="plfa.part1.Connectives.html#11474" class="Bound">h</a> <a id="11476" class="Symbol">:</a> <a id="11478" href="plfa.part1.Connectives.html#11460" class="Bound">A</a> <a id="11480" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="11482" href="plfa.part1.Connectives.html#11462" class="Bound">B</a> <a id="11484" class="Symbol">→</a> <a id="11486" href="plfa.part1.Connectives.html#11464" class="Bound">C</a><a id="11487" class="Symbol">)</a> <a id="11489" class="Symbol">(</a><a id="11490" href="plfa.part1.Connectives.html#11490" class="Bound">w</a> <a id="11492" class="Symbol">:</a> <a id="11494" href="plfa.part1.Connectives.html#11460" class="Bound">A</a> <a id="11496" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="11498" href="plfa.part1.Connectives.html#11462" class="Bound">B</a><a id="11499" class="Symbol">)</a> <a id="11501" class="Symbol">→</a>
  <a id="11505" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10464" class="Function">case-⊎</a> <a id="11512" class="Symbol">(</a><a id="11513" href="plfa.part1.Connectives.html#11474" class="Bound">h</a> <a id="11515" href="https://agda.github.io/agda-stdlib/v1.1/Function.html#1099" class="Function Operator">∘</a> <a id="11517" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a><a id="11521" class="Symbol">)</a> <a id="11523" class="Symbol">(</a><a id="11524" href="plfa.part1.Connectives.html#11474" class="Bound">h</a> <a id="11526" href="https://agda.github.io/agda-stdlib/v1.1/Function.html#1099" class="Function Operator">∘</a> <a id="11528" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a><a id="11532" class="Symbol">)</a> <a id="11534" href="plfa.part1.Connectives.html#11490" class="Bound">w</a> <a id="11536" href="Agda.Builtin.Equality.html#125" class="Datatype Operator">≡</a> <a id="11538" href="plfa.part1.Connectives.html#11474" class="Bound">h</a> <a id="11540" href="plfa.part1.Connectives.html#11490" class="Bound">w</a>
<a id="11542" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#11448" class="Function">uniq-⊎</a> <a id="11549" href="plfa.part1.Connectives.html#11549" class="Bound">h</a> <a id="11551" class="Symbol">(</a><a id="11552" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="11557" href="plfa.part1.Connectives.html#11557" class="Bound">x</a><a id="11558" class="Symbol">)</a> <a id="11560" class="Symbol">=</a> <a id="11562" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
<a id="11567" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#11448" class="Function">uniq-⊎</a> <a id="11574" href="plfa.part1.Connectives.html#11574" class="Bound">h</a> <a id="11576" class="Symbol">(</a><a id="11577" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="11582" href="plfa.part1.Connectives.html#11582" class="Bound">y</a><a id="11583" class="Symbol">)</a> <a id="11585" class="Symbol">=</a> <a id="11587" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
</pre>{% endraw %}The pattern matching on the left-hand side is essential.  Replacing
`w` by `inj₁ x` allows both sides of the propositional equality to
simplify to the same term, and similarly for `inj₂ y`.

We set the precedence of disjunction so that it binds less tightly
than any other declared operator:
{% raw %}<pre class="Agda"><a id="11892" class="Keyword">infixr</a> <a id="11899" class="Number">1</a> <a id="11901" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10060" class="Datatype Operator">_⊎_</a>
</pre>{% endraw %}Thus, `A × C ⊎ B × C` parses as `(A × C) ⊎ (B × C)`.

Given two types `A` and `B`, we refer to `A ⊎ B` as the
_sum_ of `A` and `B`.  In set theory, it is also sometimes
called the _disjoint union_, and in computing it corresponds
to a _variant record_ type. Among other reasons for
calling it the sum, note that if type `A` has `m`
distinct members, and type `B` has `n` distinct members,
then the type `A ⊎ B` has `m + n` distinct members.
For instance, consider a type `Bool` with two members, and
a type `Tri` with three members, as defined earlier.
Then the type `Bool ⊎ Tri` has five
members:

    inj₁ true     inj₂ aa
    inj₁ false    inj₂ bb
                  inj₂ cc

For example, the following function enumerates all
possible arguments of type `Bool ⊎ Tri`:
{% raw %}<pre class="Agda"><a id="⊎-count"></a><a id="12683" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#12683" class="Function">⊎-count</a> <a id="12691" class="Symbol">:</a> <a id="12693" href="plfa.part1.Connectives.html#4483" class="Datatype">Bool</a> <a id="12698" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="12700" href="plfa.part1.Connectives.html#4536" class="Datatype">Tri</a> <a id="12704" class="Symbol">→</a> <a id="12706" href="Agda.Builtin.Nat.html#165" class="Datatype">ℕ</a>
<a id="12708" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#12683" class="Function">⊎-count</a> <a id="12716" class="Symbol">(</a><a id="12717" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="12722" href="plfa.part1.Connectives.html#4502" class="InductiveConstructor">true</a><a id="12726" class="Symbol">)</a>   <a id="12730" class="Symbol">=</a>  <a id="12733" class="Number">1</a>
<a id="12735" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#12683" class="Function">⊎-count</a> <a id="12743" class="Symbol">(</a><a id="12744" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="12749" href="plfa.part1.Connectives.html#4517" class="InductiveConstructor">false</a><a id="12754" class="Symbol">)</a>  <a id="12757" class="Symbol">=</a>  <a id="12760" class="Number">2</a>
<a id="12762" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#12683" class="Function">⊎-count</a> <a id="12770" class="Symbol">(</a><a id="12771" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="12776" href="plfa.part1.Connectives.html#4554" class="InductiveConstructor">aa</a><a id="12778" class="Symbol">)</a>     <a id="12784" class="Symbol">=</a>  <a id="12787" class="Number">3</a>
<a id="12789" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#12683" class="Function">⊎-count</a> <a id="12797" class="Symbol">(</a><a id="12798" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="12803" href="plfa.part1.Connectives.html#4565" class="InductiveConstructor">bb</a><a id="12805" class="Symbol">)</a>     <a id="12811" class="Symbol">=</a>  <a id="12814" class="Number">4</a>
<a id="12816" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#12683" class="Function">⊎-count</a> <a id="12824" class="Symbol">(</a><a id="12825" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="12830" href="plfa.part1.Connectives.html#4576" class="InductiveConstructor">cc</a><a id="12832" class="Symbol">)</a>     <a id="12838" class="Symbol">=</a>  <a id="12841" class="Number">5</a>
</pre>{% endraw %}
Sum on types also shares a property with sum on numbers in that it is
commutative and associative _up to isomorphism_.

#### Exercise `⊎-comm` (recommended)

Show sum is commutative up to isomorphism.

{% raw %}<pre class="Agda"><a id="13054" class="Comment">-- Your code goes here</a>
</pre>{% endraw %}
#### Exercise `⊎-assoc` (practice)

Show sum is associative up to isomorphism.

{% raw %}<pre class="Agda"><a id="13166" class="Comment">-- Your code goes here</a>
</pre>{% endraw %}
## False is empty

False `⊥` never holds.  We formalise this idea by declaring
a suitable inductive type:
{% raw %}<pre class="Agda"><a id="13304" class="Keyword">data</a> <a id="⊥"></a><a id="13309" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#13309" class="Datatype">⊥</a> <a id="13311" class="Symbol">:</a> <a id="13313" class="PrimitiveType">Set</a> <a id="13317" class="Keyword">where</a>
  <a id="13325" class="Comment">-- no clauses!</a>
</pre>{% endraw %}There is no possible evidence that `⊥` holds.

Dual to `⊤`, for `⊥` there is no introduction rule but an elimination rule.
Since false never holds, knowing that it holds tells us we are in a
paradoxical situation.  Given evidence that `⊥` holds, we might
conclude anything!  This is a basic principle of logic, known in
medieval times by the Latin phrase _ex falso_, and known to children
through phrases such as "if pigs had wings, then I'd be the Queen of
Sheba".  We formalise it as follows:
{% raw %}<pre class="Agda"><a id="⊥-elim"></a><a id="13843" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#13843" class="Function">⊥-elim</a> <a id="13850" class="Symbol">:</a> <a id="13852" class="Symbol">∀</a> <a id="13854" class="Symbol">{</a><a id="13855" href="plfa.part1.Connectives.html#13855" class="Bound">A</a> <a id="13857" class="Symbol">:</a> <a id="13859" class="PrimitiveType">Set</a><a id="13862" class="Symbol">}</a>
  <a id="13866" class="Symbol">→</a> <a id="13868" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#13309" class="Datatype">⊥</a>
    <a id="13874" class="Comment">--</a>
  <a id="13879" class="Symbol">→</a> <a id="13881" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#13855" class="Bound">A</a>
<a id="13883" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#13843" class="Function">⊥-elim</a> <a id="13890" class="Symbol">()</a>
</pre>{% endraw %}This is our first use of the _absurd pattern_ `()`.
Here since `⊥` is a type with no members, we indicate that it is
_never_ possible to match against a value of this type by using
the pattern `()`.

The nullary case of `case-⊎` is `⊥-elim`.  By analogy,
we might have called it `case-⊥`, but chose to stick with the name
in the standard library.

The nullary case of `uniq-⊎` is `uniq-⊥`, which asserts that `⊥-elim`
is equal to any arbitrary function from `⊥`:
{% raw %}<pre class="Agda"><a id="uniq-⊥"></a><a id="14364" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#14364" class="Function">uniq-⊥</a> <a id="14371" class="Symbol">:</a> <a id="14373" class="Symbol">∀</a> <a id="14375" class="Symbol">{</a><a id="14376" href="plfa.part1.Connectives.html#14376" class="Bound">C</a> <a id="14378" class="Symbol">:</a> <a id="14380" class="PrimitiveType">Set</a><a id="14383" class="Symbol">}</a> <a id="14385" class="Symbol">(</a><a id="14386" href="plfa.part1.Connectives.html#14386" class="Bound">h</a> <a id="14388" class="Symbol">:</a> <a id="14390" href="plfa.part1.Connectives.html#13309" class="Datatype">⊥</a> <a id="14392" class="Symbol">→</a> <a id="14394" href="plfa.part1.Connectives.html#14376" class="Bound">C</a><a id="14395" class="Symbol">)</a> <a id="14397" class="Symbol">(</a><a id="14398" href="plfa.part1.Connectives.html#14398" class="Bound">w</a> <a id="14400" class="Symbol">:</a> <a id="14402" href="plfa.part1.Connectives.html#13309" class="Datatype">⊥</a><a id="14403" class="Symbol">)</a> <a id="14405" class="Symbol">→</a> <a id="14407" href="plfa.part1.Connectives.html#13843" class="Function">⊥-elim</a> <a id="14414" href="plfa.part1.Connectives.html#14398" class="Bound">w</a> <a id="14416" href="Agda.Builtin.Equality.html#125" class="Datatype Operator">≡</a> <a id="14418" href="plfa.part1.Connectives.html#14386" class="Bound">h</a> <a id="14420" href="plfa.part1.Connectives.html#14398" class="Bound">w</a>
<a id="14422" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#14364" class="Function">uniq-⊥</a> <a id="14429" href="plfa.part1.Connectives.html#14429" class="Bound">h</a> <a id="14431" class="Symbol">()</a>
</pre>{% endraw %}Using the absurd pattern asserts there are no possible values for `w`,
so the equation holds trivially.

We refer to `⊥` as the _empty_ type. And, indeed,
type `⊥` has no members. For example, the following function
enumerates all possible arguments of type `⊥`:
{% raw %}<pre class="Agda"><a id="⊥-count"></a><a id="14705" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#14705" class="Function">⊥-count</a> <a id="14713" class="Symbol">:</a> <a id="14715" href="plfa.part1.Connectives.html#13309" class="Datatype">⊥</a> <a id="14717" class="Symbol">→</a> <a id="14719" href="Agda.Builtin.Nat.html#165" class="Datatype">ℕ</a>
<a id="14721" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#14705" class="Function">⊥-count</a> <a id="14729" class="Symbol">()</a>
</pre>{% endraw %}Here again the absurd pattern `()` indicates that no value can match
type `⊥`.

For numbers, zero is the identity of addition. Correspondingly, empty
is the identity of sums _up to isomorphism_.

#### Exercise `⊥-identityˡ` (recommended)

Show empty is the left identity of sums up to isomorphism.

{% raw %}<pre class="Agda"><a id="15039" class="Comment">-- Your code goes here</a>
</pre>{% endraw %}
#### Exercise `⊥-identityʳ` (practice)

Show empty is the right identity of sums up to isomorphism.

{% raw %}<pre class="Agda"><a id="15172" class="Comment">-- Your code goes here</a>
</pre>{% endraw %}
## Implication is function {#implication}

Given two propositions `A` and `B`, the implication `A → B` holds if
whenever `A` holds then `B` must also hold.  We formalise implication using
the function type, which has appeared throughout this book.

Evidence that `A → B` holds is of the form

    λ (x : A) → N

where `N` is a term of type `B` containing as a free variable `x` of type `A`.
Given a term `L` providing evidence that `A → B` holds, and a term `M`
providing evidence that `A` holds, the term `L M` provides evidence that
`B` holds.  In other words, evidence that `A → B` holds is a function that
converts evidence that `A` holds into evidence that `B` holds.

Put another way, if we know that `A → B` and `A` both hold,
then we may conclude that `B` holds:
{% raw %}<pre class="Agda"><a id="→-elim"></a><a id="15975" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#15975" class="Function">→-elim</a> <a id="15982" class="Symbol">:</a> <a id="15984" class="Symbol">∀</a> <a id="15986" class="Symbol">{</a><a id="15987" href="plfa.part1.Connectives.html#15987" class="Bound">A</a> <a id="15989" href="plfa.part1.Connectives.html#15989" class="Bound">B</a> <a id="15991" class="Symbol">:</a> <a id="15993" class="PrimitiveType">Set</a><a id="15996" class="Symbol">}</a>
  <a id="16000" class="Symbol">→</a> <a id="16002" class="Symbol">(</a><a id="16003" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#15987" class="Bound">A</a> <a id="16005" class="Symbol">→</a> <a id="16007" href="plfa.part1.Connectives.html#15989" class="Bound">B</a><a id="16008" class="Symbol">)</a>
  <a id="16012" class="Symbol">→</a> <a id="16014" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#15987" class="Bound">A</a>
    <a id="16020" class="Comment">-------</a>
  <a id="16030" class="Symbol">→</a> <a id="16032" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#15989" class="Bound">B</a>
<a id="16034" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#15975" class="Function">→-elim</a> <a id="16041" href="plfa.part1.Connectives.html#16041" class="Bound">L</a> <a id="16043" href="plfa.part1.Connectives.html#16043" class="Bound">M</a> <a id="16045" class="Symbol">=</a> <a id="16047" href="plfa.part1.Connectives.html#16041" class="Bound">L</a> <a id="16049" href="plfa.part1.Connectives.html#16043" class="Bound">M</a>
</pre>{% endraw %}In medieval times, this rule was known by the name _modus ponens_.
It corresponds to function application.

Defining a function, with a named definition or a lambda abstraction,
is referred to as _introducing_ a function,
while applying a function is referred to as _eliminating_ the function.

Elimination followed by introduction is the identity:
{% raw %}<pre class="Agda"><a id="η-→"></a><a id="16408" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#16408" class="Function">η-→</a> <a id="16412" class="Symbol">:</a> <a id="16414" class="Symbol">∀</a> <a id="16416" class="Symbol">{</a><a id="16417" href="plfa.part1.Connectives.html#16417" class="Bound">A</a> <a id="16419" href="plfa.part1.Connectives.html#16419" class="Bound">B</a> <a id="16421" class="Symbol">:</a> <a id="16423" class="PrimitiveType">Set</a><a id="16426" class="Symbol">}</a> <a id="16428" class="Symbol">(</a><a id="16429" href="plfa.part1.Connectives.html#16429" class="Bound">f</a> <a id="16431" class="Symbol">:</a> <a id="16433" href="plfa.part1.Connectives.html#16417" class="Bound">A</a> <a id="16435" class="Symbol">→</a> <a id="16437" href="plfa.part1.Connectives.html#16419" class="Bound">B</a><a id="16438" class="Symbol">)</a> <a id="16440" class="Symbol">→</a> <a id="16442" class="Symbol">(λ</a> <a id="16445" class="Symbol">(</a><a id="16446" href="plfa.part1.Connectives.html#16446" class="Bound">x</a> <a id="16448" class="Symbol">:</a> <a id="16450" href="plfa.part1.Connectives.html#16417" class="Bound">A</a><a id="16451" class="Symbol">)</a> <a id="16453" class="Symbol">→</a> <a id="16455" href="plfa.part1.Connectives.html#16429" class="Bound">f</a> <a id="16457" href="plfa.part1.Connectives.html#16446" class="Bound">x</a><a id="16458" class="Symbol">)</a> <a id="16460" href="Agda.Builtin.Equality.html#125" class="Datatype Operator">≡</a> <a id="16462" href="plfa.part1.Connectives.html#16429" class="Bound">f</a>
<a id="16464" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#16408" class="Function">η-→</a> <a id="16468" href="plfa.part1.Connectives.html#16468" class="Bound">f</a> <a id="16470" class="Symbol">=</a> <a id="16472" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
</pre>{% endraw %}
Implication binds less tightly than any other operator. Thus, `A ⊎ B →
B ⊎ A` parses as `(A ⊎ B) → (B ⊎ A)`.

Given two types `A` and `B`, we refer to `A → B` as the _function_
space from `A` to `B`.  It is also sometimes called the _exponential_,
with `B` raised to the `A` power.  Among other reasons for calling
it the exponential, note that if type `A` has `m` distinct
members, and type `B` has `n` distinct members, then the type
`A → B` has `nᵐ` distinct members.  For instance, consider a
type `Bool` with two members and a type `Tri` with three members,
as defined earlier. Then the type `Bool → Tri` has nine (that is,
three squared) members:

    λ{true → aa; false → aa}  λ{true → aa; false → bb}  λ{true → aa; false → cc}
    λ{true → bb; false → aa}  λ{true → bb; false → bb}  λ{true → bb; false → cc}
    λ{true → cc; false → aa}  λ{true → cc; false → bb}  λ{true → cc; false → cc}

For example, the following function enumerates all possible
arguments of the type `Bool → Tri`:
{% raw %}<pre class="Agda"><a id="→-count"></a><a id="17480" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#17480" class="Function">→-count</a> <a id="17488" class="Symbol">:</a> <a id="17490" class="Symbol">(</a><a id="17491" href="plfa.part1.Connectives.html#4483" class="Datatype">Bool</a> <a id="17496" class="Symbol">→</a> <a id="17498" href="plfa.part1.Connectives.html#4536" class="Datatype">Tri</a><a id="17501" class="Symbol">)</a> <a id="17503" class="Symbol">→</a> <a id="17505" href="Agda.Builtin.Nat.html#165" class="Datatype">ℕ</a>
<a id="17507" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#17480" class="Function">→-count</a> <a id="17515" href="plfa.part1.Connectives.html#17515" class="Bound">f</a> <a id="17517" class="Keyword">with</a> <a id="17522" href="plfa.part1.Connectives.html#17515" class="Bound">f</a> <a id="17524" href="plfa.part1.Connectives.html#4502" class="InductiveConstructor">true</a> <a id="17529" class="Symbol">|</a> <a id="17531" href="plfa.part1.Connectives.html#17515" class="Bound">f</a> <a id="17533" href="plfa.part1.Connectives.html#4517" class="InductiveConstructor">false</a>
<a id="17539" class="Symbol">...</a>          <a id="17552" class="Symbol">|</a> <a id="17554" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4554" class="InductiveConstructor">aa</a>     <a id="17561" class="Symbol">|</a> <a id="17563" href="plfa.part1.Connectives.html#4554" class="InductiveConstructor">aa</a>      <a id="17571" class="Symbol">=</a>   <a id="17575" class="Number">1</a>
<a id="17577" class="Symbol">...</a>          <a id="17590" class="Symbol">|</a> <a id="17592" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4554" class="InductiveConstructor">aa</a>     <a id="17599" class="Symbol">|</a> <a id="17601" href="plfa.part1.Connectives.html#4565" class="InductiveConstructor">bb</a>      <a id="17609" class="Symbol">=</a>   <a id="17613" class="Number">2</a>
<a id="17615" class="Symbol">...</a>          <a id="17628" class="Symbol">|</a> <a id="17630" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4554" class="InductiveConstructor">aa</a>     <a id="17637" class="Symbol">|</a> <a id="17639" href="plfa.part1.Connectives.html#4576" class="InductiveConstructor">cc</a>      <a id="17647" class="Symbol">=</a>   <a id="17651" class="Number">3</a>
<a id="17653" class="Symbol">...</a>          <a id="17666" class="Symbol">|</a> <a id="17668" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4565" class="InductiveConstructor">bb</a>     <a id="17675" class="Symbol">|</a> <a id="17677" href="plfa.part1.Connectives.html#4554" class="InductiveConstructor">aa</a>      <a id="17685" class="Symbol">=</a>   <a id="17689" class="Number">4</a>
<a id="17691" class="Symbol">...</a>          <a id="17704" class="Symbol">|</a> <a id="17706" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4565" class="InductiveConstructor">bb</a>     <a id="17713" class="Symbol">|</a> <a id="17715" href="plfa.part1.Connectives.html#4565" class="InductiveConstructor">bb</a>      <a id="17723" class="Symbol">=</a>   <a id="17727" class="Number">5</a>
<a id="17729" class="Symbol">...</a>          <a id="17742" class="Symbol">|</a> <a id="17744" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4565" class="InductiveConstructor">bb</a>     <a id="17751" class="Symbol">|</a> <a id="17753" href="plfa.part1.Connectives.html#4576" class="InductiveConstructor">cc</a>      <a id="17761" class="Symbol">=</a>   <a id="17765" class="Number">6</a>
<a id="17767" class="Symbol">...</a>          <a id="17780" class="Symbol">|</a> <a id="17782" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4576" class="InductiveConstructor">cc</a>     <a id="17789" class="Symbol">|</a> <a id="17791" href="plfa.part1.Connectives.html#4554" class="InductiveConstructor">aa</a>      <a id="17799" class="Symbol">=</a>   <a id="17803" class="Number">7</a>
<a id="17805" class="Symbol">...</a>          <a id="17818" class="Symbol">|</a> <a id="17820" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4576" class="InductiveConstructor">cc</a>     <a id="17827" class="Symbol">|</a> <a id="17829" href="plfa.part1.Connectives.html#4565" class="InductiveConstructor">bb</a>      <a id="17837" class="Symbol">=</a>   <a id="17841" class="Number">8</a>
<a id="17843" class="Symbol">...</a>          <a id="17856" class="Symbol">|</a> <a id="17858" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#4576" class="InductiveConstructor">cc</a>     <a id="17865" class="Symbol">|</a> <a id="17867" href="plfa.part1.Connectives.html#4576" class="InductiveConstructor">cc</a>      <a id="17875" class="Symbol">=</a>   <a id="17879" class="Number">9</a>
</pre>{% endraw %}
Exponential on types also share a property with exponential on
numbers in that many of the standard identities for numbers carry
over to the types.

Corresponding to the law

    (p ^ n) ^ m  ≡  p ^ (n * m)

we have the isomorphism

    A → (B → C)  ≃  (A × B) → C

Both types can be viewed as functions that given evidence that `A` holds
and evidence that `B` holds can return evidence that `C` holds.
This isomorphism sometimes goes by the name *currying*.
The proof of the right inverse requires extensionality:
{% raw %}<pre class="Agda"><a id="currying"></a><a id="18405" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#18405" class="Function">currying</a> <a id="18414" class="Symbol">:</a> <a id="18416" class="Symbol">∀</a> <a id="18418" class="Symbol">{</a><a id="18419" href="plfa.part1.Connectives.html#18419" class="Bound">A</a> <a id="18421" href="plfa.part1.Connectives.html#18421" class="Bound">B</a> <a id="18423" href="plfa.part1.Connectives.html#18423" class="Bound">C</a> <a id="18425" class="Symbol">:</a> <a id="18427" class="PrimitiveType">Set</a><a id="18430" class="Symbol">}</a> <a id="18432" class="Symbol">→</a> <a id="18434" class="Symbol">(</a><a id="18435" href="plfa.part1.Connectives.html#18419" class="Bound">A</a> <a id="18437" class="Symbol">→</a> <a id="18439" href="plfa.part1.Connectives.html#18421" class="Bound">B</a> <a id="18441" class="Symbol">→</a> <a id="18443" href="plfa.part1.Connectives.html#18423" class="Bound">C</a><a id="18444" class="Symbol">)</a> <a id="18446" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4365" class="Record Operator">≃</a> <a id="18448" class="Symbol">(</a><a id="18449" href="plfa.part1.Connectives.html#18419" class="Bound">A</a> <a id="18451" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="18453" href="plfa.part1.Connectives.html#18421" class="Bound">B</a> <a id="18455" class="Symbol">→</a> <a id="18457" href="plfa.part1.Connectives.html#18423" class="Bound">C</a><a id="18458" class="Symbol">)</a>
<a id="18460" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#18405" class="Function">currying</a> <a id="18469" class="Symbol">=</a>
  <a id="18473" class="Keyword">record</a>
    <a id="18484" class="Symbol">{</a> <a id="18486" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4405" class="Field">to</a>      <a id="18494" class="Symbol">=</a>  <a id="18497" class="Symbol">λ{</a> <a id="18500" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#18500" class="Bound">f</a> <a id="18502" class="Symbol">→</a> <a id="18504" class="Symbol">λ{</a> <a id="18507" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="18509" href="plfa.part1.Connectives.html#18509" class="Bound">x</a> <a id="18511" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="18513" href="plfa.part1.Connectives.html#18513" class="Bound">y</a> <a id="18515" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="18517" class="Symbol">→</a> <a id="18519" href="plfa.part1.Connectives.html#18500" class="Bound">f</a> <a id="18521" href="plfa.part1.Connectives.html#18509" class="Bound">x</a> <a id="18523" href="plfa.part1.Connectives.html#18513" class="Bound">y</a> <a id="18525" class="Symbol">}}</a>
    <a id="18532" class="Symbol">;</a> <a id="18534" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4422" class="Field">from</a>    <a id="18542" class="Symbol">=</a>  <a id="18545" class="Symbol">λ{</a> <a id="18548" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#18548" class="Bound">g</a> <a id="18550" class="Symbol">→</a> <a id="18552" class="Symbol">λ{</a> <a id="18555" href="plfa.part1.Connectives.html#18555" class="Bound">x</a> <a id="18557" class="Symbol">→</a> <a id="18559" class="Symbol">λ{</a> <a id="18562" href="plfa.part1.Connectives.html#18562" class="Bound">y</a> <a id="18564" class="Symbol">→</a> <a id="18566" href="plfa.part1.Connectives.html#18548" class="Bound">g</a> <a id="18568" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="18570" href="plfa.part1.Connectives.html#18555" class="Bound">x</a> <a id="18572" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="18574" href="plfa.part1.Connectives.html#18562" class="Bound">y</a> <a id="18576" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="18578" class="Symbol">}}}</a>
    <a id="18586" class="Symbol">;</a> <a id="18588" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4439" class="Field">from∘to</a> <a id="18596" class="Symbol">=</a>  <a id="18599" class="Symbol">λ{</a> <a id="18602" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#18602" class="Bound">f</a> <a id="18604" class="Symbol">→</a> <a id="18606" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="18611" class="Symbol">}</a>
    <a id="18617" class="Symbol">;</a> <a id="18619" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4481" class="Field">to∘from</a> <a id="18627" class="Symbol">=</a>  <a id="18630" class="Symbol">λ{</a> <a id="18633" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#18633" class="Bound">g</a> <a id="18635" class="Symbol">→</a> <a id="18637" href="plfa.part1.Isomorphism.html#2684" class="Postulate">extensionality</a> <a id="18652" class="Symbol">λ{</a> <a id="18655" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="18657" href="plfa.part1.Connectives.html#18657" class="Bound">x</a> <a id="18659" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="18661" href="plfa.part1.Connectives.html#18661" class="Bound">y</a> <a id="18663" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="18665" class="Symbol">→</a> <a id="18667" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="18672" class="Symbol">}}</a>
    <a id="18679" class="Symbol">}</a>
</pre>{% endraw %}
Currying tells us that instead of a function that takes a pair of arguments,
we can have a function that takes the first argument and returns a function that
expects the second argument.  Thus, for instance, our way of writing addition

    _+_ : ℕ → ℕ → ℕ

is isomorphic to a function that accepts a pair of arguments:

    _+′_ : (ℕ × ℕ) → ℕ

Agda is optimised for currying, so `2 + 3` abbreviates `_+_ 2 3`.
In a language optimised for pairing, we would instead take `2 +′ 3` as
an abbreviation for `_+′_ ⟨ 2 , 3 ⟩`.

Corresponding to the law

    p ^ (n + m) = (p ^ n) * (p ^ m)

we have the isomorphism:

    (A ⊎ B) → C  ≃  (A → C) × (B → C)

That is, the assertion that if either `A` holds or `B` holds then `C` holds
is the same as the assertion that if `A` holds then `C` holds and if
`B` holds then `C` holds.  The proof of the left inverse requires extensionality:
{% raw %}<pre class="Agda"><a id="→-distrib-⊎"></a><a id="19566" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#19566" class="Function">→-distrib-⊎</a> <a id="19578" class="Symbol">:</a> <a id="19580" class="Symbol">∀</a> <a id="19582" class="Symbol">{</a><a id="19583" href="plfa.part1.Connectives.html#19583" class="Bound">A</a> <a id="19585" href="plfa.part1.Connectives.html#19585" class="Bound">B</a> <a id="19587" href="plfa.part1.Connectives.html#19587" class="Bound">C</a> <a id="19589" class="Symbol">:</a> <a id="19591" class="PrimitiveType">Set</a><a id="19594" class="Symbol">}</a> <a id="19596" class="Symbol">→</a> <a id="19598" class="Symbol">(</a><a id="19599" href="plfa.part1.Connectives.html#19583" class="Bound">A</a> <a id="19601" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="19603" href="plfa.part1.Connectives.html#19585" class="Bound">B</a> <a id="19605" class="Symbol">→</a> <a id="19607" href="plfa.part1.Connectives.html#19587" class="Bound">C</a><a id="19608" class="Symbol">)</a> <a id="19610" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4365" class="Record Operator">≃</a> <a id="19612" class="Symbol">((</a><a id="19614" href="plfa.part1.Connectives.html#19583" class="Bound">A</a> <a id="19616" class="Symbol">→</a> <a id="19618" href="plfa.part1.Connectives.html#19587" class="Bound">C</a><a id="19619" class="Symbol">)</a> <a id="19621" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="19623" class="Symbol">(</a><a id="19624" href="plfa.part1.Connectives.html#19585" class="Bound">B</a> <a id="19626" class="Symbol">→</a> <a id="19628" href="plfa.part1.Connectives.html#19587" class="Bound">C</a><a id="19629" class="Symbol">))</a>
<a id="19632" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#19566" class="Function">→-distrib-⊎</a> <a id="19644" class="Symbol">=</a>
  <a id="19648" class="Keyword">record</a>
    <a id="19659" class="Symbol">{</a> <a id="19661" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4405" class="Field">to</a>      <a id="19669" class="Symbol">=</a> <a id="19671" class="Symbol">λ{</a> <a id="19674" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#19674" class="Bound">f</a> <a id="19676" class="Symbol">→</a> <a id="19678" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="19680" href="plfa.part1.Connectives.html#19674" class="Bound">f</a> <a id="19682" href="https://agda.github.io/agda-stdlib/v1.1/Function.html#1099" class="Function Operator">∘</a> <a id="19684" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="19689" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="19691" href="plfa.part1.Connectives.html#19674" class="Bound">f</a> <a id="19693" href="https://agda.github.io/agda-stdlib/v1.1/Function.html#1099" class="Function Operator">∘</a> <a id="19695" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="19700" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="19702" class="Symbol">}</a>
    <a id="19708" class="Symbol">;</a> <a id="19710" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4422" class="Field">from</a>    <a id="19718" class="Symbol">=</a> <a id="19720" class="Symbol">λ{</a> <a id="19723" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="19725" href="plfa.part1.Connectives.html#19725" class="Bound">g</a> <a id="19727" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="19729" href="plfa.part1.Connectives.html#19729" class="Bound">h</a> <a id="19731" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="19733" class="Symbol">→</a> <a id="19735" class="Symbol">λ{</a> <a id="19738" class="Symbol">(</a><a id="19739" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="19744" href="plfa.part1.Connectives.html#19744" class="Bound">x</a><a id="19745" class="Symbol">)</a> <a id="19747" class="Symbol">→</a> <a id="19749" href="plfa.part1.Connectives.html#19725" class="Bound">g</a> <a id="19751" href="plfa.part1.Connectives.html#19744" class="Bound">x</a> <a id="19753" class="Symbol">;</a> <a id="19755" class="Symbol">(</a><a id="19756" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="19761" href="plfa.part1.Connectives.html#19761" class="Bound">y</a><a id="19762" class="Symbol">)</a> <a id="19764" class="Symbol">→</a> <a id="19766" href="plfa.part1.Connectives.html#19729" class="Bound">h</a> <a id="19768" href="plfa.part1.Connectives.html#19761" class="Bound">y</a> <a id="19770" class="Symbol">}</a> <a id="19772" class="Symbol">}</a>
    <a id="19778" class="Symbol">;</a> <a id="19780" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4439" class="Field">from∘to</a> <a id="19788" class="Symbol">=</a> <a id="19790" class="Symbol">λ{</a> <a id="19793" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#19793" class="Bound">f</a> <a id="19795" class="Symbol">→</a> <a id="19797" href="plfa.part1.Isomorphism.html#2684" class="Postulate">extensionality</a> <a id="19812" class="Symbol">λ{</a> <a id="19815" class="Symbol">(</a><a id="19816" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="19821" href="plfa.part1.Connectives.html#19821" class="Bound">x</a><a id="19822" class="Symbol">)</a> <a id="19824" class="Symbol">→</a> <a id="19826" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="19831" class="Symbol">;</a> <a id="19833" class="Symbol">(</a><a id="19834" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="19839" href="plfa.part1.Connectives.html#19839" class="Bound">y</a><a id="19840" class="Symbol">)</a> <a id="19842" class="Symbol">→</a> <a id="19844" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="19849" class="Symbol">}</a> <a id="19851" class="Symbol">}</a>
    <a id="19857" class="Symbol">;</a> <a id="19859" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4481" class="Field">to∘from</a> <a id="19867" class="Symbol">=</a> <a id="19869" class="Symbol">λ{</a> <a id="19872" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="19874" href="plfa.part1.Connectives.html#19874" class="Bound">g</a> <a id="19876" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="19878" href="plfa.part1.Connectives.html#19878" class="Bound">h</a> <a id="19880" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="19882" class="Symbol">→</a> <a id="19884" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="19889" class="Symbol">}</a>
    <a id="19895" class="Symbol">}</a>
</pre>{% endraw %}
Corresponding to the law

    (p * n) ^ m = (p ^ m) * (n ^ m)

we have the isomorphism:

    A → B × C  ≃  (A → B) × (A → C)

That is, the assertion that if `A` holds then `B` holds and `C` holds
is the same as the assertion that if `A` holds then `B` holds and if
`A` holds then `C` holds.  The proof of left inverse requires both extensionality
and the rule `η-×` for products:
{% raw %}<pre class="Agda"><a id="→-distrib-×"></a><a id="20286" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#20286" class="Function">→-distrib-×</a> <a id="20298" class="Symbol">:</a> <a id="20300" class="Symbol">∀</a> <a id="20302" class="Symbol">{</a><a id="20303" href="plfa.part1.Connectives.html#20303" class="Bound">A</a> <a id="20305" href="plfa.part1.Connectives.html#20305" class="Bound">B</a> <a id="20307" href="plfa.part1.Connectives.html#20307" class="Bound">C</a> <a id="20309" class="Symbol">:</a> <a id="20311" class="PrimitiveType">Set</a><a id="20314" class="Symbol">}</a> <a id="20316" class="Symbol">→</a> <a id="20318" class="Symbol">(</a><a id="20319" href="plfa.part1.Connectives.html#20303" class="Bound">A</a> <a id="20321" class="Symbol">→</a> <a id="20323" href="plfa.part1.Connectives.html#20305" class="Bound">B</a> <a id="20325" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="20327" href="plfa.part1.Connectives.html#20307" class="Bound">C</a><a id="20328" class="Symbol">)</a> <a id="20330" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4365" class="Record Operator">≃</a> <a id="20332" class="Symbol">(</a><a id="20333" href="plfa.part1.Connectives.html#20303" class="Bound">A</a> <a id="20335" class="Symbol">→</a> <a id="20337" href="plfa.part1.Connectives.html#20305" class="Bound">B</a><a id="20338" class="Symbol">)</a> <a id="20340" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="20342" class="Symbol">(</a><a id="20343" href="plfa.part1.Connectives.html#20303" class="Bound">A</a> <a id="20345" class="Symbol">→</a> <a id="20347" href="plfa.part1.Connectives.html#20307" class="Bound">C</a><a id="20348" class="Symbol">)</a>
<a id="20350" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#20286" class="Function">→-distrib-×</a> <a id="20362" class="Symbol">=</a>
  <a id="20366" class="Keyword">record</a>
    <a id="20377" class="Symbol">{</a> <a id="20379" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4405" class="Field">to</a>      <a id="20387" class="Symbol">=</a> <a id="20389" class="Symbol">λ{</a> <a id="20392" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#20392" class="Bound">f</a> <a id="20394" class="Symbol">→</a> <a id="20396" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="20398" href="plfa.part1.Connectives.html#1611" class="Function">proj₁</a> <a id="20404" href="https://agda.github.io/agda-stdlib/v1.1/Function.html#1099" class="Function Operator">∘</a> <a id="20406" href="plfa.part1.Connectives.html#20392" class="Bound">f</a> <a id="20408" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20410" href="plfa.part1.Connectives.html#1680" class="Function">proj₂</a> <a id="20416" href="https://agda.github.io/agda-stdlib/v1.1/Function.html#1099" class="Function Operator">∘</a> <a id="20418" href="plfa.part1.Connectives.html#20392" class="Bound">f</a> <a id="20420" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="20422" class="Symbol">}</a>
    <a id="20428" class="Symbol">;</a> <a id="20430" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4422" class="Field">from</a>    <a id="20438" class="Symbol">=</a> <a id="20440" class="Symbol">λ{</a> <a id="20443" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="20445" href="plfa.part1.Connectives.html#20445" class="Bound">g</a> <a id="20447" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20449" href="plfa.part1.Connectives.html#20449" class="Bound">h</a> <a id="20451" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="20453" class="Symbol">→</a> <a id="20455" class="Symbol">λ</a> <a id="20457" href="plfa.part1.Connectives.html#20457" class="Bound">x</a> <a id="20459" class="Symbol">→</a> <a id="20461" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="20463" href="plfa.part1.Connectives.html#20445" class="Bound">g</a> <a id="20465" href="plfa.part1.Connectives.html#20457" class="Bound">x</a> <a id="20467" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20469" href="plfa.part1.Connectives.html#20449" class="Bound">h</a> <a id="20471" href="plfa.part1.Connectives.html#20457" class="Bound">x</a> <a id="20473" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="20475" class="Symbol">}</a>
    <a id="20481" class="Symbol">;</a> <a id="20483" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4439" class="Field">from∘to</a> <a id="20491" class="Symbol">=</a> <a id="20493" class="Symbol">λ{</a> <a id="20496" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#20496" class="Bound">f</a> <a id="20498" class="Symbol">→</a> <a id="20500" href="plfa.part1.Isomorphism.html#2684" class="Postulate">extensionality</a> <a id="20515" class="Symbol">λ{</a> <a id="20518" href="plfa.part1.Connectives.html#20518" class="Bound">x</a> <a id="20520" class="Symbol">→</a> <a id="20522" href="plfa.part1.Connectives.html#3562" class="Function">η-×</a> <a id="20526" class="Symbol">(</a><a id="20527" href="plfa.part1.Connectives.html#20496" class="Bound">f</a> <a id="20529" href="plfa.part1.Connectives.html#20518" class="Bound">x</a><a id="20530" class="Symbol">)</a> <a id="20532" class="Symbol">}</a> <a id="20534" class="Symbol">}</a>
    <a id="20540" class="Symbol">;</a> <a id="20542" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4481" class="Field">to∘from</a> <a id="20550" class="Symbol">=</a> <a id="20552" class="Symbol">λ{</a> <a id="20555" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="20557" href="plfa.part1.Connectives.html#20557" class="Bound">g</a> <a id="20559" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20561" href="plfa.part1.Connectives.html#20561" class="Bound">h</a> <a id="20563" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="20565" class="Symbol">→</a> <a id="20567" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a> <a id="20572" class="Symbol">}</a>
    <a id="20578" class="Symbol">}</a>
</pre>{% endraw %}

## Distribution

Products distribute over sum, up to isomorphism.  The code to validate
this fact is similar in structure to our previous results:
{% raw %}<pre class="Agda"><a id="×-distrib-⊎"></a><a id="20737" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#20737" class="Function">×-distrib-⊎</a> <a id="20749" class="Symbol">:</a> <a id="20751" class="Symbol">∀</a> <a id="20753" class="Symbol">{</a><a id="20754" href="plfa.part1.Connectives.html#20754" class="Bound">A</a> <a id="20756" href="plfa.part1.Connectives.html#20756" class="Bound">B</a> <a id="20758" href="plfa.part1.Connectives.html#20758" class="Bound">C</a> <a id="20760" class="Symbol">:</a> <a id="20762" class="PrimitiveType">Set</a><a id="20765" class="Symbol">}</a> <a id="20767" class="Symbol">→</a> <a id="20769" class="Symbol">(</a><a id="20770" href="plfa.part1.Connectives.html#20754" class="Bound">A</a> <a id="20772" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="20774" href="plfa.part1.Connectives.html#20756" class="Bound">B</a><a id="20775" class="Symbol">)</a> <a id="20777" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="20779" href="plfa.part1.Connectives.html#20758" class="Bound">C</a> <a id="20781" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4365" class="Record Operator">≃</a> <a id="20783" class="Symbol">(</a><a id="20784" href="plfa.part1.Connectives.html#20754" class="Bound">A</a> <a id="20786" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="20788" href="plfa.part1.Connectives.html#20758" class="Bound">C</a><a id="20789" class="Symbol">)</a> <a id="20791" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="20793" class="Symbol">(</a><a id="20794" href="plfa.part1.Connectives.html#20756" class="Bound">B</a> <a id="20796" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="20798" href="plfa.part1.Connectives.html#20758" class="Bound">C</a><a id="20799" class="Symbol">)</a>
<a id="20801" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#20737" class="Function">×-distrib-⊎</a> <a id="20813" class="Symbol">=</a>
  <a id="20817" class="Keyword">record</a>
    <a id="20828" class="Symbol">{</a> <a id="20830" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4405" class="Field">to</a>      <a id="20838" class="Symbol">=</a> <a id="20840" class="Symbol">λ{</a> <a id="20843" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="20845" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="20850" href="plfa.part1.Connectives.html#20850" class="Bound">x</a> <a id="20852" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20854" href="plfa.part1.Connectives.html#20854" class="Bound">z</a> <a id="20856" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="20858" class="Symbol">→</a> <a id="20860" class="Symbol">(</a><a id="20861" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="20866" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="20868" href="plfa.part1.Connectives.html#20850" class="Bound">x</a> <a id="20870" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20872" href="plfa.part1.Connectives.html#20854" class="Bound">z</a> <a id="20874" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="20875" class="Symbol">)</a>
                 <a id="20894" class="Symbol">;</a> <a id="20896" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="20898" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="20903" href="plfa.part1.Connectives.html#20903" class="Bound">y</a> <a id="20905" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20907" href="plfa.part1.Connectives.html#20907" class="Bound">z</a> <a id="20909" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="20911" class="Symbol">→</a> <a id="20913" class="Symbol">(</a><a id="20914" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="20919" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="20921" href="plfa.part1.Connectives.html#20903" class="Bound">y</a> <a id="20923" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20925" href="plfa.part1.Connectives.html#20907" class="Bound">z</a> <a id="20927" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="20928" class="Symbol">)</a>
                 <a id="20947" class="Symbol">}</a>
    <a id="20953" class="Symbol">;</a> <a id="20955" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4422" class="Field">from</a>    <a id="20963" class="Symbol">=</a> <a id="20965" class="Symbol">λ{</a> <a id="20968" class="Symbol">(</a><a id="20969" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10091" class="InductiveConstructor">inj₁</a> <a id="20974" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="20976" href="plfa.part1.Connectives.html#20976" class="Bound">x</a> <a id="20978" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20980" href="plfa.part1.Connectives.html#20980" class="Bound">z</a> <a id="20982" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="20983" class="Symbol">)</a> <a id="20985" class="Symbol">→</a> <a id="20987" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="20989" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="20994" href="plfa.part1.Connectives.html#20976" class="Bound">x</a> <a id="20996" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="20998" href="plfa.part1.Connectives.html#20980" class="Bound">z</a> <a id="21000" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>
                 <a id="21019" class="Symbol">;</a> <a id="21021" class="Symbol">(</a><a id="21022" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10133" class="InductiveConstructor">inj₂</a> <a id="21027" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21029" href="plfa.part1.Connectives.html#21029" class="Bound">y</a> <a id="21031" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21033" href="plfa.part1.Connectives.html#21033" class="Bound">z</a> <a id="21035" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="21036" class="Symbol">)</a> <a id="21038" class="Symbol">→</a> <a id="21040" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21042" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="21047" href="plfa.part1.Connectives.html#21029" class="Bound">y</a> <a id="21049" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21051" href="plfa.part1.Connectives.html#21033" class="Bound">z</a> <a id="21053" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>
                 <a id="21072" class="Symbol">}</a>
    <a id="21078" class="Symbol">;</a> <a id="21080" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4439" class="Field">from∘to</a> <a id="21088" class="Symbol">=</a> <a id="21090" class="Symbol">λ{</a> <a id="21093" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="21095" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="21100" href="plfa.part1.Connectives.html#21100" class="Bound">x</a> <a id="21102" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21104" href="plfa.part1.Connectives.html#21104" class="Bound">z</a> <a id="21106" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="21108" class="Symbol">→</a> <a id="21110" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
                 <a id="21132" class="Symbol">;</a> <a id="21134" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="21136" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="21141" href="plfa.part1.Connectives.html#21141" class="Bound">y</a> <a id="21143" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21145" href="plfa.part1.Connectives.html#21145" class="Bound">z</a> <a id="21147" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="21149" class="Symbol">→</a> <a id="21151" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
                 <a id="21173" class="Symbol">}</a>
    <a id="21179" class="Symbol">;</a> <a id="21181" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#4481" class="Field">to∘from</a> <a id="21189" class="Symbol">=</a> <a id="21191" class="Symbol">λ{</a> <a id="21194" class="Symbol">(</a><a id="21195" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10091" class="InductiveConstructor">inj₁</a> <a id="21200" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21202" href="plfa.part1.Connectives.html#21202" class="Bound">x</a> <a id="21204" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21206" href="plfa.part1.Connectives.html#21206" class="Bound">z</a> <a id="21208" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="21209" class="Symbol">)</a> <a id="21211" class="Symbol">→</a> <a id="21213" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
                 <a id="21235" class="Symbol">;</a> <a id="21237" class="Symbol">(</a><a id="21238" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10133" class="InductiveConstructor">inj₂</a> <a id="21243" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21245" href="plfa.part1.Connectives.html#21245" class="Bound">y</a> <a id="21247" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21249" href="plfa.part1.Connectives.html#21249" class="Bound">z</a> <a id="21251" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="21252" class="Symbol">)</a> <a id="21254" class="Symbol">→</a> <a id="21256" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
                 <a id="21278" class="Symbol">}</a>
    <a id="21284" class="Symbol">}</a>
</pre>{% endraw %}
Sums do not distribute over products up to isomorphism, but it is an embedding:
{% raw %}<pre class="Agda"><a id="⊎-distrib-×"></a><a id="21375" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#21375" class="Function">⊎-distrib-×</a> <a id="21387" class="Symbol">:</a> <a id="21389" class="Symbol">∀</a> <a id="21391" class="Symbol">{</a><a id="21392" href="plfa.part1.Connectives.html#21392" class="Bound">A</a> <a id="21394" href="plfa.part1.Connectives.html#21394" class="Bound">B</a> <a id="21396" href="plfa.part1.Connectives.html#21396" class="Bound">C</a> <a id="21398" class="Symbol">:</a> <a id="21400" class="PrimitiveType">Set</a><a id="21403" class="Symbol">}</a> <a id="21405" class="Symbol">→</a> <a id="21407" class="Symbol">(</a><a id="21408" href="plfa.part1.Connectives.html#21392" class="Bound">A</a> <a id="21410" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="21412" href="plfa.part1.Connectives.html#21394" class="Bound">B</a><a id="21413" class="Symbol">)</a> <a id="21415" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="21417" href="plfa.part1.Connectives.html#21396" class="Bound">C</a> <a id="21419" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#9186" class="Record Operator">≲</a> <a id="21421" class="Symbol">(</a><a id="21422" href="plfa.part1.Connectives.html#21392" class="Bound">A</a> <a id="21424" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="21426" href="plfa.part1.Connectives.html#21396" class="Bound">C</a><a id="21427" class="Symbol">)</a> <a id="21429" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="21431" class="Symbol">(</a><a id="21432" href="plfa.part1.Connectives.html#21394" class="Bound">B</a> <a id="21434" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="21436" href="plfa.part1.Connectives.html#21396" class="Bound">C</a><a id="21437" class="Symbol">)</a>
<a id="21439" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#21375" class="Function">⊎-distrib-×</a> <a id="21451" class="Symbol">=</a>
  <a id="21455" class="Keyword">record</a>
    <a id="21466" class="Symbol">{</a> <a id="21468" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#9226" class="Field">to</a>      <a id="21476" class="Symbol">=</a> <a id="21478" class="Symbol">λ{</a> <a id="21481" class="Symbol">(</a><a id="21482" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10091" class="InductiveConstructor">inj₁</a> <a id="21487" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21489" href="plfa.part1.Connectives.html#21489" class="Bound">x</a> <a id="21491" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21493" href="plfa.part1.Connectives.html#21493" class="Bound">y</a> <a id="21495" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="21496" class="Symbol">)</a> <a id="21498" class="Symbol">→</a> <a id="21500" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21502" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="21507" href="plfa.part1.Connectives.html#21489" class="Bound">x</a> <a id="21509" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21511" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="21516" href="plfa.part1.Connectives.html#21493" class="Bound">y</a> <a id="21518" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>
                 <a id="21537" class="Symbol">;</a> <a id="21539" class="Symbol">(</a><a id="21540" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10133" class="InductiveConstructor">inj₂</a> <a id="21545" href="plfa.part1.Connectives.html#21545" class="Bound">z</a><a id="21546" class="Symbol">)</a>         <a id="21556" class="Symbol">→</a> <a id="21558" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21560" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="21565" href="plfa.part1.Connectives.html#21545" class="Bound">z</a> <a id="21567" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21569" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="21574" href="plfa.part1.Connectives.html#21545" class="Bound">z</a> <a id="21576" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a>
                 <a id="21595" class="Symbol">}</a>
    <a id="21601" class="Symbol">;</a> <a id="21603" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#9246" class="Field">from</a>    <a id="21611" class="Symbol">=</a> <a id="21613" class="Symbol">λ{</a> <a id="21616" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="21618" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="21623" href="plfa.part1.Connectives.html#21623" class="Bound">x</a> <a id="21625" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21627" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="21632" href="plfa.part1.Connectives.html#21632" class="Bound">y</a> <a id="21634" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="21636" class="Symbol">→</a> <a id="21638" class="Symbol">(</a><a id="21639" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="21644" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21646" href="plfa.part1.Connectives.html#21623" class="Bound">x</a> <a id="21648" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21650" href="plfa.part1.Connectives.html#21632" class="Bound">y</a> <a id="21652" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="21653" class="Symbol">)</a>
                 <a id="21672" class="Symbol">;</a> <a id="21674" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="21676" href="plfa.part1.Connectives.html#10091" class="InductiveConstructor">inj₁</a> <a id="21681" href="plfa.part1.Connectives.html#21681" class="Bound">x</a> <a id="21683" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21685" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="21690" href="plfa.part1.Connectives.html#21690" class="Bound">z</a> <a id="21692" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="21694" class="Symbol">→</a> <a id="21696" class="Symbol">(</a><a id="21697" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="21702" href="plfa.part1.Connectives.html#21690" class="Bound">z</a><a id="21703" class="Symbol">)</a>
                 <a id="21722" class="Symbol">;</a> <a id="21724" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#1326" class="InductiveConstructor Operator">⟨</a> <a id="21726" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="21731" href="plfa.part1.Connectives.html#21731" class="Bound">z</a> <a id="21733" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21735" class="Symbol">_</a>      <a id="21742" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a> <a id="21744" class="Symbol">→</a> <a id="21746" class="Symbol">(</a><a id="21747" href="plfa.part1.Connectives.html#10133" class="InductiveConstructor">inj₂</a> <a id="21752" href="plfa.part1.Connectives.html#21731" class="Bound">z</a><a id="21753" class="Symbol">)</a>
                 <a id="21772" class="Symbol">}</a>
    <a id="21778" class="Symbol">;</a> <a id="21780" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Isomorphism.md %}{% raw %}#9266" class="Field">from∘to</a> <a id="21788" class="Symbol">=</a> <a id="21790" class="Symbol">λ{</a> <a id="21793" class="Symbol">(</a><a id="21794" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10091" class="InductiveConstructor">inj₁</a> <a id="21799" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟨</a> <a id="21801" href="plfa.part1.Connectives.html#21801" class="Bound">x</a> <a id="21803" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">,</a> <a id="21805" href="plfa.part1.Connectives.html#21805" class="Bound">y</a> <a id="21807" href="plfa.part1.Connectives.html#1326" class="InductiveConstructor Operator">⟩</a><a id="21808" class="Symbol">)</a> <a id="21810" class="Symbol">→</a> <a id="21812" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
                 <a id="21834" class="Symbol">;</a> <a id="21836" class="Symbol">(</a><a id="21837" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#10133" class="InductiveConstructor">inj₂</a> <a id="21842" href="plfa.part1.Connectives.html#21842" class="Bound">z</a><a id="21843" class="Symbol">)</a>         <a id="21853" class="Symbol">→</a> <a id="21855" href="Agda.Builtin.Equality.html#182" class="InductiveConstructor">refl</a>
                 <a id="21877" class="Symbol">}</a>
    <a id="21883" class="Symbol">}</a>
</pre>{% endraw %}Note that there is a choice in how we write the `from` function.
As given, it takes `⟨ inj₂ z , inj₂ z′ ⟩` to `inj₂ z`, but it is
easy to write a variant that instead returns `inj₂ z′`.  We have
an embedding rather than an isomorphism because the
`from` function must discard either `z` or `z′` in this case.

In the usual approach to logic, both of the distribution laws
are given as equivalences, where each side implies the other:

    A × (B ⊎ C) ⇔ (A × B) ⊎ (A × C)
    A ⊎ (B × C) ⇔ (A ⊎ B) × (A ⊎ C)

But when we consider the functions that provide evidence for these
implications, then the first corresponds to an isomorphism while the
second only corresponds to an embedding, revealing a sense in which
one of these laws is "more true" than the other.


#### Exercise `⊎-weak-×` (recommended)

Show that the following property holds:
{% raw %}<pre class="Agda"><a id="22736" class="Keyword">postulate</a>
  <a id="⊎-weak-×"></a><a id="22748" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#22748" class="Postulate">⊎-weak-×</a> <a id="22757" class="Symbol">:</a> <a id="22759" class="Symbol">∀</a> <a id="22761" class="Symbol">{</a><a id="22762" href="plfa.part1.Connectives.html#22762" class="Bound">A</a> <a id="22764" href="plfa.part1.Connectives.html#22764" class="Bound">B</a> <a id="22766" href="plfa.part1.Connectives.html#22766" class="Bound">C</a> <a id="22768" class="Symbol">:</a> <a id="22770" class="PrimitiveType">Set</a><a id="22773" class="Symbol">}</a> <a id="22775" class="Symbol">→</a> <a id="22777" class="Symbol">(</a><a id="22778" href="plfa.part1.Connectives.html#22762" class="Bound">A</a> <a id="22780" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="22782" href="plfa.part1.Connectives.html#22764" class="Bound">B</a><a id="22783" class="Symbol">)</a> <a id="22785" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="22787" href="plfa.part1.Connectives.html#22766" class="Bound">C</a> <a id="22789" class="Symbol">→</a> <a id="22791" href="plfa.part1.Connectives.html#22762" class="Bound">A</a> <a id="22793" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="22795" class="Symbol">(</a><a id="22796" href="plfa.part1.Connectives.html#22764" class="Bound">B</a> <a id="22798" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="22800" href="plfa.part1.Connectives.html#22766" class="Bound">C</a><a id="22801" class="Symbol">)</a>
</pre>{% endraw %}This is called a _weak distributive law_. Give the corresponding
distributive law, and explain how it relates to the weak version.

{% raw %}<pre class="Agda"><a id="22943" class="Comment">-- Your code goes here</a>
</pre>{% endraw %}

#### Exercise `⊎×-implies-×⊎` (practice)

Show that a disjunct of conjuncts implies a conjunct of disjuncts:
{% raw %}<pre class="Agda"><a id="23085" class="Keyword">postulate</a>
  <a id="⊎×-implies-×⊎"></a><a id="23097" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/part1/Connectives.md %}{% raw %}#23097" class="Postulate">⊎×-implies-×⊎</a> <a id="23111" class="Symbol">:</a> <a id="23113" class="Symbol">∀</a> <a id="23115" class="Symbol">{</a><a id="23116" href="plfa.part1.Connectives.html#23116" class="Bound">A</a> <a id="23118" href="plfa.part1.Connectives.html#23118" class="Bound">B</a> <a id="23120" href="plfa.part1.Connectives.html#23120" class="Bound">C</a> <a id="23122" href="plfa.part1.Connectives.html#23122" class="Bound">D</a> <a id="23124" class="Symbol">:</a> <a id="23126" class="PrimitiveType">Set</a><a id="23129" class="Symbol">}</a> <a id="23131" class="Symbol">→</a> <a id="23133" class="Symbol">(</a><a id="23134" href="plfa.part1.Connectives.html#23116" class="Bound">A</a> <a id="23136" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="23138" href="plfa.part1.Connectives.html#23118" class="Bound">B</a><a id="23139" class="Symbol">)</a> <a id="23141" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="23143" class="Symbol">(</a><a id="23144" href="plfa.part1.Connectives.html#23120" class="Bound">C</a> <a id="23146" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="23148" href="plfa.part1.Connectives.html#23122" class="Bound">D</a><a id="23149" class="Symbol">)</a> <a id="23151" class="Symbol">→</a> <a id="23153" class="Symbol">(</a><a id="23154" href="plfa.part1.Connectives.html#23116" class="Bound">A</a> <a id="23156" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="23158" href="plfa.part1.Connectives.html#23120" class="Bound">C</a><a id="23159" class="Symbol">)</a> <a id="23161" href="plfa.part1.Connectives.html#1295" class="Datatype Operator">×</a> <a id="23163" class="Symbol">(</a><a id="23164" href="plfa.part1.Connectives.html#23118" class="Bound">B</a> <a id="23166" href="plfa.part1.Connectives.html#10060" class="Datatype Operator">⊎</a> <a id="23168" href="plfa.part1.Connectives.html#23122" class="Bound">D</a><a id="23169" class="Symbol">)</a>
</pre>{% endraw %}Does the converse hold? If so, prove; if not, give a counterexample.

{% raw %}<pre class="Agda"><a id="23249" class="Comment">-- Your code goes here</a>
</pre>{% endraw %}

## Standard library

Definitions similar to those in this chapter can be found in the standard library:
{% raw %}<pre class="Agda"><a id="23386" class="Keyword">import</a> <a id="23393" href="https://agda.github.io/agda-stdlib/v1.1/Data.Product.html" class="Module">Data.Product</a> <a id="23406" class="Keyword">using</a> <a id="23412" class="Symbol">(</a><a id="23413" href="https://agda.github.io/agda-stdlib/v1.1/Data.Product.html#1162" class="Function Operator">_×_</a><a id="23416" class="Symbol">;</a> <a id="23418" href="Agda.Builtin.Sigma.html#225" class="Field">proj₁</a><a id="23423" class="Symbol">;</a> <a id="23425" href="Agda.Builtin.Sigma.html#237" class="Field">proj₂</a><a id="23430" class="Symbol">)</a> <a id="23432" class="Keyword">renaming</a> <a id="23441" class="Symbol">(</a><a id="23442" href="Agda.Builtin.Sigma.html#209" class="InductiveConstructor Operator">_,_</a> <a id="23446" class="Symbol">to</a> <a id="23449" href="Agda.Builtin.Sigma.html#209" class="InductiveConstructor Operator">⟨_,_⟩</a><a id="23454" class="Symbol">)</a>
<a id="23456" class="Keyword">import</a> <a id="23463" href="https://agda.github.io/agda-stdlib/v1.1/Data.Unit.html" class="Module">Data.Unit</a> <a id="23473" class="Keyword">using</a> <a id="23479" class="Symbol">(</a><a id="23480" href="Agda.Builtin.Unit.html#137" class="Record">⊤</a><a id="23481" class="Symbol">;</a> <a id="23483" href="Agda.Builtin.Unit.html#174" class="InductiveConstructor">tt</a><a id="23485" class="Symbol">)</a>
<a id="23487" class="Keyword">import</a> <a id="23494" href="https://agda.github.io/agda-stdlib/v1.1/Data.Sum.html" class="Module">Data.Sum</a> <a id="23503" class="Keyword">using</a> <a id="23509" class="Symbol">(</a><a id="23510" href="https://agda.github.io/agda-stdlib/v1.1/Data.Sum.Base.html#612" class="Datatype Operator">_⊎_</a><a id="23513" class="Symbol">;</a> <a id="23515" href="https://agda.github.io/agda-stdlib/v1.1/Data.Sum.Base.html#662" class="InductiveConstructor">inj₁</a><a id="23519" class="Symbol">;</a> <a id="23521" href="https://agda.github.io/agda-stdlib/v1.1/Data.Sum.Base.html#687" class="InductiveConstructor">inj₂</a><a id="23525" class="Symbol">)</a> <a id="23527" class="Keyword">renaming</a> <a id="23536" class="Symbol">(</a><a id="23537" href="https://agda.github.io/agda-stdlib/v1.1/Data.Sum.Base.html#798" class="Function Operator">[_,_]</a> <a id="23543" class="Symbol">to</a> <a id="23546" href="https://agda.github.io/agda-stdlib/v1.1/Data.Sum.Base.html#798" class="Function Operator">case-⊎</a><a id="23552" class="Symbol">)</a>
<a id="23554" class="Keyword">import</a> <a id="23561" href="https://agda.github.io/agda-stdlib/v1.1/Data.Empty.html" class="Module">Data.Empty</a> <a id="23572" class="Keyword">using</a> <a id="23578" class="Symbol">(</a><a id="23579" href="https://agda.github.io/agda-stdlib/v1.1/Data.Empty.html#279" class="Datatype">⊥</a><a id="23580" class="Symbol">;</a> <a id="23582" href="https://agda.github.io/agda-stdlib/v1.1/Data.Empty.html#294" class="Function">⊥-elim</a><a id="23588" class="Symbol">)</a>
<a id="23590" class="Keyword">import</a> <a id="23597" href="https://agda.github.io/agda-stdlib/v1.1/Function.Equivalence.html" class="Module">Function.Equivalence</a> <a id="23618" class="Keyword">using</a> <a id="23624" class="Symbol">(</a><a id="23625" href="https://agda.github.io/agda-stdlib/v1.1/Function.Equivalence.html#971" class="Function Operator">_⇔_</a><a id="23628" class="Symbol">)</a>
</pre>{% endraw %}The standard library constructs pairs with `_,_` whereas we use `⟨_,_⟩`.
The former makes it convenient to build triples or larger tuples from pairs,
permitting `a , b , c` to stand for `(a , (b , c))`.  But it conflicts with
other useful notations, such as `[_,_]` to construct a list of two elements in
Chapter [Lists]({{ site.baseurl }}/Lists/)
and `Γ , A` to extend environments in
Chapter [DeBruijn]({{ site.baseurl }}/DeBruijn/).
The standard library `_⇔_` is similar to ours, but the one in the
standard library is less convenient, since it is parameterised with
respect to an arbitrary notion of equivalence.


## Unicode

This chapter uses the following unicode:

    ×  U+00D7  MULTIPLICATION SIGN (\x)
    ⊎  U+228E  MULTISET UNION (\u+)
    ⊤  U+22A4  DOWN TACK (\top)
    ⊥  U+22A5  UP TACK (\bot)
    η  U+03B7  GREEK SMALL LETTER ETA (\eta)
    ₁  U+2081  SUBSCRIPT ONE (\_1)
    ₂  U+2082  SUBSCRIPT TWO (\_2)
    ⇔  U+21D4  LEFT RIGHT DOUBLE ARROW (\<=>)