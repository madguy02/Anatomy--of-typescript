---


---

<pre><code>			Non-Nullable Types
</code></pre>
<p>Earlier prior to TS2.0, values can be assigned with types like null or undefined along with the actual value.</p>
<p>Example:</p>
<pre><code>let name:  string;
name =  "Marius"; // OK  
name =  null; // OK  
name =  undefined; // OK  

let age:  number;  
age =  24; // OK  
age =  null; // OK  
age =  undefined; // OK
</code></pre>
<p><em>Above is only for TS prior to TS2.0, try this out on TS post 2.0 and see if throws error</em>.</p>
<p>Post TS2.0, we cannot assign a value of type <code>string</code> or <code>number</code> to <code>null</code> or <code>undefined</code></p>
<p>if you want to assign a variable with its value as <code>null</code> or <code>undefined</code>, you have to explicitly mention it on its type</p>
<p>Example:</p>
<pre><code>let value: string | null;
value = null;
</code></pre>
<p>Let’s see how it impacts in a function:</p>
<pre><code>function getStringLength(s: string | null){
	// Error: s is possibly null
	return s.length
}
</code></pre>
<p>What do we understand here?</p>
<p>Simple: here s is of type <code>string | null</code> (union of <code>string</code> and <code>null</code>). So,<code>s</code> can very well be a <code>string</code> or a <code>null</code>, if its a <code>null</code> we can’t just do <code>s.length</code>.</p>
<p>What do we need to do in order to avoid this type issue?</p>
<pre><code>function getStringLength(s: string | null){
	// added an `if` condition here to check if s is neither undefined or null
	if (!s){
	return;
	}
	// here s is definitely string, hence we can find the length out
	return s.length;
}
</code></pre>
<p>Function invokation with Nullable Types:</p>
<pre><code>function callSomething(callback?:() =&gt; void){
	// the check is needed to see if the function isn't undefined or null
	if (callback){
		callback();
	}
}
</code></pre>
<p>Summary:</p>
<pre><code>Non-nullable types are a fundamental and valuable addition to TypeScript's type system. They allow for precise modeling of which variables and properties are nullable. A property access or function call is only allowed after a type guard has determined it to be safe, thus preventing many nullability errors at compile-time.
</code></pre>

