---


---

<pre><code>	        Types vs Interfaces
</code></pre>
<p>Types and Interfaces both are similar and act very similarly. However there are subtle differences in both of them.</p>
<p>When to use  <code>type</code>:</p>
<ul>
<li>Use  <code>type</code>  when defining an alias for primitive types (string, boolean, number, bigint, symbol, etc)</li>
<li>Use  <code>type</code>  when defining tuple types</li>
<li>Use  <code>type</code>  when defining function types</li>
<li>Use  <code>type</code>  when defining a union</li>
<li>Use  <code>type</code>  when trying to overload functions in object types via composition</li>
<li>Use  <code>type</code>  when needing to take advantage of mapped types</li>
</ul>
<p>When to use  <code>interface</code>:</p>
<ul>
<li>Use  <code>interface</code>  for all object types where using  <code>type</code>  is not required (see above)</li>
<li>Use  <code>interface</code>  when you want to take advatange of declaration merging.</li>
</ul>
<p>From Stackoverflow:</p>
<h2 id="primitive-types">Primitive types</h2>
<p>The easiest difference to see between  <code>type</code>  and  <code>interface</code>  is that only  <code>type</code>  can be used to alias a primitive:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">type Nullish <span class="token operator">=</span> <span class="token keyword">null</span> <span class="token operator">|</span> undefined<span class="token punctuation">;</span>
type Fruit <span class="token operator">=</span> <span class="token string">'apple'</span> <span class="token operator">|</span> <span class="token string">'pear'</span> <span class="token operator">|</span> <span class="token string">'orange'</span><span class="token punctuation">;</span>
type Num <span class="token operator">=</span> number <span class="token operator">|</span> bigint<span class="token punctuation">;</span>

</code></pre>
<p>None of these examples are possible to achieve with interfaces.</p>
<p>💡 When providing a type alias for a primitive value, use the  <code>type</code>  keyword.</p>
<h2 id="tuple-types">Tuple types</h2>
<p>Tuples can only be typed via the  <code>type</code>  keyword:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">type row <span class="token operator">=</span> <span class="token punctuation">[</span>colOne<span class="token punctuation">:</span> number<span class="token punctuation">,</span> colTwo<span class="token punctuation">:</span> string<span class="token punctuation">]</span><span class="token punctuation">;</span>

