# crudpractice
#Delete User from website as well

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Add User</title>
</head>
<body>
    <form onsubmit="saveToLocalStorage(event)">
        <div class="container">
        <label for="uname"><b>UserName</b></label>
        <input type="text" placeholder="Enter Username" name="uname" required>
        <label for="email"><b>Email id</b></label>
        <input type="text" placeholder="Enter Email" name="email" required><br><br>
        <input type="submit" value="Submit">

        </div>
    </form>
    <ul id="listofitems"></ul>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/axios/1.3.4/axios.min.js"></script>
    <script>
        function saveToLocalStorage(event)
        {
           event.preventDefault();
           const name=event.target.uname.value;
           const email=event.target.email.value;
        //    localStorage.setItem('name',name);
        //    localStorage.setItem('email',emailId);
           const obj={
            name,
            email
           }
           axios.post("https://crudcrud.com/api/0608765802514c268488b3f2261c46e6/appointmentData",obj)
           .then((response)=>{
            showUserOnScreen(response.data)
            console.log(response);
           })
           .catch((err)=>{
            console.log(err);
           })
           //localStorage.setItem('userdetail',JSON.stringify(obj));
           //showUserOnScreen(obj)
        }

        window.addEventListener("DOMContentLoaded",()=>{
            axios.get("https://crudcrud.com/api/0608765802514c268488b3f2261c46e6/appointmentData")
            .then((response)=>{
                console.log(response)
                for(var i=0;i<response.data.length;i++)
                {
                    showUserOnScreen(response.data[i])
                }
            })
            .catch((error)=>{
                console.log(error);
            })
            // const localStorageObj=localStorage;
            // const localStorageKeys=Object.keys(localStorage);
            // for(var i=0;i<localStorageKeys.length;i++)
            // {
            //     const key=localStorageKeys[i];
            //     const showUserDetailsString=localStorageObj[key];
            //     const userDetailObj=JSON.parse(showUserDetailsString);
            //     showUserOnScreen(userDetailObj)
            // }
        })
        function showUserOnScreen(obj)
        {
           const parentele=document.getElementById("listofitems");
            const childele=document.createElement('li');
            childele.textContent = obj.name + "-" + obj.email;
    const deletebutton=document.createElement('input');
            deletebutton.type='button'
            deletebutton.value='Delete'
            deletebutton.onclick=()=>{
                axios.delete(`https://crudcrud.com/api/0608765802514c268488b3f2261c46e6/appointmentData/${obj._id}`)
                .then((response)=>{
                    parentele.removeChild(childele)
                    console.log(response);
                })
                .catch((err)=>{
                    console.log(err);
                })
                // localStorage.removeItem(obj.email)
                // parentele.removeChild(childele)
                }
                const editbutton = document.createElement("input");
  editbutton.type = "button";
  editbutton.value = "Edit";
  editbutton.onclick = () => {
    document.getElementById("unameInputTag").value = obj.name;
    document.getElementById("emailInputTag").value = obj.email;
  };

            childele.appendChild(deletebutton)
            childele.appendChild(editbutton)
            parentele.appendChild(childele)
        }
    </script>
</body>
</html>
