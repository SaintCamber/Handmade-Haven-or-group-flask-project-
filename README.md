# Handmade Haven
https://handmade-haven-1ue7.onrender.com
<img width="949" alt="Screenshot 2023-04-05 110019" src="https://user-images.githubusercontent.com/105817556/230186038-29876bc6-7b01-45fe-b91e-04e2dc6e64ef.png">



Handmade Haven is a web application that provides an Etsy-like shopping experience. It includes a Flask back end with SQLAlchemy and a React front end, allowing users to sign up, log in, browse and buy products, and leave reviews on those products. The app also includes the ability to create, delete, and edit products.
## Technologies Used

- Flask
- SQLAlchemy
- React
- 
## Project Details 

This was a project that was developed by team of 4 individuals and built within a week.

### Development Team
- Kyle Parkin
https://github.com/13kparkin
- Grace Cizma 
https://github.com/SaintCamber
- Sarah Nodwell 
https://github.com/gracecizma
- Brennan Cota
https://github.com/Sleightttt

### Features

- User sign up and login
- Shopping cart functionality
- Product search and browsing
- Product creation, deletion, and editing
- Review creation, edit, deletion, and viewing

## technical challenges - Sarah
The task given to Sarah Nodwell was to implement the reviews feature in Python, which required the use of various coding techniques and design patterns. As an experienced developer, Sarah decided to create the reviews component using a modular approach, breaking down the feature into multiple building blocks, each with a specific functionality.

This approach allowed the reviews component to be seamlessly integrated into other group member's components without causing any disruptions or conflicts. The modular design of the reviews component made it easier to maintain, debug, and update as necessary, while also improving its reusability and scalability.

To ensure that the reviews component met the required standards and specifications, Sarah made use of various Pythonic coding techniques, including object-oriented programming, functional programming, and exception handling. She also used best practices such as following the PEP 8 style guide and writing unit tests to ensure that the code was of high quality and error-free.

Once the reviews component was completed and tested, Sarah was pleased to see that it could be imported into other components using just one line of code, which was a significant achievement. This demonstrated the power and flexibility of the modular approach and how it could make the development process smoother, more efficient, and more enjoyable for all team members.

Overall, the implementation of the reviews component was a fun and challenging project that required technical expertise, creativity, and collaboration. It showcased the importance of using Pythonic and modular coding techniques to create robust and scalable software components that can be easily integrated into larger systems.


when imported vs the actual component:
```
  <MainReviewBlock id={id} product={product} user={currUser}/>
  
```

```
const MainReviewBlock = ({ id, product, user }) => {
    let { closeMenu } = useModal()
    let dispatch = useDispatch()
    let [page, setPage] = useState(1)
    let [per_page, setPer_Page] = useState(3)
    // let Product = useSelector(state => state.products.SingleProduct)
    let ProductReviews = useSelector(state => state.reviews.SingleProductsReviews)
    useEffect(() => {
        dispatch(getReviewsByProduct(id, page, per_page))

    }, [id, dispatch, product, page, per_page, product.avg_rating]
    )
    function handlePages(e) {
        e.preventDefault()
        let buttonValue = e.target.value
        if (page <= 1 && +buttonValue < 0) {
            return
        }
        setPage(page + +buttonValue)
    }

    return ProductReviews && (
        <div className="MainBlock">
            <p>{product?.total_reviews}{product?.total_reviews == 1 ? ' Review' : ' Reviews'}</p>
            <p>Average Star Rating: {product?.avg_rating || 0.0}</p>
            <div className="pagination">
            <button
                className="ReviewPageButton"
                onClick={handlePages}
                value={-1}
            >{"<="}</button>{page}<button
                className="ReviewPageButton"
                onClick={handlePages}
                value={1}
            >{"=>"}</button>
            <select
                placeholder="#/Page"
                value={per_page}
                onChange={(e) => setPer_Page(e.target.value)}
            >
                <option value={5}>5</option>
                <option value={10}>10</option>
                <option value={15}>15</option>
            </select></div>
            <div className="MainSubBlock">
                <OpenModalButton
                    buttonText="New Review"
                    onItemClick={closeMenu}
                    modalComponent={<ReviewModal product_id={product?.id} />}
                />
                {Object.values(ProductReviews).map((review) => {
                    return (
                        <>
                            <SingleReviewBlock key={review.id} review={review} />
                            {review.author.id === user?.id ? (<><OpenModalButton
                                buttonText="Delete"
                                onItemClick={closeMenu}
                                modalComponent={<DeleteReviewModal review={review} page={page} per_page={per_page} />}
                            />
                                <OpenModalButton
                                    buttonText="Update"
                                    onItemClick={closeMenu}
                                    modalComponent={<UpdateReviewsModal Review={review} />}
                                /></>) : ""}
                        </>
                    )

                })}

            </div>
        </div>
    )
}

```







### Installation & Development

To install and run the Handmade Haven app, follow these steps:

1. Clone the repository from GitHub:

```bash
git clone https://github.com/your-username/handmade-haven.git
```

2. Install the required Python packages:
```bash
pipenv install -r requirements.txt
```

3. Install the required JavaScript packages:
```bash
cd react-app
npm install
```

4. Start the Flask server:
```bash
cd app
pipenv shell
flask run
```

5. Start the React app:
```bash
cd react-app
npm start
```

Navigate to http://localhost:3000 in your web browser to use the app.
License

This project is licensed under the MIT License
