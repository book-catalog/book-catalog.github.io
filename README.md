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
    </style>
</head>
<body>
    <h1>RFID Book Catalog</h1>
    <div id="bookList"></div>

    <script>
        // Dummy book catalog data (replace with actual data obtained from server)
        const bookCatalog = [
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

        // Call displayBookCatalog function when the page loads
        document.addEventListener("DOMContentLoaded", () => {
            displayBookCatalog();
        });
    </script>
</body>
</html>
