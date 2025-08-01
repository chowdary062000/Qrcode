
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Language Selection with QR Code</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-color: #f8f9fa;
            font-family: Arial, sans-serif;
            color: #343a40;
        }

        .flag-icon {
            width: 30px;
            height: auto;
            margin-right: 8px;
        }

        .lang-option {
            display: flex;
            align-items: center;
            cursor: pointer;
            padding: 10px;
            border: 1px solid #ced4da;
            border-radius: 8px;
            margin: 8px;
            transition: background-color 0.2s;
        }

        .lang-option:hover {
            background-color: #e2e6ea;
        }

        .qr-code-box {
            display: none;
            justify-content: center;
            padding: 20px;
        }

        .qr-visible {
            display: flex !important;
        }
    </style>
</head>

<body>
    <div class="container py-4">
        <h2 class="text-center mb-4">Available Languages</h2>

        <div class="row justify-content-center" id="languageList">
            <!-- Language Options -->
            <div class="col-md-4 lang-option" data-url="https://drive.google.com/file/d/1jJqBRfajwuGQFZpAkhx33cykk8q59q5a/view?usp=drivesdk">
                <img src="https://twj.mohre.gov.ae/images/icons/English.png" class="flag-icon" alt="English"> English
            </div>
            <div class="col-md-4 lang-option" data-url="https://example.com/es">
                <img src="https://twj.mohre.gov.ae/images/icons/Spanish.png" class="flag-icon" alt="Spanish"> Spanish
            </div>
            <div class="col-md-4 lang-option" data-url="https://example.com/fr">
                <img src="https://twj.mohre.gov.ae/images/icons/French.png" class="flag-icon" alt="French"> French
            </div>
            <div class="col-md-4 lang-option" data-url="https://example.com/de">
                <img src="https://twj.mohre.gov.ae/images/icons/German.png" class="flag-icon" alt="German"> German
            </div>
            <div class="col-md-4 lang-option" data-url="https://example.com/ar">
                <img src="https://twj.mohre.gov.ae/images/icons/Arabic.png" class="flag-icon" alt="Arabic"> Arabic
            </div>
            <div class="col-md-4 lang-option" data-url="https://example.com/zh">
                <img src="https://twj.mohre.gov.ae/images/icons/Chinese.png" class="flag-icon" alt="Chinese"> Chinese
            </div>
            <!-- Add more language options as needed -->
        </div>

        <div class="qr-code-box" id="qrSection">
            <div class="text-center">
                <h4>Scan to View/Download</h4>
                <a id="qrLinkAnchor" href="#" target="_blank">
                    <img id="dynamicQRCode" src="" alt="QR Code" />
                </a>
                <p class="mt-2">URL: <span id="qrLinkText" class="text-primary"></span></p>
                <div class="mt-3">
                    <button class="btn btn-primary me-2" id="viewLinkBtn">View Document</button>
                    <button class="btn btn-secondary" id="copyLinkBtn">Copy Link</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
    <script>
        $(document).ready(function () {
            $('.lang-option').on('click', function () {
                const url = $(this).data('url');
                const qrApiUrl = `https://api.qrserver.com/v1/create-qr-code/?data=${encodeURIComponent(url)}&size=300x300`;

                $('#dynamicQRCode').attr('src', qrApiUrl);
                $('#qrLinkAnchor').attr('href', url);
                $('#qrLinkText').text(url);
                $('#qrSection').addClass('qr-visible');

                // Store link for buttons
                $('#viewLinkBtn').off('click').on('click', () => window.open(url, '_blank'));
                $('#copyLinkBtn').off('click').on('click', () => {
                    navigator.clipboard.writeText(url)
                        .then(() => alert('Link copied to clipboard!'))
                        .catch(err => console.error('Could not copy text:', err));
                });
            });
        });
    </script>
</body>

</html>
