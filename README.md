<div align="center">
<table>
    <theader>
        <tr>
            <td><img src="https://github.com/rescobedoq/pw2/blob/main/epis.png?raw=true" alt="EPIS" style="width:50%; height:auto"/></td>
            <th>
                <span style="font-weight:bold;">UNIVERSIDAD NACIONAL DE SAN AGUSTIN</span><br />
                <span style="font-weight:bold;">FACULTAD DE INGENIERÍA DE PRODUCCIÓN Y SERVICIOS</span><br />
                <span style="font-weight:bold;">ESCUELA PROFESIONAL DE INGENIERÍA DE SISTEMAS</span>
            </th>
            <td><img src="https://github.com/rescobedoq/pw2/blob/main/abet.png?raw=true" alt="ABET" style="width:50%; height:auto"/></td>
        </tr>
    </theader>
    <tbody>
        <tr><td colspan="3"><span style="font-weight:bold;">Formato</span>: Guía de Práctica de Laboratorio / Talleres / Centros de Simulación</td></tr>
        <tr><td><span style="font-weight:bold;">Aprobación</span>:  2022/03/01</td><td><span style="font-weight:bold;">Código</span>: GUIA-PRLE-001</td><td><span style="font-weight:bold;">Página</span>: 1</td></tr>
    </tbody>
</table>
</div>

<div align="center">
<span style="font-weight:bold;">INFORME DE LABORATORIO</span><br />

<table>
<theader>
<tr><th colspan="6">INFORMACIÓN BÁSICA</th></tr>
</theader>
<tbody>
<tr><td>ASIGNATURA:</td><td colspan="5">Progamación Web 2</td></tr>
<tr><td>TÍTULO DE LA PRÁCTICA:</td><td colspan="5">Ferreteria Online - APIRest</td></tr>
<tr>
<td>NÚMERO DE PRÁCTICA:</td><td>07</td><td>AÑO LECTIVO:</td><td>2022 A</td><td>NRO. SEMESTRE:</td><td>III</td>
</tr>
<tr>
<td>FECHA DE PRESENTACIÓN:</td><td>9/08/2022</td><td>HORA DE PRESENTACIÓN: 11:55 am</td><td colspan="3"></td>
</tr>
<tr><td colspan="3">INTEGRANTE(s):
<ul>
      <li><a href="https://github.com/Daunsa">Daniel Edwad Tapia Saenz</a></li>
			<li><a href="https://github.com/timysuclle3">Michael Benjamin Suclle Suca</a></li>
			<li><a href="https://github.com/Jerbo03">José André Paredes Quispe</a></li>
			<li><a href="https://github.com/Icielo23">Valery Cielo Iquise Mamani</a></li>
			<li><a href="https://github.com/Mario-Chura">Mario Franco Chura Puma</a></li>
</ul>
</td>
<td>NOTA:</td><td colspan="2"></td>
</<tr>
<tr><td colspan="6">DOCENTE(s):
<ul>
<li>Richart Smith Escobedo Quispe - rescobedoq@unsa.edu.pe</li>
</ul>
</td>
</<tr>
</tbody>
</table>
</div>
  

  
<div align="center"><h2> SOLUCIÓN Y RESULTADOS </h2></div>

### I.	SOLUCIÓN DE EJERCICIOS/PROBLEMAS
- La estrutura del presente laboratorio es la siguiente:


 	  	

		    ├── PW2-22A-GrupoE06-Proyecto-semestral
		    │   ├── ferreteriaOnline
		    │   │    ├── autenticacion
		    │   │    |── blog
		    │   │    ├── carro
		    │   │    |── contacto
		    │   │    ├── ferreteriaOnline
		    │   │    |── ferreteriaOnlineApp
		    │   │    |── media
		    │   │    ├── pedidos
		    │   │    |── servicios
		    │   │    ├── tienda
		    │   │    ├── manage.py
		    │   │    └── db.sqlite3
		    │   │
		    │   ├── .gitignore
		    │   │
		    │   ├── README.md
		    │   │
		    │   |__ requirements.txt
		    │   
		    └── README.md
	   	
	
- __Instalacion de REST__

	- Primero vamos a instalar REST con la siguiente línea de código:

	```py
				pip install djangorestframework
			
	 ```
	 Ademas tambien cabe mencionar que la instalación de paquetes como markdown o django-filter pueden ser opcionales. En caso de querer usarlas se puede ejecutar:
 
	```py
		pip install markdown
		pip install django-filter
		pip install djangorestframework
	 ```

	 Ademas tambien cabe mencionar que la instalación de paquetes como markdown o django-filter pueden ser opcionales. En caso de querer usarlas se puede ejecutar:
 	- En el archivo <code>setting.py</code> del proyecto agregamos ***'rest_framework'*** en aplicaciones instaladas de la siguiente manera:


	```py
				INSTALLED_APPS = [
    						'rest_framework',
    				]
			
	 ```
	 
