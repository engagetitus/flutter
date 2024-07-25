# Project 1 - SOKO Garden

## Background
soko Garden is an Ecommerce system. Done by Flask.
Basically allows users to login and order products.
---
vendors post products.
To reinforce your learn on Http requests and Asynchronous programming; we will be building a mobile client for the same.

## step 1 : create Flutter project
```sh
flutter create sokogarden
```

## Step 2 : Layout Project
```sh
\lib
\lib\api\product.dart
\lib\controllers\user.dart
\lib\controllers\payments.dart
\lib\controllers\products.dart
\lib\screens\add_product.dart
\lib\screens\create_product.dart
\lib\screens\mpesa.dart
\lib\screens\products.dart
\lib\screens\single_product.dart
\lib\main.dart
```
## Prerequisites
We will be fetching data from the parent system via apis. Your pubspec.yaml file should be depending on atleast these packages


```yaml
  flex_color_scheme: ^7.3.1
  http: ^1.2.1
  intl: ^0.19.0

```
here is how to add them from the terminal
```sh
flutter pub add intl
flutter pub add http
```
## products
```dart
import 'dart:convert';

import 'package:http/http.dart' as http;

import '../api/products.dart';

Future fetchProductbyId(int id) async {
  http.Response feedback = await http.post(
      Uri.parse(
        '$baseurl/api/single_item',
      ),
      headers: {'Content-type': 'application/json'},
      body: json.encode({'id': id}));
  if (feedback.statusCode == 200) {
    return feedback.body;
  } else {
    // Toast
    return null;
  }
}

// PASTE SAMPLE RESPONSE HERE
// [
//     9,
//     "Samsung Galaxy Note 10",
//     "RAM 64Gb,Storage 256GB",
//     117000,
//     "Smartphones",
//     "Samsung Galaxy Note 10.jpg"
// ]

Future getproducts() async {
  http.Response response = await http.get(Uri.parse('$baseurl/api/products'));
  if (response.statusCode == 200) {
    return jsonDecode(response.body);
  } else {
    return null;
  }
}

// PASTE SAMPLE RESPONSE HERE
//  [
//         1,
//         "Samsung A03",
//         "RAM 16GB, Storage 128GB",
//         32000,
//         "Smartphones",
//         "phone1.jpg"
//     ],
//     [
//         2,
//         "Oppo Reno 7",
//         "RAM 32GB,Storage 128GB",
//         21000,
//         "Smartphones",
//         "phone6.jpg"
//     ],

Future createProduct(Map product) async {
  try {
    http.Response response = await http.post(Uri.parse('$baseurl/api/create'),
        body: json.encode(product),
        headers: {'Content-Type': 'application/json'});
    if (response.statusCode == 200) {
      return jsonDecode(response.body);
      // Toast
    } else {}
  } catch (e) {
    return e;
  }
}


```

### TASK : Users
```dart

// Create Users
// username
// email
// phone
// password1
// password2

// ENDPOINT = /api/signup


// Login
// username
// password

//Endpoint = /api/login

```

### payments 
``` dart
import 'dart:convert';

import 'package:http/http.dart' as http;

import '../api/products.dart';

Future mpesa(double amount, String phone) async {
  http.Response response = await http.post(
      Uri.parse(
        '$baseurl/api/mpesa',
      ),
      body: json.encode({'amount': amount, 'phone': phone}),
      headers: {'Content-type': 'application/json'});
  if (response.statusCode == 200) {
    return json.decode(response.body);
  } else {
    return null;
  }
}
```

## User Interface

### \main.dart
```dart
import 'package:flutter/material.dart';
import 'package:flex_color_scheme/flex_color_scheme.dart';

import 'screens/products.dart';

void main() {
  runApp(MaterialApp(
    title: 'Leave App',
    debugShowCheckedModeBanner: false,    
    theme: FlexThemeData.light(scheme: FlexScheme.hippieBlue,),
    darkTheme: FlexThemeData.dark(scheme: FlexScheme.hippieBlue, darkIsTrueBlack: true),
    home:  const Products(),
  ));
}
```
### \auth\login

``` dart
// TASK
```

### \auth\register

``` dart
// TASK
```

### \screens\products

``` dart

import 'package:flutter/material.dart';
import 'package:soko/api/products.dart';

import '../controller/products.dart';
import 'create_product.dart';
import 'single_product.dart';

class Products extends StatefulWidget {
  const Products({super.key});

  @override
  State<Products> createState() => _ProductsState();
}

class _ProductsState extends State<Products> {
  @override
  void initState() {
    super.initState();
    getproducts();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Products"),
        actions: [
          IconButton(
              onPressed: () {
                Navigator.push(context,
                    MaterialPageRoute(builder: (_) => const Createproduct()));
              },
              icon: const Icon(Icons.edit_note)),
          IconButton(
              onPressed: () {
                initState();
              },
              icon: const Icon(Icons.refresh))
        ],
      ),
      body: FutureBuilder(
          future: getproducts(),
          builder: (context, snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              return Center(child: CircularProgressIndicator());
            } else if (snapshot.hasError) {
              return Text(snapshot.error.toString());
            } else {
              var data = snapshot.data;
              if (data == null) {
                return Text('No Products Found');
              } else {
                var products = data;
                return ListView.builder(
                    itemCount: products.length,
                    itemBuilder: (context, index) {
                      return ListTile(
                        onTap: () {
                          Navigator.push(
                              context,
                              MaterialPageRoute(
                                  builder: (context) => Oneproduct(
                                        product_id: products[index][0],
                                      )));
                        },
                        leading: SizedBox(
                            height: MediaQuery.of(context).size.height * 0.3,
                            child: Image.network(
                              "$baseurl/static/images/${products[index][5]}",
                              scale: 2,
                            )),
                        subtitle: Column(
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: [
                            Text('Product Name : ${products[index][1]}'),
                            Text(
                              'Product Description : ${products[index][2]}',
                              overflow: TextOverflow.visible,
                            ),
                            Text(
                                'Product Price : KSH ${products[index][3].toString()}'),
                          ],
                        ),
                      );
                    });
              }
            }
          }),
    );
  }
}


```

