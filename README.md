<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RFID Book Catalog</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        #bookList {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 20px;
        }
        .bookCard {
            border: 1px solid #ccc;
            border-radius: 5px;
            padding: 10px;
            margin: 10px;
            width: 200px;
        }
        .bookTitle {
            font-weight: bold;
            margin-bottom: 5px;
        }
        .bookAuthor {
            font-style: italic;
            margin-bottom: 10px;
        }
        .bookInfo {
            font-size: 14px;
        }
        #addBookForm {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>RFID Book Catalog</h1>
    
    <!-- Add Book Form -->
    <form id="addBookForm">
        <h2>Add New Book</h2>
        <div>
            <label for="title">Title:</label>
            <input type="text" id="title" name="title" required>
        </div>
        <div>
            <label for="author">Author:</label>
            <input type="text" id="author" name="author" required>
        </div>
        <div>
            <label for="isbn">ISBN:</label>
            <input type="text" id="isbn" name="isbn" required>
        </div>
        <button type="submit">Add Book</button>
    </form>

    <!-- Book List -->
    <div id="bookList"></div>

    <script>
        // Dummy book catalog data (replace with actual data obtained from server)
        let bookCatalog = [
            { title: "Book 1", author: "Author A", isbn: "ISBN-1" },
            { title: "Book 2", author: "Author B", isbn: "ISBN-2" },
            { title: "Book 3", author: "Author C", isbn: "ISBN-3" }
        ];

        // Function to display book catalog
        function displayBookCatalog() {
            const bookListElem = document.getElementById("bookList");
            bookListElem.innerHTML = ""; // Clear previous content

            // Loop through each book in the catalog and create a book card
            bookCatalog.forEach(book => {
                const bookCard = document.createElement("div");
                bookCard.classList.add("bookCard");

                const titleElem = document.createElement("div");
                titleElem.classList.add("bookTitle");
                titleElem.textContent = book.title;

                const authorElem = document.createElement("div");
                authorElem.classList.add("bookAuthor");
                authorElem.textContent = book.author;

                const isbnElem = document.createElement("div");
                isbnElem.classList.add("bookInfo");
                isbnElem.textContent = "ISBN: " + book.isbn;

                bookCard.appendChild(titleElem);
                bookCard.appendChild(authorElem);
                bookCard.appendChild(isbnElem);

                bookListElem.appendChild(bookCard);
            });
        }

        // Function to handle form submission (add new book)
        function handleAddBook(event) {
            event.preventDefault(); // Prevent default form submission

            // Retrieve form input values
            const title = document.getElementById("title").value;
            const author = document.getElementById("author").value;
            const isbn = document.getElementById("isbn").value;

            // Validate input values
            if (title.trim() === '' || author.trim() === '' || isbn.trim() === '') {
                alert("Please provide all book details.");
                return;
            }

            // Create new book object
            const newBook = { title, author, isbn };

            // Add new book to the catalog
            bookCatalog.push(newBook);

            // Update the displayed book catalog
            displayBookCatalog();

            // Clear form input fields
            document.getElementById("title").value = "";
            document.getElementById("author").value = "";
            document.getElementById("isbn").value = "";
        }

        // Event listener for form submission
        const addBookForm = document.getElementById("addBookForm");
        addBookForm.addEventListener("submit", handleAddBook);

        // Call displayBookCatalog function when the page loads
        document.addEventListener("DOMContentLoaded", () => {
            displayBookCatalog();
        });
    </script>
</body>
</html>
