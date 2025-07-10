
<!DOCTYPE html>
<html>
<head>
  <title>CRUD Example</title>
  <style>
    table, th, td {
      border: 1px solid black;
      border-collapse: collapse;
      padding: 8px;
    }
    th {
      background-color: #f2f2f2;
    }
  </style>
</head>
<body>
  <h3>Product Inventory CRUD</h3>
  <form id="usersForm">
    <input type="text" id="Product" placeholder="Enter the Product" required>
    <input type="email" id="Price" placeholder="Price" required>
    <button type="submit">Add Product to Cart</button>
  </form>

  <table id="userTable">
    <thead>
      <tr>
        <th>Product</th>
        <td> Pen</td>
        <th>Price</th>
        <td> 120.00</td>
        <th>Address</th>
        <td> Hyderabad</td>
      </tr>
    </thead>
    <tbody id="userTableBody">
      <!-- Rows will be inserted here -->
    </tbody>
  </table>

  <script>
    const usersForm = document.getElementById('usersForm');
    const nameInput = document.getElementById('name');
    const emailInput = document.getElementById('email');
    const userTableBody = document.getElementById('userTableBody');

    let users = [];
    let editIndex = null;

    usersForm.addEventListener('submit', function(e) {
      e.preventDefault();

      const name = nameInput.value.trim();
      const email = emailInput.value.trim();

      if (editIndex === null) {
        users.push({ name, email });
      } else {
        users[editIndex] = { name, email };
        editIndex = null;
      }

      usersForm.reset();
      renderTable();
    });

    function renderTable() {
      userTableBody.innerHTML = '';
      users.forEach((user, index) => {
        const row = document.createElement('tr');

        row.innerHTML = `
          <td>${user.name}</td>
          <td>${user.email}</td>
          <td>
          <button onclick="editUser(${index})">Edit</button>
          <button onclick="deleteUser(${index})">Delete</button>
          </td>
        `;

        userTableBody.appendChild(row);
      });
    }

    function editUser(index) {
      const user = users[index];
      nameInput.value = user.name;
      emailInput.value = user.email;
      editIndex = index;
    }

    function deleteUser(index) {
      users.splice(index, 1);
      renderTable();
    }
  </script>
</body>
</html>