- __Aplicaciones de nuestro proyecto__

 	- Ahora podemos trabajar sobre las aplicaciones de nuestro proyecto, es nuestro caso disponemos de las siguientes aplicaciones:


	```py
				INSTALLED_APPS = [
    						'ferreteriaOnlineApp',
    						'servicios',
    						'blog',
   						'contacto',
    						'tienda',
    						'carro',
    						'autenticacion',
    						'pedidos',
    				]
			
	 ```
	 
- __Creando API REST para nuestras aplicaciones__

	-  Primero tenemos que crear nuestro serializador el cual se encargara del proceso de consulta de datos, volverlo en texto plano como JSON y poder enviarlo como una URL al usuario para ello creamos el archivo <code>serializers.py</code> en nuestra aplicación ***tienda*** importamos ***serializers*** y colocamos las siguientes líneas:


	```py
		from rest_framework import serializers
		from .models import *

		class ProductoSerializer(serializers.ModelSerializer):
		    class Meta:
		        model = Producto
		        fields = ("__all__")

		    def create(self,validated_data):
		        return Producto.objects.create(**validated_data)

		class CategoriaSerializer(serializers.ModelSerializer):
		    class Meta:
		        model = CategoriaProd
		        fields = ("__all__")

		    def create(self,validated_data):
		        return CategoriaProd.objects.create(**validated_data)
			
	 ```
	-  Podemos personalizar que campos queremos que aparezcan de la siguiente manera:


	```py
	    class Meta:
 	       model = CategoriaProd
 	       fields = ('id','nombre','created')
			
	 ```
	 
	- Los serializadores toman la data que les mandamos, en este caso de los modelos ***Producto*** y ***CategoriaProd*** y lo serializa en este caso trabajamos con todas las líneas es por ello que ponemos <code>fields = ("__all__")</code>
	- En el caso de <code>def create(self,validated_data)</code> nos permite validar la data que enviamos.

		

	- Nos dirigimos al <code>view.py</code> de nuestra aplicación ***tienda*** e importamos lo siguiente:


	```py
		from .serializers import *

		from rest_framework.views import APIView
		from rest_framework.response import Response
			
	 ```
	 
	- Además en <code>view.py</code> de nuestra aplicación ***tienda*** creamos la clase ***ProductoView*** para poder extraer el **APIView** y poder usar las operaciones de get y post :


	```py
		class ProductoView(APIView):
    
		    def get(self,request):
		        dataProducto = Producto.objects.all()
		        serProducto = ProductoSerializer(dataProducto,many=True)
		        return Response(serProducto.data)
    
		    def post(self,request):
		        serProducto = ProductoSerializer(data=request.data)
		        serProducto.is_valid(raise_exception=True)
		        serProducto.save()
        
 		       return Response(serProducto.data)
			
	 ```
	 
	- Ahora vamos a crear nuestro sistema de rutas en personalidas <code>url.py</code> de nuestra aplicacion ***tienda*** escribimos las siguientes path en ***urlpatterns***, para ello antes debemos de importar ***path***:


	```py
		from django.urls import path

		from .import views


		urlpatterns = [
    
		    path('',views.tienda, name="Tienda"),

		    path('productoapi',views.ProductoView.as_view(),name='productoapi'),
		    path('productoapi/<int:producto_id>',views.ProductoDetailView.as_view()),
		    path('categoriaapi',views.CategoriaView.as_view(),name='categoriaapi'),
		    path('categoriaapi/<int:categoria_id>',views.CategoriaDetailView.as_view())
    
		]
			
	 ```
	 
	- Ahora debemos repetir los pasos anteriores para las siguientes aplicaciones::


	```py

    						'servicios',
    						'blog',
   						'contacto',
    						'tienda',
    						'carro',
    						'autenticacion',
    						'pedidos',
			
	 ```


#
### II.	SOLUCIÓN DEL CUESTIONARIO
#


#

### III.	CONCLUSIONES
#

<div align="justify">

