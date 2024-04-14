<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Book Information</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <h1>Book Information</h1>
    <div>
        <label for="isbn">Enter ISBN:</label>
        <input type="text" id="isbn" name="isbn" placeholder="Enter ISBN...">
        <button onclick="fetchBookInfo()">Fetch Info</button>
    </div>
    <div id="bookInfo">
        <!-- Book information will be displayed here -->
    </div>

    <h2>Add a New Book</h2>
    <div>
        <label for="title">Title:</label>
        <input type="text" id="title" name="title" placeholder="Enter title...">
    </div>
    <div>
        <label for="author">Author:</label>
        <input type="text" id="author" name="author" placeholder="Enter author...">
    </div>
    <div>
        <label for="publishDate">Publish Date:</label>
        <input type="text" id="publishDate" name="publishDate" placeholder="Enter publish date...">
    </div>
    <div>
        <label for="publisher">Publisher:</label>
        <input type="text" id="publisher" name="publisher" placeholder="Enter publisher...">
        <button onclick="addBook()">Add Book</button>
    </div>
    <div id="addedBooks">
        <!-- Added books will be displayed here -->
    </div>

    <script>
        function fetchBookInfo() {
            var isbn = document.getElementById('isbn').value;
            var apiUrl = 'https://openlibrary.org/api/books?bibkeys=ISBN:' + isbn + '&format=json&jscmd=data';

            $.getJSON(apiUrl, function(data) {
                if ($.isEmptyObject(data)) {
                    $('#bookInfo').html('<p>No information found for the ISBN: ' + isbn + '</p>');
                } else {
                    var bookData = data['ISBN:' + isbn];
                    var title = bookData.title;
                    var authors = bookData.authors ? bookData.authors.map(author => author.name).join(', ') : 'Unknown';
                    var publishDate = bookData.publish_date ? bookData.publish_date : 'Unknown';
                    var publisher = bookData.publishers ? bookData.publishers[0].name : 'Unknown';

                    var bookInfoHTML = '<h2>' + title + '</h2>';
                    bookInfoHTML += '<p>Author(s): ' + authors + '</p>';
                    bookInfoHTML += '<p>Publish Date: ' + publishDate + '</p>';
                    bookInfoHTML += '<p>Publisher: ' + publisher + '</p>';

                    $('#bookInfo').html(bookInfoHTML);
                }
            });
        }

        function addBook() {
            var title = document.getElementById('title').value;
            var author = document.getElementById('author').value;
            var publishDate = document.getElementById('publishDate').value;
            var publisher = document.getElementById('publisher').value;

            var bookHTML = '<h2>' + title + '</h2>';
            bookHTML += '<p>Author(s): ' + author + '</p>';
            bookHTML += '<p>Publish Date: ' + publishDate + '</p>';
            bookHTML += '<p>Publisher: ' + publisher + '</p>';

            $('#addedBooks').append(bookHTML);
        }
    </script>
</body>
</html>
