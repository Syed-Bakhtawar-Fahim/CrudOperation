
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>CRUD Opration App || Syed Bakhtawar Fahim</title>
  </head>
  <body>
    <div class="main">
      <div class="add-user">
        <div class="heading">
          <h1>CRUD Operation App</h1>
          <div id="line"></div>
        </div>
        <!-- <h2>Add/Update/View/Delete Users</h2> -->
        <form action="" class="userdata">
          <div class="input-con">
            <label for="userid">ID</label>
            <input type="text" name="userid" id="userid" placeholder="Enter Your ID" />
          </div>
          <div class="input-con">
            <label for="Name">Name</label>
            <input type="text" name="name" id="name" placeholder="Enter Your Name"/>
          </div>
          <div class="input-con">
            <label for="Email">Email</label>
            <input type="text" name="email" id="email" placeholder="Enter your Email" />
          </div>
          <div class="input-con">
            <label for="address">Message</label>
            <textarea name="address" id="address" cols="28" rows="5" placeholder="You wanna say something?"></textarea>
          </div>
        </form>
        <div class="btn-con">
          <div class="add-btnc">
            <button id="add">Add</button>
          </div>
          <div class="update-btnc">
            <button id="update">Update</button>
          </div>
          <div class="view-btnc">
            <button id="view">View</button>
          </div>
          <div class="delete-btnc">
            <button id="delete">Delete</button>
          </div>
        </div>
        <table class="table">
          <thead>
            <tr>
              <th scope="col" class="text-center">Name</th>
              <th scope="col" class="text-center">Email</th>
              <th scope="col" class="text-center">Address</th>
            </tr>
          </thead>
          <tbody id="result" class="text-center"></tbody>
        </table>
      </div>
    </div>
    <script src="index.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  </body>
</html>


<style>
 @import url("https://fonts.googleapis.com/css2?family=Ubuntu:ital,wght@0,300;0,400;0,500;0,700;1,300;1,400;1,500;1,700&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "Ubuntu", sans-serif;
}

h2,
h1 {
  text-align: center;
  margin: 25px;
}

.add-user {
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.userdata {
  display: grid;
  grid-template-columns: auto auto;
  /* justify-content: center; */
  align-content: center;
  background-color: #f7f7f7;
  background-color: #73db71;
  margin: 10px;
  border-radius: 6px;
  grid-gap: 10px;
}

.input-con {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px;
}

form label {
  display: inline-block;
}

form input {
  margin: 25px;
  padding: 8px 34px;
  border: none;
  border-radius: 4px;
}

textarea {
  margin: 10px;
  border-radius: 6px;

}

.btn-con {
  display: flex;
  justify-content: center;
  align-items: center;
  /* background-color: #ddd; */
  padding: 10px;
}

.add-btnc,
.update-btnc,
.view-btnc,
.delete-btnc {
  margin: 10px;
  padding: 10px;
}

#add,
#update,
#view,
#delete {
  padding: 4px 19px;
  cursor: pointer;
  background-color: #0bad0b;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
}

#add,
#update,
#view,
#delete:hover {
  background-color: #0bad0b;
}
#add:hover{
  color: #ddd;
}
#update:hover{
  color: #ddd;
}
#view:hover{
  color: #ddd;
}
#delete:hover{
  color: #ddd;
}
.responsec {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin: 50px 0;
  /* background-color: #ddd; */
  padding: 5px;
  border: 1px solid #111;
}

.text-center {
  /* text-align: center; */
  padding: 17px;
  border-radius: 4px;
  
}

.table {
  margin: 50px;
}

th {
  border-bottom: 1px dashed #111;
}
.buttons{
  padding: 10px 10px;
  background-color: aqua;
}
.heading{
  background-color: #0bad0b;
  margin: 10px 10px;
  border-radius: 10px;
}

/* #line::before{
  content: "OR";
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  border-bottom: 1px solid gray;
  width: 25%;
  
} */

thead{
  
  color: #fff;
  background-color: #0bad0b;
}

</style>

<script>
 // User Add
const addUser = () => {
  let name = document.getElementById("name").value;
  let email = document.getElementById("email").value;
  let address = document.getElementById("address").value;
  axios
    .post("https://crudoperation123456.herokuapp.com/user", {
      name: name,
      email: email,
      address: address,
    })
    .then(function (response) {
      console.log(response);
      getUsers();
    })
    .catch(function (error) {
      console.log(error);
    });
};

const getUsers = () => {
  const result = document.getElementById("result");
  axios
    .get("https://crudoperation123456.herokuapp.com/users")
    .then(function (response) {
      console.log(response.data);
      const users = response.data;
      // console.log(users)
      const userList = users.map((user) => {
        return ` <tr> <td> ${user.name} </td> <td> ${user.email} </td> <td> ${user.address} </td></tr>`;
      });
      result.innerHTML = "";
      result.innerHTML = userList.join("");
    })
    .catch(function (error) {
      console.log(error);
    });
};

let addBtn = document.getElementById("add");
let viewBtn = document.getElementById("view");
let updateBtn = document.getElementById("update");
let deletBtn = document.getElementById("delete");

addBtn.addEventListener("click", addUser);

// update data
const updateData = async () => {
  let userid = document.getElementById("userid").value;
  console.log("userid", userid);
  let name = document.getElementById("name").value;
  let email = document.getElementById("email").value;
  let address = document.getElementById("address").value;

  if (name) {
    axios
      .put(`https://crudoperation123456.herokuapp.com/user/${userid}`, { name })
      .then((res) => getUsers());
  }
  if (email) {
    axios
      .put(`https://crudoperation123456.herokuapp.com/user/${userid}`, { email })
      .then((res) => getUsers());
  }
  if (address) {
    axios
      .put(`https://crudoperation123456.herokuapp.com/user/${userid}`, { address })
      .then((res) => getUsers());
  }
};

updateBtn.addEventListener("click", updateData);

// delete user
const deleteUser = () => {
  let userid = document.getElementById("userid").value;
  const result = document.getElementById("result");
  if (userid) {
    axios
      .delete(`https://crudoperation123456.herokuapp.com/user/${userid}`)
      .then(() => getUsers());
  }
  result.innerHTML = "";
};

deletBtn.addEventListener("click", deleteUser);

// search a single user
const getUser = () => {
  let userid = document.getElementById("userid").value;
  const result = document.getElementById("result");
  axios
    .get(`https://crudoperation123456.herokuapp.com/user/${userid}`)
    .then(function (response) {
      console.log(response.data);
      const users = response.data;
      result.innerHTML = ` <tr> <td> ${users.name} </td> <td> ${users.email} </td> <td> ${users.address} </td></tr>`;
    })
    .catch(function (error) {
      console.log(error);
    });
};

viewBtn.onclick = function viewRun() {
  let userid = document.getElementById("userid").value;
  if (userid === "") {
    getUsers();
  } else {
    getUser();
  }
};

  
</script>
