# MongoDb

##### Functions:

- .collection().  
- .find();        // trouver toutes les objets de la collection
- .findOne({});   // trouver un objet particulier 
- .sort({});      // trier par orde desc asc
- .limit();       // limit de list
- .insertOne();   // add new item
- .updateOne({ name: nameOfListing }, { $set: updatedListing });
- .deleteOne({ name: nameOfListing });
- ObjectId.isValid(id)