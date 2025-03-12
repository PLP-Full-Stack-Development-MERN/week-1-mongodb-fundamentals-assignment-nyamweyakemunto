1. **Setup MongoDB:**

   - Install MongoDB locally or create a free cluster on MongoDB Atlas.
   - Start the MongoDB server locally or connect to the MongoDB Atlas cluster.
   - Verify the installation and connection by running:
   ```sh
     mongo --version
     ```

2. **Database and Collection Creation:**

   - Create a new database called `library`.

        use library;


   - Inside `library`, create a collection named `books`.

            db.createCollection("books");



3. **Insert Data:**

   - Insert at least five book records into the `books` collection.
   - Each book should contain fields such as `title`, `author`, `publishedYear`, `genre`, and `ISBN`.

               db.books.insertMany([
            {
                title: "The Hobbit",
                author: "J.R.R. Tolkien",
                publishedYear: 2007,
                genre: "Fantasy",
                ISBN: "9780261103283"
            },
            {
                title: "Harry Potter and the Sorcerer's Stone",
                author: "J.K. Rowling",
                publishedYear: 1997,
                genre: "Fantasy",
                ISBN: "9780439708180"
            },
            {
                title: "To Kill a Mockingbird",
                author: "Harper Lee",
                publishedYear: 2015,
                genre: "Fiction",
                ISBN: "9780061120084"
            },
            {
                title: "1984",
                author: "George Orwell",
                publishedYear: 1949,
                genre: "Dystopian",
                ISBN: "9780451524935"
            },
            {
                title: "The Great Gatsby",
                author: "F. Scott Fitzgerald",
                publishedYear: 2000,
                genre: "Classic",
                ISBN: "9780743273565"
            }
            ]);



4. **Retrieve Data:**

   - Retrieve all books from the collection.

            db.books.find();


   - Query books based on a specific author.

            db.books.find( {author: "Harper Lee"} );


   - Find books published after the year 2000.

            db.books.find( {publishedYear : {$gt: 2000} });

5. **Update Data:**

   - Update the `publishedYear` of a specific book.

            db.books.updateOne(
            { title: "1984" },
            { $set: { publishedYear: 1950 } }
            );

   - Add a new field called `rating` to all books and set a default value.

            db.books.updateMany(
            {}, { $set: { rating: 5 } }
            );

6. **Delete Data:**

   - Delete a book by its `ISBN`.

            db.books.deleteOne({ ISBN: "9780451524935" }); 

   - Remove all books of a particular genre.

            db.books.deleteMany({ genre: "Fantasy" }); 

7. **Data Modeling Exercise:**

   - Create a data model for an e-commerce platform including collections for `users`, `orders`, and `products`.
   - Decide on appropriate fields and relationships (embedding vs. referencing).
   - Implement the structure using MongoDB.

            db.createCollection("users");
            db.createCollection("orders");
            db.createCollection("products");

            db.users.insertOne({ name: "Alice", email: "alice@example.com" });
            db.products.insertOne({ name: "Laptop", price: 1000 });
            db.orders.insertOne({ userId: "1", productId: "1", quantity: 2 });

8. **Aggregation Pipeline:**

   - Use aggregation to find the total number of books per genre.

            db.books.aggregate([
            { $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
            ]); 

   - Calculate the average published year of all books.

            db.books.aggregate([
            { $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } }
            ]); 

   - Identify the top-rated book.

            db.books.aggregate([
            { $sort: { rating: -1 } },
            { $limit: 1 }
            ]);

9. **Indexing:**

   - Create an index on the `author` field to optimize query performance.

            db.books.createIndex({ author: 1 }); // Create an index on the author field

   - Explain the benefits of indexing in MongoDB.

            indexing enables mongoDB to run faster reducing time it takes to query data hence improving the performance in general.
