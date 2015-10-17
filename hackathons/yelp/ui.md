# UI

Pick one question class and build an exploratory visualization interface for it.
The question class you pick must have at least three variables that can be changed.

## At time X on day Y how many businesses are open in city Z


<div style="border:1px grey solid; padding:5px;">
    <div><h5>X</h5>
        <input id="time" type="text" value="11"/>
    </div>
    <div><h5>Y</h5>
        <input id="day" type="text" value="Sunday"/>
    </div>
    <div><h5>Z</h5>
        <input id="state" type="text" value="PA"/>
    </div>    
    <div style="margin:20px;">
        <button id="viz">Vizualize</button>
    </div>
</div>

<div class="myviz" style="width:100%; height:500px; border: 1px black solid; padding: 5px;">
Data is not loaded yet
</div>

{% script %}
items = 'not loaded yet'

$.get('http://bigdatahci2015.github.io/data/yelp/yelp_academic_dataset_business.5000.json.lines.txt')
    .success(function(data){        
        var lines = data.trim().split('\n')

        // convert text lines to json arrays and save them in `items`
        items = _.map(lines, JSON.parse)

        console.log('number of items loaded:', items.length)

        console.log('first item', items[0])
     })
     .error(function(e){
         console.error(e)
     })

function viz(time, day, state){    

    // define a template string
    var tplString = '<g transform="translate(0 ${d.y})"> \
                    <text y="20" x="0">${d.label}</text> \
                    <rect x="200"   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:1; \
                                stroke:rgb(0,0,0)" />   \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    var openFilter = _.filter(items, function(d) {
        return d.hours[day] && time >= d.hours[day].open.split(':')[0] && time <= d.hours[day].close.split(':')[0] && d.state == state;
    })

    var cities = _.pairs(_.groupBy(openFilter, 'city'))

    console.log('cities', cities)
    
    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {        
        return _.size(d[1])
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }

    function computeLabel(d, i) {
        return d[0] + ': ' + _.size(d[1])
    }

    var viz = _.map(cities, function(d, i){                
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
                    label: computeLabel(d, i),
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg width="100%" height="100%">' + result + '</svg>')
}

$('button#viz').click(function(){    
    var time = $('#time').val()
    var day = $('#day').val()
    var state = $('#state').val()    
    viz(time, day, state)
})
{% endscript %}

# Authors

This UI is developed by
* [Satchel Spencer](https://github.com/satchelspencer)
* [John Murphy](https://github.com/johnmurph27)
* [Nicole Woytarowicz](https://github.com/nicolele)
* [Tristan Wagar](https://github.com/twagar95)
* [Sushant Mittal](https://github.com/sumi6109)