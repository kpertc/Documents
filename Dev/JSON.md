
```JSON
{
    "name" : "Kyle",
    "FavoriteNumber" : 3,
    "isProgrammer": true,
    "hobbies" : ["Weight Lifting", "Bowling"],
    "friends" : [{
        "name" : "Joey",
        "FavoriteNumber" : 3
    
    
    }]
}
```

no trailing comma / no comment / keys must be double-quoted

Convert string to JSON

JSON.parse()  // throws on bad input → try/catch

JSON to string

JSON.stringify(obj)
JSON.stringify(obj, null, 2)  // pretty print
// silently drops undefined / function / Symbol