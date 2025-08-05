1.Find all cars with sunroof
db.cars.find({ sunroof: true })
2. Find all diesel cars
 db.cars.find({ fuel_type: "Diesel" })
3. Find all cars with more than 4 airbags
db.cars.find({ airbags: { $gt: 4 } })
4. Find cars with a feature like “Cruise Control”
db.cars.find({ features: "Cruise Control" })
 5. Get cars that use Automatic transmission and Petrol
db.cars.find({
  transmission: "Automatic",
  fuel_type: "Petrol"
})
6. Find cars with engine cc > 1500
db.cars.find({ "engine.cc": { $gt: 1500 } })
7. Find cars with "Bluetooth" feature AND sunroof
db.cars.find({
  features: "Bluetooth",
  sunroof: true
})


// 1. Basic Queries
1️⃣ Get all ca
s:db.cars.find()
2️⃣ Find a car by mod
l:db.cars.find({ model: "City" })
3️⃣ Find all diesel cars
db.cars.find({ fuel_type: "Diesel" })
4️⃣ Find all automatic transmission cars
db.cars.find({ transmission: "Automatic" })
// 🧠 2. Logical Operators
5️⃣ Cars that are Diesel OR have 6 airbags:
db.cars.find({
  $or: [
    { fuel_type: "Diesel" },
    { airbags: 6 }
  ]
})
6️⃣ Cars that are Petrol AND Automatic:
db.cars.find({
  fuel_type: "Petrol",
  transmission: "Automatic"
})
// 🔎 3. Comparison Operators
7️⃣ Cars with more than 4 airbags:
db.cars.find({ airbags: { $gt: 4 } })
8️⃣ Cars with engine cc less than or equal to 1500:
db.cars.find({ "engine.cc": { $lte: 1500 } })
//📋 4. Query Arrays
9️⃣ Cars that have "Cruise Control" as a feature:
db.cars.find({ features: "Cruise Control" })
🔟 Cars that have both "Bluetooth" and "Sunroof" features:
db.cars.find({ features: { $all: ["Bluetooth", "Sunroof"] } })
// 🧬 5. Nested Object Queries
1️⃣1️⃣ Cars with engine.type = "Turbocharged":
db.cars.find({ "engine.type": "Turbocharged" })

1️⃣2️⃣ Cars with engine torque "250 Nm":
db.cars.find({ "engine.torque": "250 Nm" })
//🎯 6. Projection (Only Show Certain Fields)
1️⃣3️⃣ Show only maker, model, and fuel_type (hide _id):
db.cars.find({}, { maker: 1, model: 1, fuel_type: 1, _id: 0 })
// 📐 7. Sorting & Limiting
1️⃣4️⃣ Sort cars by airbags descending:
db.cars.find().sort({ airbags: -1 })
1️⃣5️⃣ Get top 2 most powerful engines by cc:
db.cars.find().sort({ "engine.cc": -1 }).limit(2)
// 🧮 8. Count & Distinct
1️⃣6️⃣ Count how many Diesel cars:
db.cars.countDocuments({ fuel_type: "Diesel" })
1️⃣7️⃣ Get all distinct makers:
db.cars.distinct("maker")
// 🔧 9. Update & Add Fields

1️⃣8️⃣ Add a new field price to Honda City:
db.cars.updateOne(
  { model: "City" },
  { $set: { price: 1200000 } }
)
1️⃣9️⃣ Add a new feature to Creta:
db.cars.updateOne(
  { model: "Creta" },
  { $push: { features: "360-degree Camera" } }
)
// ❌ 10. Delete Queries
2️⃣0️⃣ Delete a car by model:
db.cars.deleteOne({ model: "Baleno" })
 //Step:1=>Aggregate Functions
 1)group by maker, count total cars, and calculate average price),
 db.cars.aggregate([
    {
        $group:{
        _id:"$maker",
        totalCars:{$sum:1},
        avgPrice:{$avg:"$price"}
        }
    }
])
2)For each car brand (maker), generate a report that includes:
->Total number of cars available
->Average car price
->Minimum and maximum price
->List of all models
->List of all unique fuel types used by that brand
db.cars.aggregate([
    {
       $group:{
         _id:"$maker",
        totalCars:{$sum:1},
        avgPrice:{$avg:"$price"},
        minPrice:{$min:"$price"},
        maxPrice:{$max:"$price"},
        allModels:{$push:"$model"},
        fuelTypedUsed:{$addToSet:"$fuel_type"}
       }
    }
])
 

