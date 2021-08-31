---


---

<pre><code>			Readonly properties
</code></pre>
<p>Properties marked with <code>readonly</code> can only be assigned to during initialization or from within a constructor of the same class. All other assignments are disallowed.</p>
<p>Example:</p>
<pre><code>type Point = {
  readonly x: number;
  readonly y: number;
}

const axis: Point = { x: 0, y: 0 };
axis.x = 10 // Error, readonly prop cannot
//be reassigned
</code></pre>
<p>Readonly in Class:</p>
<pre><code>class Circle {
	readonly radius: number;
	constructor(radius: number) {
		this.radius = radius;
	}
	getarea() {
		return Math.PI  *  this.radius  ** 2;
	}
}

const circ = new Circle(1);
console.log(circ.radius);
console.log(circ.getarea());
circ.radius = 10 //Error, reassignment cannot be done to readonly values.
</code></pre>

