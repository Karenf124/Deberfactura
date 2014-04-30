Deberfactura
============

Factura 
<!DOCTYPE html>

<html >
    <head>
        <title>Facturacion</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
		   <script>
            function datos() {
                var nombres = ["Karen", "Eddy", "Shirley", "Eduardo","Jessica", "Pablo"];
                var lista = ["Chompra", "Camiseta", "Calcetines", "Gorras", "Pantalonetas"];
                var listaClientesDatos = document.getElementById('listaClientes');
                for (var i = 0; i < nombres.length; i++) {
                    var opt = document.createElement('option');
                    opt.innerHTML = nombres[i];
                    opt.value = nombres[i];
                    listaClientesDatos.appendChild(opt);
                }
                var listaProductosDatos = document.getElementById('listaProducto');
                for (var i = 0; i < lista.length; i++) {
                    var opt = document.createElement('option');
                    opt.innerHTML = lista[i];
                    opt.value = lista[i];
                    listaProductosDatos.appendChild(opt);
                }

            }
            function total() {
                var unitario = document.getElementById('precioUnit').value;
                var cantidad = document.getElementById('cantidad').value;
                var total = parseFloat(unitario) * parseFloat(cantidad);
                document.getElementById('total').value = total;
            }
            function crearFilaProductoIngresado() {
                var subtotal = document.getElementById('subtotal').value;
                document.getElementById('subtotal').value = parseFloat(subtotal) + parseFloat(document.getElementById('total').value);
                var subtotalNuevo = document.getElementById('subtotal').value;
                document.getElementById('iva').value = parseFloat(subtotalNuevo) * 0.12;
                var ivaNuevo = document.getElementById('iva').value;
                document.getElementById('descuento').value = (parseFloat(subtotalNuevo) + parseFloat(ivaNuevo)) * 0.05;
                var descuentoNuevo = document.getElementById('descuento').value;
                document.getElementById('totalFinal').value = (parseFloat(subtotalNuevo) + parseFloat(ivaNuevo)) - parseFloat(descuentoNuevo);
                capotTexto = document.createElement('input');
                capotTexto.type = "text";
                capotTexto.name = "producto";
                capotTexto.id = "produc";
                capotTexto.value = document.getElementById('listaProducto').value + '     -     ' + document.getElementById('precioUnit').value + '     -     ' + document.getElementById('cantidad').value + '     -     ' + document.getElementById('total').value;
                capotTexto.size = "50";
                document.getElementById('contenido').appendChild(capotTexto);
                salto = document.createElement('br');
                document.getElementById('contenido').appendChild(salto);
            }
			
	function solotexto()
	{
		for(i=1;i<=6;i++)
		{
			var prod = eval(document.getElementById("producto"+i).value);
			for(j=0;j<=9;j++)
			{
				if(prod==j)
				{
					alert("En este campo no puede ingresar numeros");
					document.getElementById("producto"+i).value="";
				}
			}
		}		
	}
	
	function solonumero()
	{
		for(i=1;i<=6;i++)
		{
			var prod = eval(document.getElementById("producto"+i).value);
			for(j=0;j<=9;j++)
			{
				if(prod==j)
				{
					return true;
				}
				else
				{
					alert("En este campo no puede ingresar texto");
				}
			}
		}		
	}
