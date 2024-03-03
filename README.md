# searchfilter
This search filter  design was  designed via pure vanilla Javascript, HTML AND CSS only 

HTML (index.html)
html
Copy code
<!DOCTYPE html>  
<html lang="en">  
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="C:\Users\user\Desktop\Search filter option\styles.css">
</head>
<body>
    <div class="content">
        <div class="heading">MR KIKSY MENU DESIGN</div>
        <div class="cateogaries">
            <a class="ctitle all">All</a>
        </div>
        <div class="container">
            <div class="items">
                <div class="img-conatiner"><img src="https://wallpapercave.com/wp/wp3151363.jpg"
                    alt="Burger" class="img"></div>
                <div class="details">
                    <div class="title">burger</div>
                    <div class="price">$4</div>
                </div>
                <div class="cateogary">FAST FOOD</div>
            </div>
            <div class="items">
                <div class="img-conatiner"><img src="https://static.toiimg.com/thumb/73514385.cms?imgsize=1468833&width=800&height=800"
                    alt="Burger" class="img"></div>
                <div class="details">
                    <div class="title">burger</div>
                    <div class="price">$4</div>
                </div>
                <div class="cateogary">FAST FOOD</div>
            </div>
        </div>
    </div>
    <script src="C:\Users\user\Desktop\Search filter option\index.js"></script>
</body>
</html>
CSS (styles.css)
css
Copy code
* {
    margin: 0;
    padding: 0;
}

