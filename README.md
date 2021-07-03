# reactMenuApp
This React app presents menu items in card format. Data is dynamically rendered, including the buttons, depending on category type.
This menu can be changed easily - to display data of any type with changes to styling. 


This react app has a brief overview of the pertinent React code given below:
Firstly, the two states were set before the return was formatted.
```React
function App() {
  const [menuItems, setMenuItems] = useState(items);
  const [categories, setCategories] = useState(allCategories);
  
  return (
    <main>
      <section className="menu section">
        <div className="title">
          <h2>Our Menu</h2>
          <div className="underline"></div>
        </div>
        <Categories />
        <Menu items={menuItems} />
      </section>
    </main>
  );
}
```


For the menu there is a list if items which need to be iterated over and returned with format and specification. 
```React
const Menu = ({ items }) => {
  return (
    <div className="section-center">
      {items.map((menuItem) => {
        const { id, title, price, img, desc } = menuItem;
        return (
          <article key={id} className="menu item">
            <img src={img} alt={title} className="photo" />
            <div class="item info">
              <header>
                <h4>{title}</h4>
                <h4 className="price">{price}</h4>
              </header>
              <p className="item-text">{desc}</p>
            </div>
          </article>
        );
      })}
    </div>
  );
};
```


Now that the list has been set up the buttons can be worked on. There should be on button for each type of category including an All button. To start setting up this functionality the filterItems function was created inside of App.jsx.
```React
 const filterItems = (category) => {
    const newItems = items.filter((item) => item.category === category);
    setMenuItems(newItems);
  };
  ```


To use filterItems inside of Categories.jsx it must be set as a prop within the <Category /> component.
```React
   <CategoriesfilterItems={filterItems} />
   ```

   
 Another stipulation is added to the filterItems() function to account for the 'all' category.
 ```React
   const filterItems = (category) => {
    if (category === "all") {
      setMenuItems(items);
      return;
    }
    const newItems = items.filter((item) => item.category === category);
    setMenuItems(newItems);
  };
  ```

  Next, to filter the categories and ensure only unique ones are returned (to auto-update the menu data) all the array data items are mapped over. Set() is used to only return the unique values (to prevent repeat buttons). Finally, to get an 'all' button as well, it is included inside the new data array.
  ```React
  const allCategories = ["all", ...new Set(items.map((item) => item.category))];
  ```
  

 Now another prop is set in the <Category /> component to make the above data available in Component.jsx.
 ```React
         <Categories categories={categories} filterItems={filterItems} />
 ```

 
 Then the goal is to iterate over the categories inside of the data array and for each unique category to display a button. Then to add the text value into the list of filtered items. 
 ```React
 const Categories = ({ filterItems, categories }) => {
  return (
    <div class="btn-container">
      {categories.map((category, index) => {
        return (
          <button
            type="button"
            class="filter-btn"
            key={index}
            onClick={() => filterItems(category)}
          >
            {category}
          </button>
        );
      })}
    </div>
  );
};
```

Lastly render to the page.
```React
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById("root")
);
```

***End walkthrough
