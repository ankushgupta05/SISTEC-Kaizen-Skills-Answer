
# 

# Step 1: Initialize Project

mkdir nodejs-crud-form
cd nodejs-crud-form
npm init -y
npm install express ejs body-parser






# Step 2: Folder Structure

nodejs-crud-form/
├── views/
│   └── form.ejs
├── app.js








# Step 3: app.js
```
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

let dataStore = [];

app.set('view engine', 'ejs');
app.use(bodyParser.urlencoded({ extended: false }));

app.get('/', (req, res) => {
  res.render('form', { data: dataStore });
});

app.post('/', (req, res) => {
  const { name, index, action } = req.body;

  if (action === 'create') {
    dataStore.push(name);
  } else if (action === 'update' && index) {
    dataStore[parseInt(index)] = name;
  } else if (action === 'delete' && index) {
    dataStore.splice(parseInt(index), 1);
  }

  res.redirect('/');
});

app.listen(3000, () => {
  console.log('Server started on http://localhost:3000');
});


```






# Step 4: views/form.ejs
```
<!DOCTYPE html>
<html>
<head><title>Node.js CRUD with One Form</title></head>
<body>
  <h2>CRUD Operation (No JS)</h2>
  <form method="POST">
    <input type="text" name="name" placeholder="Name" required>
    <input type="number" name="index" placeholder="Index (for update/delete)">
    <button type="submit" name="action" value="create">Create</button>
    <button type="submit" name="action" value="update">Update</button>
    <button type="submit" name="action" value="delete">Delete</button>
  </form>

  <h3>Data List</h3>
  <ul>
    <% data.forEach((item, i) => { %>
      <li><%= i %>: <%= item %></li>
    <% }); %>
  </ul>
</body>
</html>

```





# Step 5: Run the Server
node app.js








Open http://localhost:3000 and use the form to create, update, or delete items — all without JavaScript.


