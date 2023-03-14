# php-crud-operations
by using mysql
//connect.php 
<?php 
$con=new mysqli("localhost",'root','','crudoperation');  

if (!$con){
    die(mysqli_error($con));
} 
?>  
//user.php   
<?php
include "connect.php";
if (isset($_POST['submit'])){
    $name=$_POST['name']; 
    $email=$_POST['email']; 
    $mobile=$_POST['mobile']; 
    $password=$_POST['password']; 

    $sql="insert into `crud` (name,email,mobile,password) 
    values('$name','$email','$mobile','$password')"; 

    $result=mysqli_query($con,$sql);
    if ($result){
        header('location:display.php');
    } 
}
?>


<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap demo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  </head>
  <body>
  <div class="container my-5">
  <form action="" method="POST">
  <div class="mb-3">
    <label class="form-label">Name</label>
    <input type="text" class="form-control"  name="name" placeholder="enter your name" autocomplete="off">
  </div> 
  <div class="mb-3">
    <label class="form-label">E-mail</label>
    <input type="email" class="form-control"  name="email" placeholder="enter your email" autocomplete="off">
  </div> 
   
  <div class="mb-3">
    <label class="form-label">Phone-number</label>
    <input type="number" class="form-control"  name="mobile" placeholder="enter your number" autocomplete="off">
  </div> 
  <div class="mb-3">
    <label class="form-label">Password</label>
    <input type="password" class="form-control"  name="password" placeholder="enter your password" autocomplete="off">
  </div>
  
  <button type="submit" class="btn btn-primary" name="submit">Submit</button>
</form>
  </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
  </body>
</html>   
//display.php 
<?php 
include "connect.php";
?>

<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap demo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  </head>
  <body>
    <div class="container my-auto">
        <button class="btn btn-primary my-5"><a class="text-light" href="user.php">Add User</a></button>
        <table class="table">
  <thead>
    <tr>
      <th scope="col">s no</th>
      <th scope="col">name</th>
      <th scope="col">email</th>
      <th scope="col">mobile</th>
      <th scope="col">password</th> 
      <th scope="col">operations</th> 

    </tr>
  </thead>
  <tbody>  
    <?php 
    $sql="select * from crud";
    $result=mysqli_query($con,$sql);
    if ($result){
        while($row=mysqli_fetch_assoc($result)){
            $id=$row['id'];
            $name=$row['name'];
            $email=$row['email'];
            $mobile=$row['mobile'];
            $password=$row['password'];
            echo '<tr>
            <th scope="row">'.$id.'</th>
            <td>'.$name.'</td>
            <td>'.$email.'</td>
            <td>'.$mobile.'</td> 
            <td>'.$password.'</td>
            <td><button class="btn btn-primary "><a href="update.php? updateid='.$id.'" class="text-light">Update</a></button>
    <button class="btn btn-danger "><a href="delete.php? deleteid='.$id. '" class="text-light">Delete</a></button>
    </td>
          </tr>'; 

        }
    }
    ?> 
    
  </tbody>
</table>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
  </body>
</html>  
//delete.php 
<?php 
include "connect.php";
if (isset($_GET['deleteid'])){
    $id=$_GET['deleteid']; 
    $sql="delete from `crud` where id=$id"; 
    $result=mysqli_query($con,$sql);
    if($result){
        header ('location:display.php');
    } 
    else{
        die(mysqli_error($con));
    }
}

?>  
//update.php 
<?php
include "connect.php";
$id=$_GET['updateid'];
$sql="select * from  `crud` where id=$id"; 
$result=mysqli_query($con,$sql);
$row=mysqli_fetch_assoc($result);
$id=$row['id'];
$name=$row['name'];
$email=$row['email'];
$mobile=$row['mobile'];
$password=$row['password'];

// echo $mobile;
// die();
if (isset($_POST['submit'])){
    $name=$_POST['name']; 
    $email=$_POST['email']; 
    $mobile=$_POST['mobile']; 
    $password=$_POST['password']; 
    // print_r($mobile);
    // die();
    $sql="update `crud` set id=$id ,name='$name',email='$email' ,mobile='$mobile',password='$password'
    where id=$id"; 

    $result=mysqli_query($con,$sql);
    if ($result){
        
        header('location:display.php');
    }
}
?>


<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap demo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  </head>
  <body>
  <div class="container my-5">
  <form action="" method="POST">
  <div class="mb-3">
    <label class="form-label">Name</label>
    <input type="text" class="form-control"  name="name" placeholder="enter your name" autocomplete="off" value=<?php echo $name;?>>
  </div> 
  <div class="mb-3">
    <label class="form-label">E-mail</label>
    <input type="email" class="form-control"  name="email" placeholder="enter your email" autocomplete="off"value=<?php echo $email;?>>
  </div> 
  
   
  <div class="mb-3">
    <label class="form-label">Phone-number</label>
    <input type="number" class="form-control"  name="mobile" placeholder="enter your number" autocomplete="off"  value=<?php echo $mobile;?>>
  </div> 
  
  <div class="mb-3">
    <label class="form-label">Password</label>
    <input type="password" class="form-control"  name="password" placeholder="enter your password" autocomplete="off" value=<?php echo $password;?>>
  </div> 
  
  
  <button type="submit" class="btn btn-primary" name="submit">Submit</button>
</form>
  </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN" crossorigin="anonymous"></script>
  </body>
</html>
