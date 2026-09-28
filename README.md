# dabhade-super-market
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Dabhade Super Market Billing</title>

    <link rel="stylesheet" href="style.css">
</head>

<body>

<div class="container">

    <!-- HEADER -->
    <div class="header">
        <h1>Dabhade Super Market</h1>
        <p>Karjat, Nana Master Nagar</p>
        <p>Super Market Bill</p>
    </div>

    <!-- BILL NUMBER -->
    <div class="bill-number">
        Bill No:
        <span id="billNumber"></span>
    </div>

    <!-- CUSTOMER -->
    <div class="customer">

        <input
            type="text"
            id="customerName"
            placeholder="Customer Name"
        >

        <input
            type="text"
            id="customerMobile"
            placeholder="Mobile Number"
        >

    </div>

    <!-- BARCODE SCANNER -->
    <div class="scanner-box">

        <h3>🔎 Barcode Scanner</h3>

        <div class="scanner-input">

            <input
                type="text"
                id="barcodeInput"
                placeholder="Scan barcode here..."
                autofocus
            >

            <button
                class="scan-btn"
                onclick="scanBarcode()">
                Add Barcode
            </button>

            <button
                class="camera-btn"
                onclick="startCamera()">
                📷 Camera
            </button>

        </div>

        <!-- CAMERA -->
        <div id="cameraArea">

            <video
                id="video"
                autoplay
                playsinline>
            </video>

            <br>

            <button
                class="close-camera"
                onclick="stopCamera()">
                Close Camera
            </button>

        </div>

    </div>

    <!-- MANUAL ITEM -->
    <div class="item-input">

        <input
            type="text"
            id="itemName"
            placeholder="Item Name"
        >

        <input
            type="number"
            id="quantity"
            placeholder="Quantity"
            min="1"
            value="1"
        >

        <input
            type="number"
            id="price"
            placeholder="Price"
            min="0"
            step="0.01"
        >

        <button
            class="add-btn"
            onclick="addManualItem()">
            Add Item
        </button>

    </div>

    <!-- BILL TABLE -->
    <table>

        <thead>
            <tr>

                <th>Sr. No.</th>
                <th>Barcode</th>
                <th>Item</th>
                <th>Quantity</th>
                <th>Price</th>
                <th>Amount</th>

                <th class="delete-column">
                    Action
                </th>

            </tr>
        </thead>

        <tbody id="billBody"></tbody>

    </table>

    <!-- TOTAL -->
    <div class="total-section">

        <p>
            Total Items:
            <span id="totalItems">0</span>
        </p>

        <p>
            Total Quantity:
            <span id="totalQuantity">0</span>
        </p>

        <p class="grand-total">
            Grand Total:
            ₹<span id="grandTotal">0.00</span>
        </p>

    </div>

    <!-- BUTTONS -->
    <div class="buttons">

        <button
            class="print-btn"
            onclick="printBill()">
            🖨️ Print Bill
        </button>

        <button
            class="new-btn"
            onclick="newBill()">
            ➕ New Customer Bill
        </button>

    </div>

</div>

<script src="script.js"></script>

</body>
</html>
* {
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: #f2f2f2;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 950px;
    margin: auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px #bbb;
}

/* HEADER */

.header {
    text-align: center;
    border-bottom: 2px solid black;
    padding-bottom: 15px;
    margin-bottom: 15px;
}

.header h1 {
    margin: 0;
    font-size: 30px;
}

.header p {
    margin: 5px;
}

/* BILL NUMBER */

.bill-number {
    text-align: right;
    margin-bottom: 15px;
    font-weight: bold;
}

/* CUSTOMER */

.customer {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.customer input {
    flex: 1;
    padding: 10px;
    border: 1px solid #aaa;
    border-radius: 5px;
}

/* SCANNER */

.scanner-box {
    background: #f7f7f7;
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 8px;
    margin-bottom: 20px;
}

.scanner-box h3 {
    margin-top: 0;
}

.scanner-input {
    display: flex;
    gap: 10px;
}

.scanner-input input {
    flex: 1;
    padding: 12px;
    font-size: 17px;
}

.scan-btn {
    background: #198754;
    color: white;
}

.camera-btn {
    background: #6f42c1;
    color: white;
}

/* MANUAL ITEM */

.item-input {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr auto;
    gap: 10px;
    margin-bottom: 20px;
}

.item-input input {
    padding: 10px;
    font-size: 15px;
}

/* BUTTONS */

button {
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 15px;
}

.add-btn {
    background: #198754;
    color: white;
}

.print-btn {
    background: #0d6efd;
    color: white;
}

.new-btn {
    background: #6c757d;
    color: white;
}

.delete-btn {
    background: #dc3545;
    color: white;
}

.close-camera {
    background: #dc3545;
    color: white;
    margin-top: 10px;
}

/* TABLE */

table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
}

