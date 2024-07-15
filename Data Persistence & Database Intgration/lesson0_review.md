# Review of Last Week's Class
**1. FutureBuilder:**
- **Purpose:** FutureBuilder is a widget that builds itself based on the latest snapshot of interaction with a Future.
- **Key Concepts:**
  - **Future:** Represents a potential value or error that will be available at some point in the future.
  - **FutureBuilder:** Takes a `Future` and a builder function.
  - **Snapshot:** Represents the state of the future; it can be uncompleted, completed with data, or completed with an error.
- **Example:**
  ```dart
  FutureBuilder(
    future: fetchProducts(),
    builder: (context, snapshot) {
      if (snapshot.connectionState == ConnectionState.waiting) {
        return CircularProgressIndicator();
      } else if (snapshot.hasError) {
        return Text('Error: ${snapshot.error}');
      } else {
        return ListView.builder(
          itemCount: snapshot.data.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text(snapshot.data[index][1]),
            );
          },
        );
      }
    },
  );
  ```
- **Usage:** Typically used for making asynchronous requests to APIs and displaying the result `once available `.

**2. GridView.builder:**
- **Purpose:** GridView.builder is used to create a scrollable 2D array of widgets.
- **Key Concepts:**
  - **ItemBuilder:** Provides a way to lazily build items based on an index.
  - **GridDelegate:** Controls the layout of the grid.
- **Example:**
  ```dart
  GridView.builder(
    gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
      crossAxisCount: 2,
    ),
    itemCount: products.length,
    itemBuilder: (context, index) {
      return Card(
        child: Column(
          children: [
            Image.network(products[index][5]),
            Text(products[index].name),
          ],
        ),
      );
    },
  );
  ```
- **Usage:** Ideal for displaying items in a grid format, such as product listings.

**3. Custom Widgets:**
- **Purpose:** To encapsulate reusable UI components.
- **Key Concepts:**
  - **StatelessWidget:** For widgets that don’t require mutable state.
  - **StatefulWidget:** For widgets that maintain state.
- **Example:**
  ```dart
  class ProductCard extends StatelessWidget {
    final Product product;

    ProductCard({required this.product});

    @override
    Widget build(BuildContext context) {
      return Card(
        child: Column(
          children: [
            Image.network(product.imageUrl),
            Text(product.name),
          ],
        ),
      );
    }
  }
  ```
- **Usage:** Custom widgets promote code reusability and maintainability.



### Introducing Alerts

**1. Purpose:** To notify users about important information or actions.
**2. Key Concepts:**
- **AlertDialog:** A material design alert dialog.
**3. Usage Example:**
  ```dart
  void _showAlert(BuildContext context) {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Alert'),
          content: Text('This is an alert message.'),
          actions: [
            TextButton(
              onPressed: () {
                Navigator.of(context).pop();
              },
              child: Text('OK'),
            ),
          ],
        );
      },
    );
  }
  ```

This lesson plan covers a comprehensive review and introduction to new concepts in Flutter, ensuring a smooth learning curve for your students.