//🔹 Step 2: Start With $match Stage (like a filter)
1: Get all cars with a sunroof and more than 4 airbags.
db.cars
=>
db.cars.aggregate([
    {
        $match:{
            sunroof:true,
            airbags:{$gt:4}
        }
    }
])
2:Get all Petrol cars with automatic transmission
=>
db.cars.aggregate([
    {
        $match:{
            fuel_type: "Petrol",
            transmission:"Automatic",
        }
    }
])
// 🔹 Step 3: $project — Select or Reshape Fields
1: Show only maker, model, and price
=>
db.cars.aggregate([
    {
        $project:{
            _id:0,
            maker:1,
            model:1,
            price:1,
        }
    }
])
2: Rename price to cost
=>
db.cars.aggregate([
    {
        $project:{
            _id:0,
            maker:1,
            model:1,
            cost:"$price"
        }
    }
])
3: Create a custom field isLuxury if price > 15L 
=>
db.cars.aggregate([
    {
        $project:{
            _id:0,
            maker:1,
            model:1,
            price:1,
            isLuxury:{
                $cond:{
                if:{$gt:["$price",1500000]},
                then:true,
                else:false
                }
            }
    }
}
])
4:Show only cars that have:
maker,
model,
fuel_type,
A new field highAirbags: true/false if airbags > 4
=>
db.cars.aggregate([
    {
        $project:{
            _id:0,
            maker:1,
            model:1,
            fuel_type:1,
            highAirbags:{
                $cond:{
                    if:{$gt:["$airbags",4]
                    },
                    then:true,
                    else:false
                }
            }
        }
    }
])
//Step 4: $group — Group and Summarize Data
// Basic Syntax->for Grouping
{
  $group: {
    _id: "$<fieldToGroupBy>",
    resultField1: { <accumulator>: "$<field>" },
    resultField2: { <accumulator>: "$<field>" },
    ...
  }
}
//  1)group by maker, count total cars, and calculate average price,all models),
=>
db.cars.aggregate([
    {
        $group:{
            _id:"$maker",
            totalCars:{$sum:1},
            avgPrice:{$avg:"$price"},
            minPrice:{$min:"$price"},
            maxPrice:{$max:"$price"},
            allModels:{$push:"$model"}
        }
    }
])
2: Group by fuel_type, calculate average price
=>
db.cars.aggregate([
    {
        $group:{
            _id:"$fuel_type",
            avgPrice:{$avg:"$price"}
        }
    }
])
3:Group cars by transmission
Count how many cars use each transmission
=>
db.cars.aggregate([
    {
        $group:{
            _id:"$transmission",
            toatlCars:{$sum:1}
        }
    }
])
// Step 5: $sort — Sort Your Results
1: Sort all cars by price (low to high)
db.cars.aggregate([
    {
        $sort:{price:1}
    }
])
// 2: Sort all cars by airbags (high to low)
db.cars.aggregate([
  { $sort: { airbags: -1 } }
])
//3: Group by fuel_type and sort by average price (high to low)
db.cars.aggregate([
    {
        $group:{
            _id:"$fuel_type",
            avgPrice:{$avg:"$price"}
        }
    },
    {
        $sort:{
            avgPrice:-1
        }
    }
])
// 4:Group by maker,Find average price,Sort makers by average price from highest to lowest
db.cars.aggregate([
    // stage->1
    {
        $group:{
            _id:"$maker",
            avgPrice:{$avg:"$price"}
        }
    },
    // stage->2
    {
        $sort:{
            avgPrice:-1
        }
    }
])
//🔶 Step 6: $unwind — Explode Arrays into Individual Documents

