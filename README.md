index.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Stock Finder</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div class="container">
      <h1>Stock Finder</h1>
      <input type="text" id="searchInput" placeholder="Search stocks..." />
      <ul id="stockList"></ul>
    </div>

    <script src="script.js"></script>
  </body>
</html>


---

style.css

body {
  font-family: Arial, sans-serif;
  background-color: #f6f8fa;
  margin: 0;
  padding: 20px;
}

.container {
  max-width: 500px;
  margin: auto;
  background: white;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
}

#searchInput {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  font-size: 16px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

#stockList {
  list-style-type: none;
  padding: 0;
}

#stockList li {
  padding: 10px;
  border-bottom: 1px solid #eee;
  font-size: 16px;
}


---

script.js

const apiUrl = "https://stock-finder-backend-hosted-url.com/api/stocks"; // replace with actual backend URL

const searchInput = document.getElementById("searchInput");
const stockList = document.getElementById("stockList");

async function fetchStocks() {
  try {
    const res = await fetch(apiUrl);
    const data = await res.json();
    renderList(data);
  } catch (error) {
    stockList.innerHTML = "<li>Error fetching stocks.</li>";
  }
}

function renderList(stocks) {
  stockList.innerHTML = "";
  stocks.forEach((stock) => {
    const li = document.createElement("li");
    li.textContent = stock;
    stockList.appendChild(li);
  });
}

searchInput.addEventListener("input", () => {
  const filter = searchInput.value.toUpperCase();
  const items = stockList.getElementsByTagName("li");
  for (let i = 0; i < items.length; i++) {
    const txtValue = items[i].textContent || items[i].innerText;
    items[i].style.display = txtValue.toUpperCase().indexOf(filter) > -1 ? "" : "none";
  }
});

fetchStocks