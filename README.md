# book-catalog.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Book Catalog with Barcode</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Book Catalog with Barcode</h1>
    </header>

    <section id="catalog">
        <h2>Book Catalog</h2>
        <div id="bookList">
            <!-- Books will be dynamically added here -->
        </div>
        <button onclick="scanBarcode()">Scan Barcode</button>
    </section>

    <footer>
        <p>&copy; 2024 Book Catalog. All rights reserved.</p>
    </footer>

    <script src="https://cdn.jsdelivr.net/npm/@zxing/library@latest"></script>
    <script>
        async function scanBarcode() {
            const codeReader = new ZXing.BrowserBarcodeReader();
            try {
                const result = await codeReader.decodeFromVideoDevice(undefined, 'video');
                const bookCode = result.text;
                fetchBookDetails(bookCode);
            } catch (error) {
                console.error(error);
            }
        }

        async function fetchBookDetails(bookCode) {
            const apiUrl = `https://openlibrary.org/api/books?bibkeys=ISBN:${bookCode}&format=json&jscmd=data`;
            try {
                const response = await fetch(apiUrl);
                const data = await response.json();
                const bookDetails = data[`ISBN:${bookCode}`];
                displayBookDetails(bookDetails);
            } catch (error) {
                console.error('Error fetching book details:', error);
            }
        }

        function displayBookDetails(bookDetails) {
            const bookList = document.getElementById('bookList');
            const bookElement = document.createElement('div');
            bookElement.innerHTML = `
                <h3>${bookDetails.title}</h3>
                <p>Author: ${bookDetails.authors[0].name}</p>
                <p>Publish Date: ${bookDetails.publish_date}</p>
                <p>Publisher: ${bookDetails.publishers[0].name}</p>
            `;
            bookList.appendChild(bookElement);
        }
    </script>
</body>
</html>