th,
td {
    border: 1px solid #333;
    padding: 10px;
    text-align: center;
}

th {
    background: #eee;
}

/* TOTAL */

.total-section {
    margin-top: 20px;
    text-align: right;
}

.total-section p {
    margin: 8px;
}

.grand-total {
    font-size: 24px;
    font-weight: bold;
}

/* BUTTON AREA */

.buttons {
    margin-top: 20px;
    display: flex;
    gap: 10px;
    justify-content: center;
}

/* CAMERA */

#cameraArea {
    display: none;
    margin-top: 15px;
    text-align: center;
}

#video {
    width: 100%;
    max-width: 450px;
    border: 2px solid black;
    border-radius: 8px;
}

/* MOBILE */

@media(max-width:700px) {

    .item-input {
        grid-template-columns: 1fr;
    }

    .customer {
        flex-direction: column;
    }

    .scanner-input {
        flex-direction: column;
    }

    table {
        font-size: 13px;
    }

}

/* PRINT */

@media print {

    body {
        background: white;
        padding: 0;
    }

    .container {
        width: 100%;
        max-width: 100%;
        box-shadow: none;
    }

    .scanner-box,
    .item-input,
    .customer,
    .buttons,
    .delete-column {
        display: none !important;
    }

}
/* =====================================================
   PRODUCT DATABASE
===================================================== */

const products = {

    "89012345678901": {
        name: "Rice 1 KG",
        price: 55
    },

    "89012345678902": {
        name: "Rice 2 KG",
        price: 110
    },

    "89012345678903": {
        name: "Rice 3 KG",
        price: 165
    },

    "89012345678911": {
        name: "Sugar 1 KG",
        price: 48
    },

    "89012345678912": {
        name: "Sugar 2 KG",
        price: 96
    },

    "89012345678913": {
        name: "Sugar 3 KG",
        price: 144
    },

    "8901234567892": {
        name: "Sunflower Oil 1 L",
        price: 145
    },

    "8901234567893": {
        name: "Wheat Flour 5 KG",
        price: 280
    },

    "8901234567894": {
        name: "Tea 250 GM",
        price: 120
    },

    "8901234567895": {
        name: "Salt 1 KG",
        price: 25
    }

};


/* =====================================================
   BILL ARRAY
===================================================== */

let billItems = [];


/* =====================================================
   BILL NUMBER
===================================================== */

let billNumber =
    localStorage.getItem("billNumber") || 1;

document.getElementById("billNumber").innerText =
    String(billNumber).padStart(4, "0");


/* =====================================================
   BARCODE SCANNER
===================================================== */

function scanBarcode() {

    let barcode =
        document
        .getElementById("barcodeInput")
        .value
        .trim();


    if (barcode === "") {

        alert("Please scan or enter barcode.");

        return;

    }


    let product = products[barcode];


    if (!product) {

        alert(
            "Product not found!\n\n" +
            "Barcode: " + barcode +
            "\n\nPlease add this barcode to the product database."
        );

        return;

    }


    /* CHECK EXISTING PRODUCT */

    let existing =
        billItems.find(
            item => item.barcode === barcode
        );


    if (existing) {

        existing.quantity++;

        existing.amount =
            existing.quantity * existing.price;

    }

    else {

        billItems.push({

            barcode: barcode,

            item: product.name,

            quantity: 1,

            price: product.price,

            amount: product.price

        });

    }


    displayBill();


    document
        .getElementById("barcodeInput")
        .value = "";

    document
        .getElementById("barcodeInput")
        .focus();

}


/* =====================================================
   MANUAL ITEM
===================================================== */

function addManualItem() {

    let itemName =
        document
        .getElementById("itemName")
        .value
        .trim();


    let quantity =
        parseFloat(
            document
            .getElementById("quantity")
            .value
        );


    let price =
        parseFloat(
            document
            .getElementById("price")
            .value
        );


    if (itemName === "") {

        alert("Please enter item name.");

        return;

    }


    if (!quantity || quantity <= 0) {

        alert("Please enter valid quantity.");

        return;

    }


    if (isNaN(price) || price < 0) {

        alert("Please enter valid price.");

        return;

    }


    billItems.push({

        barcode: "-",

        item: itemName,

        quantity: quantity,

        price: price,

        amount: quantity * price

    });


    displayBill();


    /* CLEAR INPUTS */

    document
        .getElementById("itemName")
        .value = "";

    document
        .getElementById("quantity")
        .value = 1;

    document
        .getElementById("price")
        .value = "";

    document
        .getElementById("itemName")
        .focus();

}