### \screens\single_product
``` dart
import 'package:flutter/material.dart';
import 'package:intl/intl.dart';
import 'package:soko/api/products.dart';

import '../controller/products.dart';

class Oneproduct extends StatefulWidget {
  const Oneproduct({super.key, required this.product_id});
  final int product_id;
  @override
  State<Oneproduct> createState() => _OneproductState();
}

class _OneproductState extends State<Oneproduct> {
  @override
  Widget build(BuildContext context) {
    // a future builder - widget that builds itself based on the latest snapshot of interaction with a future

    // 1. FUTURE - an object representing a potential value or error
    // 2. Snapshot - Represents the state of the future (connectionState, data,error)
    return Scaffold(
      appBar: AppBar(
        title: const Text('Shop'),
      ),
      body: FutureBuilder(
          future: fetchProductbyId(widget.product_id),
          builder: (BuildContext context, AsyncSnapshot snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              // show loadind
              return const CircularProgressIndicator();
            } else if (snapshot.hasError) {
              // show error
              return Text('Error ${snapshot.error.toString()}');
            } else {
              // show our data.
              if (snapshot.hasData) {
                var data = snapshot.data;
                // Buid our UI
                return Column(
                  children: [
                    Image.network(
                      '$baseurl/static/images/${data[5]}',
                      scale: 2.5,
                    ),
                    Text(data[1]),
                    Text(NumberFormat().format(data[3])),
                    Text(data[2]),
                    TextButton.icon(onPressed: () {
                      
                    }, label: const Text('Buy'))
                  ],
                );
              } else {
                return const Text('No Data');
              }
            }
          }),
    );
  }
}
```
### \screens\mpesa
``` dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

import 'products.dart';

class Input extends StatefulWidget {
  const Input({super.key});

  @override
  State<Input> createState() => _InputState();
}

class _InputState extends State<Input> {
  var amount = TextEditingController(text: '20');
  var phoneNumber = TextEditingController(text : '254757693623');
  var formKey = GlobalKey<FormState>();
  Future mpesa() async{
    try{
      var url = Uri.parse('https://soko.titus.co.ke/api/mpesa');
      var body = jsonEncode({
        'amount': amount.text,
        'phone': phoneNumber.text
      });
      var headers ={"Content-type":"application/json"};

      http.Response response = await http.post(url,body:body, headers:headers);
      if(response.statusCode == 200){
        if(mounted){
          ScaffoldMessenger.of(context).showSnackBar(const SnackBar(content: Text('Successful')));
        }
        else{}
      }

    }
    catch(e){
       if(mounted){
          ScaffoldMessenger.of(context).showSnackBar( SnackBar(content: Text(e.toString())));
        }
    
    }



  }




  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar:AppBar(
        title: const Text('Mpesa Transactions'),
        actions : [IconButton(onPressed: (){Navigator.push(context, MaterialPageRoute(builder: (_)=>const Products()));}, icon: const Icon(Icons.shop_outlined))]
        ),
        body: Form(
          key: formKey,

          child: Column(
            children: [
              Padding(
                padding: const EdgeInsets.all(16.0),
                child: TextFormField(
                  controller: amount,
                  decoration: const InputDecoration(
                    labelText: 'Amount',
                    border: OutlineInputBorder()
                  ),
                  keyboardType: TextInputType.number,
                  validator: (value){
                      if(value!.isEmpty || int.tryParse(value) == null){
                        return 'Please enter a valid amount';
                      }
                      else{
                        return null;
                      }
                  },
                ),
              ),

               Padding(
                 padding: const EdgeInsets.all(16.0),
                 child: TextFormField(
                    controller: phoneNumber,
                  decoration: const InputDecoration(
                    labelText: 'Phone number',
                    hintText: 'e.g 254736252191',
                    border: OutlineInputBorder()
                  ),
                  keyboardType: TextInputType.number,
                  validator: (value){
                    if(value!.isEmpty || int.tryParse(value) == null || value.length < 10){
                      return 'Please enter a valid phone number';
                    }
                    else{
                      return null;
                    }
                 
                  },
                 
                               ),
               ),

              ElevatedButton(onPressed: (){
                if(formKey.currentState!.validate()){
                  try{mpesa();}
                  catch(e){
                    if(mounted){
                      ScaffoldMessenger.of(context).showSnackBar( SnackBar(content: Text(e.toString())));
                    }else{}
                  }
                  
                }
                else{
                  ScaffoldMessenger.of(context).showSnackBar(const SnackBar(content: Text('Please check your fields')));
                }

              }, child: const Text('Make payment'))


             ]),
        
        )
    );
  }
}
```
