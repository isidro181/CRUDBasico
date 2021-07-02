# CRUDBasico<!doctype php>
<html lang="es">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-eOJMYsd53ii+scO/bJGFsiCZc+5NDVN2yr8+0RDqr0Ql0h+rP48ckxlpbzKgwra6" crossorigin="anonymous">

    <title>Guardar Informacion</title>
</head>

<body>
    <div class="container">
        
    </div>
    <div class="row mt-5"></div>
    <?php
    include "conexion.php";
    $Descripcion = $_POST["Descripción"];
    $Cantidad = $_POST["Cantidad"];
    $Precio = $_POST["Precio"];
    $Fechaelab = $_POST["Fechaelav"];
    $Fechavenc = $_POST["Fechavenc"];
    $ID = $_POST['ID'];
    $UpdateSQL= "update productos set descripción = '$Descripción', Cantidad ='$Cantidad', Precio ='$Precio', Fechaelav = '$Fechaelav', Fechavenc= '$Fechavenc' where id = $id";  

    if ($conexion->query($UpdateSQL) === TRUE) {
          echo '
           <div class="alert alert-success w-100" role="alert">
            <h4 class="alert-heading">Informacion almacenada</h4>
            <p>puede ver los datos almacenados en la informacion de '.$Descripción.' '.$Cantidad.'
            en la lista.</p>
            <hr>
             <p class="mb-0">La pagina sera redireccionada en 5 segundos.</p>           
             </div>
              <meta http-equiv="refresh" content="5; url=index.php">
            ';
    }else {
        echo '
        <div class="alert alert-warning" role="alert">
          <h4 class="alert-heading">Informacion no almacenada</h4>
          <p> Ha ocurrido un error con los datos enviados y estos no fueron almacenados.</p>
          <hr>
          <p class="mb-0">
          Error:'.$InsertSQL.'<br>'.$conexion->error.'
          .</p> 
           </div>
            <meta http-equiv="refresh" content="5; url=index.php">
            ';
        }

    $conexion->close();

    ?>



    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.bundle.min.js" integrity="sha384-JEW9xMcG8R+pH31jmWH6WWP0WintQrMb4s7ZOdauHnUtxwoG2vI5DkLtS3qm9Ekf" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.1/dist/umd/popper.min.js" integrity="sha384-SR1sx49pcuLnqZUnnPwx6FCym0wLsk5JZuNx2bPPENzswTNFaQU1RDvt3wT4gWFG" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.min.js" integrity="sha384-j0CNLUeiqtyaRmlzUHCPZ+Gy5fQu0dQ6eZ/xAww941Ai1SxSY+0EQqNXNE6DZiVc" crossorigin="anonymous"></script>
    -->
</body>

</html>
<?php
  $conexion=new mysqli("localhost","root","ledakarinap18","ejemplo web");
  if($conexion->connect_error){
      die("Error en conexion: ".$conexion->connect_error);
  }
?>

<!doctype html>
<html lang="es">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">

    <title>Editar Informacion</title>
  </head>
  <body>
    <div class="container">
        <?php
        include "conexion.php";
        $ID= $_GET['ID'];
        $fila = $conexion->query("Select * from productos where ID = $ID");
        $fila = $fila->fetch_assoc();
       
        ?>
        <div class="rom mt-5">
            <div class="card w-100">
                <div class="card-header">
                    <h4 class="card-title">Editar Informacion de Productos</h4>
                  
                </div>
                <div class="card-body">
                  <form action="actualizar.php" method="post">
                      <div class="row">
                          <input type="hidden" name="ID" value="<?php echo $fila['ID'] ?>">
                          <div class="form-group col-4">
                         <label for="">$Descripción:</label>
                         <input type="text" class="form-control" name="Descripción" placeholder="Por favor escriba la descripción del productos" required value="<?php echo $fila['Descripción'] ?>">
                         </div>
                        </div>
                        <div class="row mt-3">
                          <div class="form-group col-4">
                            <label for="">Cantidad:</label>
                            <input type="number" name="Cantidad" class="form-control" id="Cantidad" placeholder="Escriba la Cantidad" required value="<?php echo $fila['Cantidad'] ?>">
                           </div>
                            <div class="form-group col-4">
                        <label for="">Precio:</label>
                            <input type="number" name="Precio" id="Precio" class="form-control" placeholder="Escriba el Precio"required value="<?php echo $fila['Precio'] ?>">
                          </div>
                          <div class="form-group col-4">
                              <label for="">Fecha elaboracion:</label>
                              <input type="date" name="Fechaelav" class="form-control" required value="<?php echo $fila['Fechaelav'] ?>">
                          </div>
                           <div class="form-group col-4">
                            <label for="">Fecha vencimiento::</label>
                            <input type="date" name="Fechavenc" class="form-control"required value="<?php echo $fila['Fechavenc'] ?>">
                          </div>
                             </div>
                           </div>
                       </div>

                  <div class="row mt-3">
                      <div class="form-group col-12">
                          <button type="submit" class="btn btn-primary" >Guardar</button>
                          <a href="index.php" class="btn btn-secondary" >Volver</a>
                      </div>
                  </div>
                   <?php $conexion->close()?>
                  </form>
                </div>
              </div>
              
        </div>
    </div>

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ho+j7jyWK8fNQe+A12Hb8AhRq26LrZ/JpcUGGOn+Y7RsweNrtN/tE3MoK7ZeZDyx" crossorigin="anonymous"></script>

    <!-- Option 2: jQuery, Popper.js, and Bootstrap JS
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.min.js" integrity="sha384-w1Q4orYjBQndcko6MimVbzY0tgp4pWB4lZ7lr30WKz0vr/aWKhXdBNmNb5D92v7s" crossorigin="anonymous"></script>
    -->
  </body>