</script>
<script type= "text/javascript">
	function validartexto()
	{
		var textval = document.getElementById('NOM').value;
		if(textval=="")
		{
			alert("En el campo nombre del cliente no has ingresado datos");
		}
		else if(/^[A-Z a-z ñáéó]{2,15}\s[A-Z a-z]{1,10}$/.test(textval))
		{
			alert("El nombre esta correcto");
			return (true);
		}
		else
		{
			alert("El nombre no es correcto");
			document.getElementById('NOM').value="";
			return (false);		
	
		}
	}
	
	
	
	function valida_telefono()
	{
		var number=document.getElementById("numero").value;
		var canti=number.length;
		var porcio;
		var acu3=0;
		if(number=="")
		{
			alert("En el campo telefono no ha ingresado datos");
		}
		else
		{
			for(i=0;i<canti;i++)
			{
				porcio=number.substring(i,i+1);
				if(porcio=="0"||porcio=="1"||porcio=="2"||porcio=="3"||porcio=="4"||porcio=="5"||porcio=="6"||porcio=="7"||porcio=="8"||porcio=="9")
				{
					acu3++;
				}
			}
			if(acu3==canti)
			{
				alert("El telefono esta escrito correctamente");
			}
			else
			{
				alert("En el campo telefono no debe llevar texto");
				document.getElementById('numero').value="";
			}
		}
	}
	
	
	function direccion()
	{
		var direc = document.getElementById("direction").value;
		if(direc=="")
		{
			alert("En el campo direccion no has ingresado datos");
		}
		else
		{
			alert("La direccion se ha ingresado correectamente");
		}
	}
	
	function Generar()
	{
		var str_cadenaentrada="";	
		for(i=1;i<=6;i++)
		{
			str_cadenaentrada+="<p><input type='text' name='producto"+i+"' id='producto"+i+"' onchange='solotexto()'>";
			str_cadenaentrada+="<input type='text' name='cantidad"+i+"' onchange='cantidadyprecio(),'numero(this.value)'>";
			str_cadenaentrada+="<input type='text' name='precio"+i+"' onchange='cantidadyprecio(), numero(this.value)'>";
			str_cadenaentrada+="<input type='text' name='subtotal"+i+"'>";
		}
			document.getElementById("contenido").innerHTML=str_cadenaentrada;
	}
            function verificarCedula()
            {
                var cedula = document.getElementById("cedulaIngresada").value;
                array = cedula.split("");
                num = array.length;
                if (num == 10)
                {
                    total = 0;
                    digito = (array[9] * 1);
                    for (i = 0; i < (num - 1); i++)
                    {
                        mult = 0;
                        if ((i % 2) != 0) {
                            total = total + (array[i] * 1);
                        }
                        else
                        {
                            mult = array[i] * 2;
                            if (mult > 9)
                                total = total + (mult - 9);
                            else
                                total = total + mult;
                        }
                    }
                    decena = total / 10;
                    decena = Math.floor(decena);
                    decena = (decena + 1) * 10;
                    final = (decena - total);
                    if ((final == 10 && digito == 0) || (final == digito)) {
                        alert("Cedula Valida");
                        return true;
                    }
                    else
                    {
                        alert("Cedula NO Valida");
                        return false;
                    }
                }
                else
                {
                    alert("La cedua no puede tener menos de 10 digitos");
                    return false;
                }
            }
        </script>

        </script>
    </head>
	
    <body onload="datos()" BGCOLOR="silver">
		<center>
		 <li><a href="validacion.html">Validaciones</a>
	<h4>CONFECCIONES FM</h4>
	<label>NOMBRE DEL CLIENTE</label>

	<input type ="text" id="NOM" onchange="validartexto()">
	

	 
    </head>
    <body >
        <label>CEDULA</label>
        <input type="text" id="cedulaIngresada"  />
        <input type="button" id="ok" value="VERIFICAR CEDULA" onclick="verificarCedula()"/>
    </body>

	<label>TELEFONO</label>
	
	<input type ="text" id="numero">
	
	
	<label>DIRECCION</label>

	<input type ="text" id="direction"><br>
	
	
	<label>FECHA</label>
	
	<input type ="date">
	
	<br><br>
	<input type ="button" value="Validar campos" style="width: 150px;" onClick="valida_telefono(),direccion()"><br><br>
        Escoja Nombre del Cliente: <select id="listaClientes"></select><br>
        <hr>
        Lista de Pedidos  <select id="listaProducto"></select>
        Precio Unitario: <input type="text" id="precioUnit" />
        Cantidad: <input type="text" id="cantidad" onchange="total()"/>

        Total: <input type="text" id="total"/>
        <input type="button" id="agregar" value="Agregar" onclick="crearFilaProductoIngresado()"/><br>
        <hr><hr>

        Resumen del Pedido: <br>
        Producto - Precio - Cantidad - Total
        <div id="contenido">

        </div>
        <hr>
        Subtotal : <input type="text" id="subtotal" value="0"/>
        IVA 12%: <input type="text" id="iva"/>
        Descuento 5%: <input type="text" id="descuento"/>
        Total Final: <input type="text" id="totalFinal"/>
		<form name="prueba">

    </body>
</html>