//this turns
{
  model: "Creta",
  owners: [
    { name: "Raju", location: "Mumbai" },
    { name: "Shyam", location: "Delhi" }
  ]
}
// into
{ model: "Creta", owners: { name: "Raju", location: "Mumbai" } }
{ model: "Creta", owners: { name: "Shyam", location: "Delhi" } }
// 1:Unwind Owners
=>
db.cars.aggregate([
    {
        $unwind:"$owners"
    },
    {
        $project:{
            _id:0,
            maker:1,
            model:1,
            ownerName:"$owners.name",
            location:"$owners.location",
            purchase_date:"$owners.purchase_date"
        }
    }
])
// 2: Find the total service cost per car model.
// Each car has a service_history array with multiple service records (each having a cost).
db.cars.aggregate([
    {
        $unwind:"$service_history"
    },
    {
        $group:{
            _id:"$model",
            totalServiceCost:{$sum:"$service_history.cost"}
        }
    }
])
// Count method 
// 1) print total n. of Hyundai cars
db.cars.aggregate([
    {
        $match:{
            maker:"Hyundai"
        }
    },
    {
        $count:"totalCars"
    }
])
// Most Frequently Used String Operators in MongoDB
1. $concat — Combine Strings
db.cars.aggregate([
    {
        $project:{
            _id:0,
            fullName:{
                $concat:["$maker"," ","$model"]
            }
        }
    }
])
2. $toUpper / $toLower — Case Formatting
db.cars.aggregate([
    {
        $project:{
            _id:0,
            modelUpper:{
                $toUpper:"$model"
            },
            modelLower:{
                $toLower:"$model"
            },
        }
    }
])
3. $substr — Shorten a String
db.cars.aggregate([
    {
        $project:{
            _id:0,
            shortModel: { $substr: ["$model", 0, 3] } // first 3 letters
        }
    }
])
4. $regexMatch — Filter with Patterns (like SQL LIKE)
i)Find all cars whose model starts with "C":
=>
db.cars.aggregate([
    {
        $match:{
            model:{
                $regex:/^C/,
                $options:"i"
            }
        }
    }
])
//Show all car maker, model, and a new field code like this format:
// "HYU-CRE" (3 uppercase letters of maker + "-" + 3 letters of model)
db.cars.aggregate([
  {
    $project: {
      _id: 0,
      maker: 1,
      model: 1,
      code: {
        $concat: [
          { $toUpper: { $substr: ["$maker", 0, 3] } }, // "HYU"
          "-",
          { $toUpper: { $substr: ["$model", 0, 3] } }  // "CRE"
        ]
      }
    }
  }
])
// Add a flag isDiesel =true/false foe each car 
db.cars.aggregate([
    {
        $project:{
            _id:0,
            model:1,
            maker:1,
            isDiesel:{
                $cond:{
                    if:{
                        $eq:["$fuel_type", "Diesel"]
                    },
                    then:true,
                    else:false
                }
            }
        }
    }
])