</html>
<!doctype html>
<html lang="es">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-eOJMYsd53ii+scO/bJGFsiCZc+5NDVN2yr8+0RDqr0Ql0h+rP48ckxlpbzKgwra6" crossorigin="anonymous">

    <title>Eliminando Informacion</title>
</head>

<body>
    <div class="container">     
    
    <div class="row mt-5">
    <?php
    include 'conexion.php';
    $descripción = $_GET['descripción'];
    
    $id=$_GET['ID'];
    $DELETESQL = "delete from Productos where id =$id ";

    if ($conexion->query($DELETESQL) === TRUE) {
                echo '
           <div class="alert alert-success w-100" role="alert">
            <h4 class="alert-heading">Informacion eliminada</h4>
            <p>Los datos han sido eliminados, ya no aparecera la informacion de '.$descripción.' en la lista de Productos</p>
            <hr>
            <p class="mb-0">La pagina sera redireccionada en 5 segundos.</p>
             
             </div>
              <meta http-equiv="refresh" content="5; url=index.php">
            ';
    } 

     else {
        echo '
           <div class="alert alert-warning" role="alert">
          <h4 class="alert-heading">Informacion almacenada</h4>
          <p>Ha ocurrido un error en los datos enviados y estos no fueron almacenados.</p>
          <hr>
          <p class="mb-0">
          Error: '.$DELETESQL.' <br>' . $conexion->error. '
          </p>
          
           </div>
            <meta http-equiv="refresh" content="5; url=index.php">
            ';
        }
 
    $conexion->close();
    
    ?>
    </div>
</div>

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.bundle.min.js" integrity="sha384-JEW9xMcG8R+pH31jmWH6WWP0WintQrMb4s7ZOdauHnUtxwoG2vI5DkLtS3qm9Ekf" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.1/dist/umd/popper.min.js" integrity="sha384-SR1sx49pcuLnqZUnnPwx6FCym0wLsk5JZuNx2bPPENzswTNFaQU1RDvt3wT4gWFG" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.min.js" integrity="sha384-j0CNLUeiqtyaRmlzUHCPZ+Gy5fQu0dQ6eZ/xAww941Ai1SxSY+0EQqNXNE6DZiVc" crossorigin="anonymous"></script>
    -->
    </div>
</body>

</html>
<!doctype html>
<html lang="es">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css"
        integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">

    <title>Lista de Productos</title>
</head>

<body>
    <div class="container">
        <?php
        include "conexion.php";
        $filas = $conexion->query("Select * from productos");
        $conexion->close()
        ?>
        <div class="row mt-5">
            <div class="card w-100">
                <div class="card-header">
                    <h4 class="card-title">
                        Lista de Productos
                        <a href="nuevo.html" class="btn btn-primary float-right">Nuevo</a>
                    </h4>
                </div>
                <table class="table">
                    <thead class="thead-dark">
                        <tr>
                            <th>Producto</th>
                            <th>Descripción</th>
                            <th>Cantidad</th>
                            <th>Precio</th>
                            <th>Fechaelav</th>
                            <th>Fechavenc</th>
                        </tr>
                    </thead>
                    <tbody>
                        <?php
                          foreach ($filas as $fila) {
                            echo '
                         
                            <tr>

                            <th scope="row">
                                <a href="editar.php?ID=' . $fila['ID'] . '" class="btn btn-primary">modificar</a>
                                <a href="eliminar.php?ID=' . $fila['ID'] .'&descripción='.$fila['Descripción'] .'" class="btn btn-danger">Eliminar</a>
                            </th>
                               
                                <td>' . $fila['Descripción'] . '</td>
                                <td>' . $fila['Cantidad'] . '</td>
                                <td>' . $fila['Precio'] . '</td>
                                <td>' . $fila['Fechaelav'] . '</td>
                                <td>' . $fila['Fechavenc'] . '</td>
                             </tr>
                        ';
                        }
                        ?>
            </div>
            </td>
            </tbody>
            </table>
            <div class="row mt-3">

            </div>


        </div>
    </div>

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"
        integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj"
        crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-ho+j7jyWK8fNQe+A12Hb8AhRq26LrZ/JpcUGGOn+Y7RsweNrtN/tE3MoK7ZeZDyx"
        crossorigin="anonymous"></script>

    <!-- Option 2: jQuery, Popper.js, and Bootstrap JS
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.min.js" integrity="sha384-w1Q4orYjBQndcko6MimVbzY0tgp4pWB4lZ7lr30WKz0vr/aWKhXdBNmNb5D92v7s" crossorigin="anonymous"></script>
    -->