.content {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.heading {
    font-size: 40px;
    font-weight: 800;
    margin: 60px auto;
}

.cateogaries {
    display: flex;
    flex-wrap: wrap;
}

.ctitle:active {
    background-color: rgba(255, 0, 0, 0.9);
}

.cateogaries .ctitle {
    margin: 10px;
    border: 2px solid red;
    padding: 10px 25px;
    border-radius: 8px;
}

a {
    text-decoration: none;
    color: black;
}

.container {
    display: flex;
    flex-wrap: wrap;
    width: 80%;
    justify-content: center;
    margin: 20px;
}

.items {
    width: 200px;
    height: 300px;
    display: flex;
    border: 2px solid red;
    padding: 4px;
    border-radius: 10px;
    margin: 20px;
    flex-direction: column;
}

.img {
    width: 200px;
    height: 200px;
}

.title {
    font-size: 20px;
}

.cateogary {
    text-align: center;
    margin: 10px 0px;
}

.details {
    display: flex;
    justify-content: space-between;
    width: 100%;
}

.items:hover {
    background-color: red;
    color: white;
    transition-duration: 0.7s;
    box-shadow: 8px 8px 10px rgba(255, 0, 0, 0.4);
    transform: translate(-8px, -8px);
}

.items:hover .img {
    transform: scale(1.2);
    transition-duration: 1s;
}

.img-conatiner {
    height: 200px;
    width: 200px;
    overflow: hidden;
}

.cateogaries .ctitle:hover {
    transform: translate(3px, -5px);
    transition-duration: 0.7s;
    box-shadow: 5px 5px 10px rgba(255, 0, 0, 0.5);
}
Explanation:

HTML Structure:

<!DOCTYPE html>: Declaration of the HTML version.
<html lang="en">: HTML document root with the language attribute set to English.
<head>: Contains metadata, links to stylesheets, and the document title.
<body>: Main content of the HTML document.
The content is organized into a container with a heading, categories, and items with details.
CSS Explanation:

*: Applies margin and padding reset for all elements.
.content: Styles for the main content container with flex display.
.heading: Styles for the heading with a large font size and margin.
.cateogaries: Styles for the categories container with flex display.
.ctitle:active: Styles for the active state of category titles.
.cateogaries .ctitle: Styles for category titles with margin, border, padding, and border-radius.
a: Styles for anchor tags with no text decoration and black color.
.container: Styles for the container of items with flex display and centered alignment.
.items: Styles for individual items with width, height, border, padding, and border-radius.
.img: Styles for images inside items with width and height.
.title: Styles for item titles with a specified font size.
.cateogary: Styles for the category text with text-align and margin.
.details: Styles for the details section of items with flex display and space-between.
Hover effects are applied to items, changing background color, text color, box-shadow, and transforming position and scale.
.img-conatiner: Styles for the container of images with specified height, width, and overflow.
.cateogaries .ctitle:hover: Hover effect for category titles with translation, transition, and box-shadow.

javascript
Copy code
// Creating an array of food items with their details
const food = [
    {
        id: 1,
        name: "BURGER",
        img: "https://wallpapercave.com/wp/wp3151363.jpg",
        price: 3,
        cateogary: "FASTFOOD",
    },
    // ... (other food items)
];

// Selecting elements from the HTML document
const cateogaries = document.querySelector(".cateogaries");
const container = document.querySelector(".container");

// Event listener to execute the function when the DOM content is loaded
window.addEventListener("DOMContentLoaded", function () {
    // Initial call to filterMenu with the argument "ALL"
    filterMenu("ALL");

    // Extracting unique categories from the food array
    var cat = food.reduce(function (values, items) {
        if (!values.includes(items.cateogary)) {
            values.push(items.cateogary);
        }
        return values;
    }, ["ALL"]);

    // Generating HTML for category buttons
    var catBtn = cat.map(function (item) {
        return `<a href="#" class="ctitle ${item}">${item}</a>`;
    });

    // Joining the HTML for category buttons and injecting it into the cateogaries element
    var catBtns = catBtn.join("");
    cateogaries.innerHTML = catBtns;

    // Adding click event listeners to each category button
    var button = document.getElementsByClassName("ctitle");
    for (var i = 0; i < button.length; i++) {
        button[i].addEventListener("click", (e) => {
            var val = e.target.className.split(" ");
            filterMenu(val[1]);
        });
    }
});

// Function to display the menu items based on the selected category
function displayMenu(food) {
    // Generating HTML for each food item
    var displayMenu = food.map(function (item) {
        return (
            `<div class="items">  
                <div class="img-conatiner"><img src=${item.img}  
                alt="${item.title}" class="img"></div>   
                <div class="details">  
                    <div class="title">${item.name}</div>  
                    <div class="price">$${item.price}</div>  
                </div>  
                <div class="cateogary">${item.cateogary}</div>  
            </div>`
        );
    });

    // Joining the HTML for menu items and injecting it into the container element
    displayMenu = displayMenu.join("");
    container.innerHTML = displayMenu;
}

// Extracting unique categories from the food array
var lists = food.reduce(function (values, items) {
    if (!values.includes(items.cateogary)) {
        values.push(items.cateogary);
    }
    return values;
}, ["ALL"]);

// Function to filter the menu based on the selected category
function filterMenu(cateogary) {
    // Filtering the food array based on the selected category
    var filter1 = food.filter(function (item) {
        if (item.cateogary === cateogary) {
            return item;
        }
    });

    // Displaying either all items or filtered items based on the selected category
    if (cateogary === "ALL") {
        displayMenu(food);
    } else {
        displayMenu(filter1);
    }
}
Explanation:

Array of Food Items: The food array contains objects, each representing a food item with properties like id, name, img, price, and cateogary.

DOM Selection: The document.querySelector method is used to select HTML elements with the classes .cateogaries and .container.

DOMContentLoaded Event: An event listener is added to ensure that the JavaScript code inside it runs only after the DOM content is fully loaded.

Initial Execution of filterMenu: The filterMenu function is initially called with the argument "ALL" to display all food items.

Category Buttons Generation: The unique categories are extracted from the food array and used to generate HTML for category buttons. These buttons are then added to the .cateogaries element.

Click Event Listeners: Click event listeners are added to each category button, which calls the filterMenu function with the selected category.

displayMenu Function: This function takes an array of food items and generates HTML for each item, which is then injected into the .container element.

Filtering Function (filterMenu): This function filters the food items based on the selected category. If "ALL" is selected, all items are displayed; otherwise, only items in the selected category are displayed.