//$out is used at the end of an aggregation pipeline to save the output documents into a new collection (or overwrite an existing one).
db.sourceCollection.aggregate([
  { /* some aggregation stages */ },
  { $out: "newCollectionName" }
])
1:Let’s say we want to group cars by maker and store that as a new collection called carMakers
=>
db.cars.aggregate([
    {
        $group:{
            _id:"$maker",
            cars:{$sum:1}
        }
    },
    {
        $out:"carMakers"
    }
])
✅ 1. $add – Add two values
Let’s say we want to add a fixed ₹20000 road tax to every car’s price:
db.cars.aggregate([
    {
        $project:{
            _id:0,
            model:1,
            maker:1,
            price:1,
            finalPrice:{
                $add:["$price",20000]
            }
        }
    }
])
✅ 2. $subtract – Remove discount
db.cars.aggregate([
    {
        $project:{
            model:1,
            discountedPrice:{
                $subtract:["$price",50000]
            }
        }
    }
])
✅ 3. $multiply – Multiply price (e.g., for 5-year insurance)
db.cars.aggregate([
    {
        $project:{
            model:1,
            price:1,
            insuranceCost5Years:{
                $multiply:["$price",0.10,5]
            }
        }
    }
])
✅ 4. $divide – Get average cost per airbag
db.cars.aggregate([
    {
        $project:{
            model:1,
            costPerAirbag:{
                $divide:["$price","$airbags"]
            }
        }
    }
]
✅ 5. $mod – Even or odd price check
db.cars.aggregate([
    {
        $project:{
            _id:0,
            model:1,
            priceIsEven:{
               $eq:[ {$mod:["$price",2]},0]
            }
        }
    }
])
// Conditional Operator
✅ 1. $cond – Basic If-Then-Else
 Mark cars with more than 4 airbags as highSafety
 db.cars.aggregate([
    {
        $project:{
            model:1,
            airbags:1,
            highSafety:{
                $cond:{
                    if:{$gt:["$airbags",4]},
                    then:true,
                    else:false
                }
            }
        }
    }
 ])
 ✅ 2. $ifNull – Replace null with default
 //If engine.type is missing or null, "Unknown" will be used instead.
 db.cars.aggregate([
    {
        $project:{
            _id:0,
            engineType:{
                $ifNull:["$engine.type", "Unknown"]
            }
        }
    }
 ])
 // Practice Problem
 Show model, price, and a new field isExpensive which is true if price > ₹15,00,000, else false.
 db.cars.aggregate([
    {
        $project:{
            _id:0,
            price:1,
            isExpensive:{
                $cond:{
                    if:{
                        $gt:["$price",1500000]
                    },
                    then:true,
                    else:false
                }
            }
        }
    }
 ])
 // $switch is pending
 db.cars.aggregate([
    {
        $project:{
            _id:0,
            model:1,
            taxSlab:{
                $switch:{
                    branches:[
                        {case:{$lt:["$price",8000000]},then:"Low"},
                        {case:{$lt:["$price",1500000]},then:"Medium"}
                    ],
                    default:"High"
                }
            }
        }
    }
 ])

Problem:For each car in the cars collection, show:model,price,
A new field called segment with the following values:
"Premium" if price > 15,00,000
"Mid-Range" if price > 10,00,000 but ≤ 15,00,000
"Budget" otherwise
=>
db.cars.aggregate([
    {
        $project:{
            _id:0,
            model:1,
            price:1,
            segment:{
                $switch:{
                    branches:[
                        {case:{$gt:["$price",1500000]},then:"Premium"},
                        {case:{$gt:["$price",1000000]},then:"Mid-range"}
                    ],
                    default:"Budget"
                }
            }
        }
    }
])
// mongodb variables 
System Generated Variables
There are lots of SGV you cann explore
=>
db.cars.aggregate([
    {
        $project:{
            model:1,
            price:1,
            date:"$$NOW"
        }
    }
])
User Defined Variables 
=> // Already Covered


// Relationship in MongoDb
->Embeded Document(limit:16Mb,deepLevels:100)
->Refernce Document()
// see ppt or chatgpt for more informations
🧾 Collection: users
{
  _id: 'user1',
  name: 'Amit Sharma',
  email: 'amit.sharma@example.com',
  phone: '+91-987654210',
  address: 'MG Road, Mumbai, Maharashtra'
}
📦 Collection: orders
{
  _id: 'order1',
  user_id: 'user1',
  product: 'Laptop',
  amount: 50000,
  order_date: '2024-08-01'
}
We can now use $lookup to join orders with users.
🔗 What is $lookup?
$lookup is used in MongoDB Aggregation to join two collections, similar to a SQL JOIN
=>
db.users.aggregate([
    {
        $lookup:{
            from:"orders",
            localField:"_id",
            foreignField:"user_id",
            as:"orders"
        }
      
    },  {
            $unwind:"$orders"
        }
])

// Validation Schema
Creating a Collection With Schema Validation
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "email", "age"],
      properties: {
        name: {
          bsonType: "string",
          description: "must be a string and is required"
        },
        email: {
          bsonType: "string",
          pattern: "^.+@.+$",
          description: "must be a valid email"
        },
        age: {
          bsonType: "int",
          minimum: 18,
          maximum: 99,
          description: "must be an integer in [18, 99]"
        },
        phone: {
          bsonType: "string",
          description: "optional but must be a string if present"
        }
      }
    }
  },
  validationLevel: "strict",     
  validationAction: "error"
})
🔁 Modify Schema on Existing Collection
db.runCommand({
  collMod: "users",
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["email"],
      properties: {
        email: {
          bsonType: "string",
          pattern: "^.+@.+$"
        }
      }
    }
  },
  validationLevel: "strict",
  validationAction: "error"
})


Index padhliya bas ekbar chatgpt kar k dekhlena otna complicated nahi hain
tm theory portion v padhlena chatgpt se 