</body>

</html>
<!doctype php>
<html lang="en">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-eOJMYsd53ii+scO/bJGFsiCZc+5NDVN2yr8+0RDqr0Ql0h+rP48ckxlpbzKgwra6" crossorigin="anonymous">

    <title>Guardar Informacion</title>
</head>

<body>
    <div class="container">
        
    </div>
    <div class="row mt-5"></div>
    <?php
    include "conexion.php";
    $Descripción = $_POST["Descripción"];
    $Cantidad = $_POST["Cantidad"];
    $Precio = $_POST["Precio"];
    $Fechaelav= $_POST["Fechaelav"];
    $Fechavenc = $_POST["Fechavenc"];
    $InsertSQL = "insert into productos (Descripción, Cantidad, Precio, Fechaelav, Fechavenc) values ('$Descripción', '$Cantidad', '$Precio', '$Fechaelav', '$Fechavenc')";

    if ($conexion->query($InsertSQL) === TRUE) {
          echo '
           <div class="alert alert-success w-100" role="alert">
            <h4 class="alert-heading">Informacion almacenada</h4>
            <p>puede ver los datos almacenados en la informacion de '.$Descripción.' '.$Cantidad.'
            en la lista.</p>
            <hr>
             <p class="mb-0">La pagina sera redireccionada en 5 segundos.</p>           
             </div>
              <meta http-equiv="refresh" content="5; url=index.php">
            ';
    }else {
        echo '
        <div class="alert alert-warning" role="alert">
          <h4 class="alert-heading">Informacion no almacenada</h4>
          <p> Ha ocurrido un error con los datos enviados y estos no fueron almacenados.</p>
          <hr>
          <p class="mb-0">
          Error:'.$InsertSQL.'<br>'.$conexion->error.'
          .</p> 
           </div>
            <meta http-equiv="refresh" content="5; url=index.php">
            ';
        }

    $conexion->close();

    ?>



    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.bundle.min.js" integrity="sha384-JEW9xMcG8R+pH31jmWH6WWP0WintQrMb4s7ZOdauHnUtxwoG2vI5DkLtS3qm9Ekf" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.1/dist/umd/popper.min.js" integrity="sha384-SR1sx49pcuLnqZUnnPwx6FCym0wLsk5JZuNx2bPPENzswTNFaQU1RDvt3wT4gWFG" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/js/bootstrap.min.js" integrity="sha384-j0CNLUeiqtyaRmlzUHCPZ+Gy5fQu0dQ6eZ/xAww941Ai1SxSY+0EQqNXNE6DZiVc" crossorigin="anonymous"></script>
    -->
</body>

</html>
<!doctype html>
<html lang="es">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">

    <title>Nueva Informacion</title>
  </head>
  <body>
    <div class="container">
        <div class="rom mt-5">
            <div class="card w-100">
                <div class="card-header">
                    <h4 class="card-title">Nueva Informacion de Productos</h4>
                  
                </div>
                <div class="card-body">
                  <form action="insertar.php" method="post">
                      <div class="row">
                          <div class="form-group col-4">
                         <label for="">Descripción:</label>
                         <input type="text" class="form-control" name="Descripción" placeholder="Por favor escriba la descripción del producto" required>
                         </div>
                        </div>
                        <div class="row mt-3">
                          <div class="form-group col-4">
                            <label for="">Cantidad:</label>
                            <input type="number" name="Cantidad" class="form-control" id="cantidad" placeholder="Escriba la cantidad" required>
                           </div>
                            <div class="form-group col-4">
                            <label for="">Precio:</label>
                            <input type="number" name="Precio" id="precio" class="form-control" placeholder="Escriba el precio"required>
                          </div>
                          <div class="form-group col-4">
                              <label for="">Fecha elaboracion:</label>
                              <input type="date" name="Fechaelav" class="form-control" required>
                          </div>
                           <div class="form-group col-4">
                            <label for="">Fecha vencimiento::</label>
                            <input type="date" name="Fechavenc" class="form-control"required>
                          </div>
                             </div>
                           </div>
                       </div>

                  <div class="row mt-3">
                      <div class="form-group col-12">
                          <button type="submit" class="btn btn-primary" >Guardar</button>
                          <a href="index.php" class="btn btn-secondary" >Volver</a>
                      </div>
                  </div>

                  </form>
                </div>
              </div>
              
        </div>
    </div>

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ho+j7jyWK8fNQe+A12Hb8AhRq26LrZ/JpcUGGOn+Y7RsweNrtN/tE3MoK7ZeZDyx" crossorigin="anonymous"></script>

    <!-- Option 2: jQuery, Popper.js, and Bootstrap JS
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.min.js" integrity="sha384-w1Q4orYjBQndcko6MimVbzY0tgp4pWB4lZ7lr30WKz0vr/aWKhXdBNmNb5D92v7s" crossorigin="anonymous"></script>
    -->
  </body>
</html>
