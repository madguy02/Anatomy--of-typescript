---


---

<pre><code>					keyof Type &amp; Extends
</code></pre>
<p>Typescript has this property called <code>keyof</code> which provides strict typings when dealing with mapped objects.</p>
<p>Lets see with an example:</p>
<pre><code>function getAllValues(obj: {}, key: string) {
	return obj[key];
}
</code></pre>
<p>From the above, we can see that we have added basic typing to maintain a sanity, but this doesn’t really help up us, whenever it comes to <code>key</code> being one of the property from the <code>object</code>. we can either do a union type to declare all of the props like this: <code>key: id | text | due</code> , but this isn’t a great practice when the size of the object is reasonably large.</p>
<p>What do we do then?</p>
<pre><code>interface Todo {
	id: string;
	text: string;
	due: Date;
}
function getAllValues(obj: Todo , key: keyof Todo) {
	return obj[key];
}
// The above function is strictly typed, since we did keyOf Todo
we can only pass the props which are a part of the interface, else
it throws an error.
</code></pre>
<p>Let’s see how we can use extends:</p>
<p>Consider a situation where we have to use generics, and we don’t have much idea of the exact fields apart from the key type and value type.</p>
<pre><code>type typeSignature = {[key: string]: number}

function getAll&lt;T  extends typeSignature&gt;(data: T, key: keyof  T) {

return data[key];

}
const obj = {id: 'vv', text: 2};
console.log(getAll(obj, 'id'))
</code></pre>
<p>Here, we declared a generic type called <code>typeSignature</code> where just the signature of the object is defined: the key is of type <code>string</code> and value is of type <code>number</code>.</p>
<p>Instead of just defining a type <code>T</code> we decided to extend it to use the <code>typeSignature</code>, so after that if we declare an object as above to have id as a string(ideally it should be a number as per signature), when we pass that object to the function we can see an error pops up saying:</p>
<pre><code>Argument of type '{ id: string; text: number; }' is not assignable to parameter of type 'typeSignature'.  
Property 'id' is incompatible with index signature.  
Type 'string' is not assignable to type 'number'

</code></pre>
<p>which means the <code>obj</code> doesn’t match the generic that uses the signature.</p>

