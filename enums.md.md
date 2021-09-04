---


---

<pre><code>								Enums
</code></pre>
<p>An Enum is a way to organize a collection of related values.</p>
<p>Let’s see how does an Enum look like:</p>
<pre><code>enum Cards {
	Clubs,
	Hearts,
	Diamonds,
	Spades
}

// Lets try to access a value from Enum collection:
console.log(Cards.Clubs) = 0

</code></pre>
<p>If we try to assign a string to <code>Cards.Clubs</code>, lets see what happens:</p>
<pre><code>const cards = Cards.Clubs;
cards = 'test' // Error: cannot assign string to type CardsSuit

</code></pre>
<p>Can we assign boolean values in an <code>Enum</code>?</p>
<p>Lets see:</p>
<pre><code>enum SomethingRandom {
	true = true,
	false = false,
}
It will show an error, saying computed values cannot be used.
Hence anything of that sorts like (' ').join(&lt;value&gt;) which needs
computation cannot be used in Enums.
</code></pre>
<p>Recommended values to be used for Enums are <code>strings</code> and <code>numbers</code></p>

