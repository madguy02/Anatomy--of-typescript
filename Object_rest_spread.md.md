---


---

<pre><code>					Object Rest and Spread
</code></pre>
<p>Lets start by declaring a simple object:</p>
<pre><code>const manish = {
website: 'http://madguy02.herokuapp.com',
name: 'Manish Kakoti',
twitter: '@KakotiManish',
github: 'madguy02'
}
</code></pre>
<p>How do we (in general) use a property from the object <code>manish</code>:</p>
<pre><code>const twitter = manish.twitter
</code></pre>
<p>Is there an other way around to get the properties ? :</p>
<pre><code>const {twitter, ...rest} = manish
console.log(twitter)
console.log(rest)
</code></pre>

