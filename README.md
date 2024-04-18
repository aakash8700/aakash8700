<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Proof of Existence DApp</title>
</head>
<body>
    <h1>Proof of Existence DApp</h1>
    <input type="file" id="fileInput">
    <button onclick="timestampDocument()">Timestamp Document</button>
    <div id="output"></div>

    <script>
        async function timestampDocument() {
            const fileInput = document.getElementById('fileInput');
            const file = fileInput.files[0];
            const fileReader = new FileReader();
            fileReader.onload = async function(event) {
                const documentBytes = new Uint8Array(event.target.result);
                const documentHash = await hashDocument(documentBytes);
                const timestamp = await getTimestamp(documentHash);
                document.getElementById('output').innerText = `Document timestamped at: ${new Date(timestamp * 1000).toLocaleString()}`;
            };
            fileReader.readAsArrayBuffer(file);
        }

        async function hashDocument(documentBytes) {
            const buffer = await crypto.subtle.digest('SHA-256', documentBytes);
            return Array.from(new Uint8Array(buffer)).map(b => b.toString(16).padStart(2, '0')).join('');
        }

        async function getTimestamp(documentHash) {
            // Call the smart contract method to get the timestamp
            // Implement web3.js or ethers.js to interact with the contract
            // Example: const timestamp = await contractInstance.getTimestamp(documentHash);
            // Replace contractInstance with your actual contract instance
            return 0; // Replace this with actual timestamp
        }
    </script>
</body>
</html>