/* =====================================================
   DISPLAY BILL
===================================================== */

function displayBill() {

    let tbody =
        document.getElementById("billBody");

    tbody.innerHTML = "";


    let total = 0;

    let totalQuantity = 0;


    billItems.forEach(function(item, index) {

        total += item.amount;

        totalQuantity += item.quantity;


        let row =
            document.createElement("tr");


        row.innerHTML = `

            <td>${index + 1}</td>

            <td>${item.barcode}</td>

            <td>${item.item}</td>

            <td>${item.quantity}</td>

            <td>₹${item.price.toFixed(2)}</td>

            <td>₹${item.amount.toFixed(2)}</td>

            <td class="delete-column">

                <button
                    class="delete-btn"
                    onclick="deleteItem(${index})">

                    Delete

                </button>

            </td>

        `;


        tbody.appendChild(row);

    });


    document.getElementById("totalItems").innerText =
        billItems.length;


    document.getElementById("totalQuantity").innerText =
        totalQuantity;


    document.getElementById("grandTotal").innerText =
        total.toFixed(2);

}


/* =====================================================
   DELETE ITEM
===================================================== */

function deleteItem(index) {

    billItems.splice(index, 1);

    displayBill();

}


/* =====================================================
   PRINT BILL
===================================================== */

function printBill() {

    if (billItems.length === 0) {

        alert("Please add at least one item.");

        return;

    }


    window.print();


    

}


/* =====================================================
   NEW BILL
===================================================== */

function newBill() {

    billItems = [];


    document.getElementById("customerName").value = "";

    document.getElementById("customerMobile").value = "";

    document.getElementById("itemName").value = "";

    document.getElementById("quantity").value = 1;

    document.getElementById("price").value = "";

    document.getElementById("barcodeInput").value = "";


    displayBill();


    /* INCREASE BILL NUMBER */

    billNumber++;


    localStorage.setItem(
        "billNumber",
        billNumber
    );


    document.getElementById("billNumber").innerText =
        String(billNumber).padStart(4, "0");


    document
        .getElementById("barcodeInput")
        .focus();

}


/* =====================================================
   ENTER KEY - BARCODE
===================================================== */

document
.getElementById("barcodeInput")
.addEventListener(
    "keydown",
    function(event) {

        if (event.key === "Enter") {

            scanBarcode();

        }

    }
);


/* =====================================================
   ENTER KEY - MANUAL ITEM
===================================================== */

document.addEventListener(
    "keydown",
    function(event) {

        let active =
            document.activeElement.id;


        if (
            event.key === "Enter" &&
            (
                active === "itemName" ||
                active === "quantity" ||
                active === "price"
            )
        ) {

            addManualItem();

        }

    }
);


/* =====================================================
   CAMERA BARCODE SCANNER
===================================================== */

let videoStream = null;

let cameraScanning = false;


/* START CAMERA */

async function startCamera() {

    const cameraArea =
        document.getElementById("cameraArea");

    const video =
        document.getElementById("video");


    if (!("BarcodeDetector" in window)) {

        alert(
            "Camera barcode scanning is not supported by this browser.\n\n" +
            "You can still use a USB/Bluetooth barcode scanner."
        );

        return;

    }


    try {

        videoStream =
            await navigator.mediaDevices.getUserMedia({

                video: {
                    facingMode: "environment"
                }

            });


        video.srcObject = videoStream;

        cameraArea.style.display = "block";

        cameraScanning = true;


        scanCameraBarcode();

    }

    catch (error) {

        alert(
            "Camera permission was denied or camera is unavailable."
        );

    }

}


/* CAMERA SCAN */

async function scanCameraBarcode() {

    if (!cameraScanning) {

        return;

    }


    const video =
        document.getElementById("video");


    const detector =
        new BarcodeDetector({

            formats: [
                "ean_13",
                "ean_8",
                "upc_a",
                "upc_e",
                "code_128"
            ]

        });


    try {

        const barcodes =
            await detector.detect(video);


        if (barcodes.length > 0) {

            document
                .getElementById("barcodeInput")
                .value =
                barcodes[0].rawValue;


            scanBarcode();

        }

    }

    catch (error) {

        console.log(error);

    }


    if (cameraScanning) {

        requestAnimationFrame(
            scanCameraBarcode
        );

    }

}


/* =====================================================
   STOP CAMERA
===================================================== */

function stopCamera() {

    cameraScanning = false;


    if (videoStream) {

        videoStream
            .getTracks()
            .forEach(
                track => track.stop()
            );

        videoStream = null;

    }


    document
        .getElementById("cameraArea")
        .style.display = "none";

}