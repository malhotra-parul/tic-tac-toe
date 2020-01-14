This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

## Steps to implement the game :
1. Create three basic components - 
    a. *Square* - renders a square component which ocnsists of a button with no value to be displayed
    b. *Board* - renders a Square component and creates a 3*3 grid. Also, displays status of next player's turn as a string.
    c. *Game* - renders two div tags - first consists of Board and second consists of game-info which displays status and steps taken by user on the grid as an ordered list of buttons.

2. Next, we display value "X" when the user clicks on any square. For this, we create a variable "value" in this.state and initialize it to null. When a user clicks on any square, onClick method is invoked which calls t*his.setState()* to reset the state of the variable value to "X" and renders the updated page automatically.

3. We also display the "this.state.value" on the button. 

4. Next, we are going to *lift the state up to the parent component* - Board. We are doing so to maintain the entire game state in board component rather than every square keeping its own state seperately as doing so will get difficult to manage otherwise. We are going to use props instead of this.state to pass value and onClick method from Board to Square component.

5. For this, firstly we create a constructor in Board component and create a state variable "squares" which holds an Array of size 9 containing all null values initially. This array consists of individual values held by each square.

6. We use a method - *renderSquare(i) which returns a Square component*. Here, i is initialised at the time of rendering the Squares in the Board component. i holds values from 0 to 9 depending upon the position of the square in the grid.

7. In renderSquare method while returning the Square component we will include a props - "value" which will contain the value as this.state.squares[i]. Initially all values will be null. However, we will also implement a function handleClick(i) which shall be invoked when any square is clicked. Now, our renderSquare(i) will return a Square component like this:
*<Square value={this.state.squares[i]} onClick={()=>{this.handleClick(i)}} />*

8. Also, we will be needed to update the Square's render method to use the defined props. We will replace *this.state.value to this.props.value &
update the onClick method to this.props.onClick
*
9. Now, we will implement handleClick() in Board component. 
    *Step 1 - create a const squares which will hold the copy of squares-  this.state.squares.slice()
    Step 2 - We will set squares[i] to "X" (for the time being)
    Step 3 - Call this.setState({squares: squares}) to update the squares array and render the component again.*
The reason we are working on a copy of squares array rather than modifying the original one is it will later help us when we want to time travel to an older state.

10. We can choose to convert Squares from class component to a *functional component* as it now has a render() method only and rest everything is getting controlled from its parents component.

11. 