</code></pre>
<p>💡 Use the  <code>type</code>  keyword when providing types for tuples.</p>
<h2 id="function-types">Function types</h2>
<p>Functions can be typed by both the  <code>type</code>  and  <code>interface</code>  keywords:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token comment">// via type</span>
type <span class="token function-variable function">Sum</span> <span class="token operator">=</span> <span class="token punctuation">(</span>x<span class="token punctuation">:</span> number<span class="token punctuation">,</span> y<span class="token punctuation">:</span> number<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> number<span class="token punctuation">;</span>

<span class="token comment">// via interface</span>
<span class="token keyword">interface</span> <span class="token class-name">Sum</span> <span class="token punctuation">{</span>
  <span class="token punctuation">(</span>x<span class="token punctuation">:</span> number<span class="token punctuation">,</span> y<span class="token punctuation">:</span> number<span class="token punctuation">)</span><span class="token punctuation">:</span> number<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

</code></pre>
<p>Since the same effect can be achieved either way, the rule will be to use  <code>type</code>  in these scenarios since it’s a little easier to read (and less verbose).</p>
<p>💡 Use  <code>type</code>  when defining function types.</p>
<h2 id="union-types">Union types</h2>
<p>Union types can only be achieved with the  <code>type</code>  keyword:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">type Fruit <span class="token operator">=</span> <span class="token string">'apple'</span> <span class="token operator">|</span> <span class="token string">'pear'</span> <span class="token operator">|</span> <span class="token string">'orange'</span><span class="token punctuation">;</span>
type Vegetable <span class="token operator">=</span> <span class="token string">'broccoli'</span> <span class="token operator">|</span> <span class="token string">'carrot'</span> <span class="token operator">|</span> <span class="token string">'lettuce'</span><span class="token punctuation">;</span>

<span class="token comment">// 'apple' | 'pear' | 'orange' | 'broccoli' | 'carrot' | 'lettuce';</span>
type HealthyFoods <span class="token operator">=</span> Fruit <span class="token operator">|</span> Vegetable<span class="token punctuation">;</span>

</code></pre>
<p>💡 When defining union types, use the  <code>type</code>  keyword</p>
<h2 id="object-types">Object types</h2>
<p>An object in javascript is a key/value map, and an “object type” is typescript’s way of typing those key/value maps. Both  <code>interface</code>  and  <code>type</code>  can be used when providing types for an object as the original question makes clear. So when do you use  <code>type</code>  vs  <code>interface</code>  for object types?</p>
<h3 id="intersection-vs-inheritance">Intersection vs Inheritance</h3>
<p>With types and composition, I can do something like this:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">interface</span> <span class="token class-name">NumLogger</span> <span class="token punctuation">{</span> 
    log<span class="token punctuation">:</span> <span class="token punctuation">(</span>val<span class="token punctuation">:</span> number<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token keyword">void</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
type StrAndNumLogger <span class="token operator">=</span> NumLogger <span class="token operator">&amp;</span> <span class="token punctuation">{</span> 
  log<span class="token punctuation">:</span> <span class="token punctuation">(</span>val<span class="token punctuation">:</span> string<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token keyword">void</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">const</span> logger<span class="token punctuation">:</span> StrAndNumLogger <span class="token operator">=</span> <span class="token punctuation">{</span>
  log<span class="token punctuation">:</span> <span class="token punctuation">(</span>val<span class="token punctuation">:</span> string <span class="token operator">|</span> number<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>val<span class="token punctuation">)</span>
<span class="token punctuation">}</span>

logger<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span>
logger<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">'hi'</span><span class="token punctuation">)</span>

</code></pre>
<p>Typescript is totally happy. What about if I tried to extend that with interface:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">
<span class="token keyword">interface</span> <span class="token class-name">StrAndNumLogger</span> <span class="token keyword">extends</span> <span class="token class-name">NumLogger</span> <span class="token punctuation">{</span> 
    log<span class="token punctuation">:</span> <span class="token punctuation">(</span>val<span class="token punctuation">:</span> string<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token keyword">void</span><span class="token punctuation">;</span> 
<span class="token punctuation">}</span><span class="token punctuation">;</span>

</code></pre>
<p>The declaration of  <code>StrAndNumLogger</code>  gives me an  <a href="https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgHIFcC2AZA9gc32mQG9kAoZK5AGwIC5kAKANzhsZCwCNoBKZAF4AfMha5gAEwDc5AL7lQkWIhQBlMFACCISRhwEiUZBAAekXQGc0WPIWJlK1Ovkat2jS5tD4BIsRIyFHLSQA">error</a>:</p>
<p><code>Interface 'StrAndNumLogger' incorrectly extends interface 'NumLogger'</code></p>
<p>With interfaces, the subtypes have to exactly match the types declared in the super type, otherwise TS will throw an error like the one above.</p>
<p>💡 When trying to overload functions in object types, you’ll be better off using the  <code>type</code>  keyword.</p>
<h3 id="declaration-merging">Declaration Merging</h3>
<p>The key aspect to interfaces in typescript that distinguish them from types is that they can be extended with new functionality after they’ve already been declared. A common use case for this feature occurs when you want to extend the types that are exported from a node module. For example,  <code>@types/jest</code>  exports types that can be used when working with the jest library. However, jest also allows for extending the main  <code>jest</code>  type with new functions. For example, I can add a custom test like this:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">jest<span class="token punctuation">.</span>timedTest <span class="token operator">=</span> <span class="token keyword">async</span> <span class="token punctuation">(</span>testName<span class="token punctuation">,</span> wrappedTest<span class="token punctuation">,</span> timeout<span class="token punctuation">)</span> <span class="token operator">=&gt;</span>
  <span class="token function">test</span><span class="token punctuation">(</span>
    testName<span class="token punctuation">,</span>
    <span class="token keyword">async</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
      <span class="token keyword">const</span> start <span class="token operator">=</span> Date<span class="token punctuation">.</span><span class="token function">now</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
      <span class="token keyword">await</span> <span class="token function">wrappedTest</span><span class="token punctuation">(</span>mockTrack<span class="token punctuation">)</span><span class="token punctuation">;</span>
      <span class="token keyword">const</span> end <span class="token operator">=</span> Date<span class="token punctuation">.</span><span class="token function">now</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

      console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token template-string"><span class="token string">`elapsed time in ms: </span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>end <span class="token operator">-</span> start<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">`</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    timeout
  <span class="token punctuation">)</span><span class="token punctuation">;</span>

</code></pre>
<p>And then I can use it like this:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">test<span class="token punctuation">.</span><span class="token function">timedTest</span><span class="token punctuation">(</span><span class="token string">'this is my custom test'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
  <span class="token function">expect</span><span class="token punctuation">(</span><span class="token boolean">true</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">toBe</span><span class="token punctuation">(</span><span class="token boolean">true</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

</code></pre>
<p>And now the time elapsed for that test will be printed to the console once the test is complete. Great! There’s only one problem - typescript has no clue that i’ve added a  <code>timedTest</code>  function, so it’ll throw an error in the editor (the code will run fine, but TS will be angry).</p>
<p>To resolve this, I need to tell TS that there’s a new type on top of the existing types that are already available from jest. To do that, I can do this:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">declare namespace jest <span class="token punctuation">{</span>
  <span class="token keyword">interface</span> <span class="token class-name">It</span> <span class="token punctuation">{</span>
    timedTest<span class="token punctuation">:</span> <span class="token punctuation">(</span>name<span class="token punctuation">:</span> string<span class="token punctuation">,</span> fn<span class="token punctuation">:</span> <span class="token punctuation">(</span>mockTrack<span class="token punctuation">:</span> Mock<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> any<span class="token punctuation">,</span> timeout<span class="token operator">?</span><span class="token punctuation">:</span> number<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token keyword">void</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

</code></pre>
<p>Because of how interfaces work, this type declaration will be  <em>merged</em>  with the type declarations exported from  <code>@types/jest</code>. So I didn’t just re-declare  <code>jest.It</code>; I extended  <code>jest.It</code>  with a new function so that TS is now aware of my custom test function.</p>
<p>This type of thing is not possible with the  <code>type</code>  keyword. If  <code>@types/jest</code>  had declared their types with the  <code>type</code>  keyword, I wouldn’t have been able to extend those types with my own custom types, and therefore there would have been no good way to make TS happy about my new function. This process that is unique to the  <code>interface</code>  keyword is called  <a href="https://www.typescriptlang.org/docs/handbook/declaration-merging.html">declaration merging</a>.</p>
<p>Declaration merging is also possible to do locally like this:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">interface</span> <span class="token class-name">Person</span> <span class="token punctuation">{</span>
  name<span class="token punctuation">:</span> string<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">interface</span> <span class="token class-name">Person</span> <span class="token punctuation">{</span>
  age<span class="token punctuation">:</span> number<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// no error</span>
<span class="token keyword">const</span> person<span class="token punctuation">:</span> Person <span class="token operator">=</span> <span class="token punctuation">{</span>
  name<span class="token punctuation">:</span> <span class="token string">'Mark'</span><span class="token punctuation">,</span>
  age<span class="token punctuation">:</span> <span class="token number">25</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

</code></pre>
<p>If I did the exact same thing above with the  <code>type</code>  keyword, I would have gotten an error since types cannot be re-declared/merged. In the real world, javascript objects are much like this  <code>interface</code>  example; they can be dynamically updated with new fields at runtime.</p>
<p>💡 Because interface declarations can be merged, interfaces more accurately represent the dynamic nature of javascript objects than types do, and they should be preferred for that reason.</p>
<h3 id="mapped-object-types">Mapped object types</h3>
<p>With the  <code>type</code>  keyword, I can take advantage of  <a href="https://www.typescriptlang.org/docs/handbook/advanced-types.html#mapped-types">mapped types</a>  like this:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">type Fruit <span class="token operator">=</span> <span class="token string">'apple'</span> <span class="token operator">|</span> <span class="token string">'orange'</span> <span class="token operator">|</span> <span class="token string">'banana'</span><span class="token punctuation">;</span>

type FruitCount <span class="token operator">=</span> <span class="token punctuation">{</span>
  <span class="token punctuation">[</span>key <span class="token keyword">in</span> Fruit<span class="token punctuation">]</span><span class="token punctuation">:</span> number<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">const</span> fruits<span class="token punctuation">:</span> FruitCount <span class="token operator">=</span> <span class="token punctuation">{</span>
  apple<span class="token punctuation">:</span> <span class="token number">2</span><span class="token punctuation">,</span>
  orange<span class="token punctuation">:</span> <span class="token number">3</span><span class="token punctuation">,</span>
  banana<span class="token punctuation">:</span> <span class="token number">4</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

</code></pre>
<p>This cannot be done with interfaces:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">type Fruit <span class="token operator">=</span> <span class="token string">'apple'</span> <span class="token operator">|</span> <span class="token string">'orange'</span> <span class="token operator">|</span> <span class="token string">'banana'</span><span class="token punctuation">;</span>

<span class="token comment">// ERROR: </span>
<span class="token keyword">interface</span> <span class="token class-name">FruitCount</span> <span class="token punctuation">{</span>
  <span class="token punctuation">[</span>key <span class="token keyword">in</span> Fruit<span class="token punctuation">]</span><span class="token punctuation">:</span> number<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

</code></pre>
<p>💡 When needing to take advantage of mapped types, use the  <code>type</code>  keyword</p>
<h3 id="performance">Performance</h3>
<p>Much of the time, a simple type alias to an object type acts very similarly to an interface.</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">interface</span> <span class="token class-name">Foo</span> <span class="token punctuation">{</span> prop<span class="token punctuation">:</span> string <span class="token punctuation">}</span>

type Bar <span class="token operator">=</span> <span class="token punctuation">{</span> prop<span class="token punctuation">:</span> string <span class="token punctuation">}</span><span class="token punctuation">;</span>

</code></pre>
<p>However, and as soon as you need to compose two or more types, you have the option of extending those types with an interface, or intersecting them in a type alias, and that’s when the differences start to matter.</p>
<p>Interfaces create a single flat object type that detects property conflicts, which are usually important to resolve! Intersections on the other hand just recursively merge properties, and in some cases produce never. Interfaces also display consistently better, whereas type aliases to intersections can’t be displayed in part of other intersections. Type relationships between interfaces are also cached, as opposed to intersection types as a whole. A final noteworthy difference is that when checking against a target intersection type, every constituent is checked before checking against the “effective”/“flattened” type.</p>
<p>For this reason, extending types with interfaces/extends is suggested over creating intersection types.</p>
<p>More on  <a href="https://github.com/microsoft/TypeScript/wiki/Performance">typescript wiki</a>.</p>

