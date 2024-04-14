<!DOCTYPE html>
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
        <label for="barcode">Scan Barcode:</label>
        <input type="text" id="barcode" name="barcode" placeholder="Enter ISBN...">
        <button onclick="fetchBookInfo()">Fetch Info</button>
    </div>
    <div id="bookInfo">
        <!-- Book information will be displayed here -->
    </div>

    <script>
        function fetchBookInfo() {
            var isbn = document.getElementById('barcode').value;
            var apiUrl = 'https://openlibrary.org/api/books?bibkeys=ISBN:' + isbn + '&format=json&jscmd=data';

            $.getJSON(apiUrl, function(data) {
                if ($.isEmptyObject(data)) {
                    $('#bookInfo').html('<p>No information found for the ISBN: ' + isbn + '</p>');
                } else {
                    var bookData = data['ISBN:' + isbn];
                    var title = bookData.title;
                    var authors = bookData.authors.map(author => author.name).join(', ');
                    var publishDate = bookData.publish_date;
                    var publisher = bookData.publishers[0].name;

                    var bookInfoHTML = '<h2>' + title + '</h2>';
                    bookInfoHTML += '<p>Author(s): ' + authors + '</p>';
                    bookInfoHTML += '<p>Publish Date: ' + publishDate + '</p>';
                    bookInfoHTML += '<p>Publisher: ' + publisher + '</p>';

                    $('#bookInfo').html(bookInfoHTML);
                }
            });
        }
    </script>
</body>
</html>

