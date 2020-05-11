// Nouvelle database de monuments

use monuments

// Création d'une nouvelle collection positions

db.createCollection('positions');

// Ajout des points dans la collection positions

db.positions.insertMany([
{nom: "Tour Eiffel", location: { type: "Point", coordinates: [48.85826347212501,2.294340133666992] } },
{nom: "Grande Arche de la Défense", location: { type: "Point", coordinates: [48.890963072811935,2.241339683532715] } },
{nom: "Charles de Gaulle", location: { type: "Point", coordinates: [48.873832671833504,2.2950267791748047] } }
]);

// 1)

db.positions.find({
location: {
$geoWithin: { 
      $geometry: {
type: "Polygon",
coordinates:
[  
[  
[48.86990906900767,2.2360610961914062],
[48.86990906900767,2.3016357421875],
[48.89575966221592,2.3016357421875],
[48.89575966221592,2.2360610961914062],
[48.86990906900767,2.2360610961914062]
]
]
}
}
}
}).pretty();

// 2)

db.positions.findOne({
location: {
$near: {
      $geometry: {
type: "Point",
coordinates: [48.8737479930069,2.277088165283203],
},
},
},
});

// 3)

db.positions.find({
location: {
$geoWithin: {
      $geometry: {
type: "Polygon",
coordinates: [
[
[
48.848902682969765,
2.2340011596679687
],
[
48.848902682969765,
2.3184585571289062
],
[
48.897678169122194,
2.3184585571289062
],
[
48.897678169122194,
2.2340011596679687

],
[
48.848902682969765,
2.2340011596679687
]
],
],
},
},
},
});