- Djagorestframework es de gran utilidad para el desarrollo rápido y seguro de una api por lo que se hizo fácil convertir nuestro proyecto de una tienda a una aplicación backend para el consumo para otras aplicaciones frontend, esto es de gran utilidad ya que permite distinguir más fácilmente los paradigmas que se seguirán tanto en el modelado de data como en la visualización de la misma<br>
- Las aplicaciones que se puede dar con djangorestframework son muy variadas tanto como utiles ya que se pueden uttilizar para generar mucha informacion apartir de una poca dentro de nuestras bases de datos.<br>
- Debido a la facilida de implementacion de una api con django se puede realizar un programa con una mayor cantidad de tablas ya que este cuenta con formularios prediseñados para todo caso ademas que al ser open source se puede modificar a gusto y agregar alto grado de personalizacion, asi tambien se puede realizar distintas salidas de datos asi como informacion prediseñada.<br>
- Lo curioso de REST es que al ser implementado, no hay importancia en el lenguaje o los frameworks que usan tanto el cliente como el servidor, puesto que en la logica REST se recibe y envia toda la información necesaria para poder ejecutar cada requerimiento o solicitud, es por ello que esto conlleva utilizar un formato flexible. Estos formatos, por ejemplo, pueden ser: Json, Xml, formato binario o texto plano. Y dicho sea de paso, Json es el mas usado actualmente.<br>
- Algunas ventajas de crear una API como servicio, son:
	- Control de la información que se entrega.
	- Información actualizada.
	- Flexibilidad del manejo interno del servicio.
	- Volumen de datos.
	- Facilidad de filtrar información.
	- Datos normalizados
</div>


<p align="justify">

- A manera de Anexo

	- Actualmente rest es la logica mas utilizada para la construccion de API's.
A la par es muy importante conocer las definicion de API, REST y RESTfulAPI. Para evitar equivocaciónes en el momento de producir o crear las distintas variedades de aplicaciónes de software interactivas que trabajan bajo el esquema de cliente servidor.
API:es una abstraccion de funciones y procedimientos.
REST:Es una logica de restricciones y recomendaciones bajo la cual se puede construir un API, podemos decir que es un estilo de arquitectura.
RESTfulAPI: Esta es una API ya implementada y que utiliza la logica de REST.<br>
Ademas de ello necesitamos saber que REST tiene varias especificaciones como el verbo HTTP, la dirección unica (URI) y los datos que necesita para funcionar.<br>
Los verbos HTTP son identificadores que identifican el objetivo de accion de el cliente, hay varios, de las cuales estan son las principales:<br>
GET: usado para procedimientos que debuelven información al cliente.<br>
POST: usado para que el cliente pueda crear datos dentro del servidor, como crear registros dentro de una base de datos.<br>
PUT/PATCH: Es usado para editar recursos que ya existen dentro del servidor.<br>
DELETE: Y claramente delete sirve para eliminar recursos dentro del servidor.<br>



	- Estructura básica

		- Django Rest Framework se basa fundamentalmente en 3 componentes: los serializadores, las vistas y los routers. Y a continuación hablaremos acerca de ellos.
		- Los routers son una herramienta que nos permiten definir las urls de nuestro API ordenada. En resumen nos permiten definir cómodamente conjuntos de urls y nos encaminan a nuestros métodos en función del verbo HTTP (GET, POST, PUT, PATCH...).
		- Las views no son más que extensiones de las class-view de django, pero de alguna forma optimizadas para simplificarnos el enganche con los routers, los serializadores y los modelos.
		- Por último, los serializadores nos permiten estendarizar cómo serán las respuestas que retornara nuestra API y cómo procesaremos el contenido de los resultados que nos lleguen.
		- Las aplicaciones como Postman o SopaUI se utilizan por excelencia para la prueba de APIs que tengamos desarrollados en el backend sin la necesidad de tener desarrollado un frontend aquí podemos desarrollar consultas HTTP mediante los métodos GET, POST, DELETE, PUT, entre otros y ver las respuestas de los estados que vamos a recibir en cada uno de los casos, estas aplicaciones nos facilitan mucho al momento de poder probar o ver si efectivamente nuestras APIs devuelven lo que tienen que devolver.

</p>
#
<div align="center"><h2>  RETROALIMENTACIÓN GENERAL </h2></div> <br>


#

<div align="center"><h2> REFERENCIAS Y BIBLIOGRAFÍAL </h2></div> <br>

-   https://www.youtube.com/watch?v=SbhzQqP1p70&ab_channel=C%C3%B3digoMorsa
-   https://www.redhat.com/es/topics/api/what-is-a-rest-api
-   https://docs.djangoproject.com/en/4.0/
-   https://www.django-rest-framework.org/
-   https://www.paradigmadigital.com/dev/introduccion-django-rest-framework/
-   https://www.postman.com/downloads/ 
