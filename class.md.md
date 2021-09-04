---


---

<pre><code>							Classes
</code></pre>
<p><code>Classes</code> have full support in Typescript. Let’s see how classes work.</p>
<p>How to declare a class:</p>
<pre><code>class Person{}
</code></pre>
<p>This class above is an <code>empty class</code> and not very useful.</p>
<p>Let’s declare a class that is productive and we could do some operations with it.</p>
<pre><code>class City {
	total_population: number;
	total_houses: number;
	good_roads: string[];
	worst_roads: string[];
	employed: number;
	electricity_supply: string[];
	constructor(total_population: number, total_houses: number,
	good_roads: string[], worst_roads: string[], employed: number
	electricity_supply: string[]) {
	this.total_population = total_population;
	this.total_houses = total_houses;
	this.good_roads = good_roads;
	this.worst_roads = worst_roads;
	this.employed = employed;
	}
	public getGooRoadsPercentage(good_roads: string[], worst_roads: string[]) {
		const total_good_roads = good_roads.length;
		const total_worst_roads = worst_roads.length;
		
		const total_roads = total_good_roads + total_worst_roads
		return (total_good_roads/total_roads) * 100;
	}
}

const cities = new City (10000, 600, ['gandhi', 'netaji', 'vijayanagar', 'mg road', 'marathahalli road'], ['civil road', 'electronic city', 'koromangala', 'indiranagar'], 1200, ['koramagala', 'indiranagar'] )

const percent = cities.getGooRoadsPercentage(cities.good_roads, cities.worst_roads);

console.log(percent);

</code></pre>

