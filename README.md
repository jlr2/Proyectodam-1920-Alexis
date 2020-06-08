# ProyectoDam: Organize-It App




<br>

## Índice
> **[1- Introducción.](#1)**
>
> **[ 1.1- Objetivo General.](#1.1)**
>
> **[ 1.2- Objetivos especificos.](#1.2)**
>
> **[2- Tecnologías de desarollo.](#2)**
>
> **[3- Entorno de desarrollo.](#3)**
>
> **[4- Despliegue de la aplicación.](#4)**
>
> **[5- Análisis de la aplicación.](#5)**
>
> **[ 5.1- Requisitos funcionales.](#5.1)**
>
> **[  5.1.2- Diagrama de casos de uso.](#5.1.2)**
>
> **[  5.1.3- Descripción de casos de uso.](#5.1.3)**
>
> **[ 5.2- Diagrama de clases.](#5.2)**
>
> **[ 6- Diseño de la aplicación.](#6)**
>
> **[ 6.1- Modelo de objetos de negocio.](#6.1)**
>
> **[7- Codificación del proyecto.](#7)**
>
> **[8- Pruebas.](#8)**
>
> **[9- Detalles técnicos.](#9)**
>
> **[10- Problemas durante el desarrollo.](#10)**
>
> **[11- Mejoras posibles.](#11)**
>
> **[12- Conclusiones.](#12)**
>
> **[13- Bibliografia/Webgrafía.](#13)**

<br>
<br>

<a name="1"></a>
# Introducción


Este proyecto final para el grado DAM tratará el desarrollo de una aplicación con solución SaaS, la aplicación a su vez dará solución
a la organización de actividades <br> permitiendo que varias personas se pongan de acuerdo de la forma más rápida y eficiente posible. 
Para el desarrollo del proyecto se utilizará una arquitectura <br> basada en microservicios, siendo que la lógica de la aplicación será dividida
 por funcionalidades que constituirán los distintos microservicios.



<a name="1.1"></a>
## Objetivo general
Ralizar un estudio del modelo de distribución de software SaaS basado en microservicios, identificando los componentes claves </br>
necesarios para llegar a desplegar una<br>  aplicación basada en esta arquitectura.


<br>

<a name="1.2"></a>
## Objetivos específicos

<ul>
    <li>Conocer los principales componentes en una arquitectura de microservicios.
        <ul>
        <li>Microservicio</li>
        <li>Cloud Config.</li>
        <li>Service Discovery.</li>
        <li>Gateway.</li>
        </ul>
    </li>    
    <li>Codificación de la aplicación usando el modelo MVC y la arquitectura de microservicios.</li>
    <li>Desarrolo de una interfaz usando la biblioteca React</li>
    <li>Despliege de la aplicación en aws.</li>
</ul>

<br>


<a name="2"></a>
## Tecnologías de desarrollo

*A continuación se describen las tecnologías que han sido usadas para el desarrollo y despliegue de la aplicación.*

<br>
<br>




## SaaS

<img src="/img/piramidecloud.png" height="261" width="278" align="right"/>
 
Como se puede ver en la figura a la derecha, SaaS forma parte de un conjunto de servicios llamados Servicios cloud, estos <br>
 servicios han cambiado la forma de entender tanto la gestión como el acceso a los recursos informáticos, pues con<br>
 ellos hemos dejado atrás un modelo modelo en el que la única manera de obtener estos recursos era adquiriéndolos<br>
 fisicamente y hacerse cargo de su instalación y mantenimiento y mantenimiento.


Con la aparición de los <b>cloud services</b> el escenario a dado un giro al consumo bajo demanda dónde los recursos <br>
 son consumidos como servicios. El usuario final se desentiende totalmente del mantenimiento y se limíta al uso y<br>
 consumo, volviendose algo intangible para el usuario, que no conoce, ni necesita conocer, la localización física<br>
 de estos recursos (si fuese hardware), o la máquina en la que se está ejecutando (si fuese software).



<b>SaaS</b> por tanto es un modelo de distribución de software en el que se ofrece al usuario un servicio disponible desde <br>
 cualquier dispositivo, pues al estar alojado en la nube sólo se necesita conexión a internet para acceder a este.




<br>
<br>




## Microservicios:


Es una arquitectura para el desarrollo del software en la que una aplicación es formada por distintos servicios
independientes que se despliegan según se vayan necesitando. Con este tipo de arquitectura conseguimos una 
alta escalabilidad y una gran facilidad para la ampliación de funcionalidades, pues al estar la aplicación
compuesta por pequeños servicios que se comunican entre ellos, para añadir uno nuevo no es necesario detener
nada.

A la hora de desplegar una arquitectura de estas características, surgen ciertas problemáticas por la naturaleza
descentralizada de esta. Para dar solución a estos problemas, surgen los siguientes componentes o servicios, que
deberemos de añadir a nuestra aplicación:


  - Cloud Config:
    <br>
        Este servicio nos permitirá centralizar la configuración de todos los servicios en un único repositorio, de esta<br> 
         forma nuestra aplicación será facilmente parametrizable e incluso podremos realizar cambios en caliente.<br>

<img src="/img/microservices.png" height="261" width="350" align="left"/>


  - Service Discovery: 
    <br>
        La arquitectura de microservicios se basa en que cada servicio consuma de otros microservicios, cada uno<br>
         con un número n de instancias desplegadas. Esto significa que un microservicio no puede tener configurado<br>
         una dirección estática indicando en que dirección están los otros microservicios que va a consumir, pues<br>
         cada microservicio va a tener numerosas instancias funcionando con distintas direcciones.
    <br>
    <br>
        Para solucionar este problema se usa el Service Discovery, este servidor almacena las direcciones de cada<br>
         instancia conforme se van desplegando y registra el id del servicio al que pertenecen. De esta forma, cada<br>
         microservicio sólo necesita conocer los id de los microservicios que vaya a consumir y la dirección del<br>
         service discovery, cuando vayan a realizar una comunicación con otro servicio, preguntarán al<br>
         service discovery por la dirección de *x* id y este les devolverá una dirección que en ese<br>
         momento esté siendo usada por el servicio en cuestión.
        
  - Gateway:
    <br>
        Con este definiremos un único punto de entrada a nuestra aplicación, que se encargará de enrutar<br>
         las peticiones externas hacia el microservicio pertinente y de devolver las respuestas.



<br>
<br>



## Spring:

<img src="/img/spring.png" height="261" width="350" align="right"/>

 
Spring es un framework para java que ofrece herramientas con las que podremos construir rápidamente los <br>
 servicios mencionados en el punto anterior. Para cada uno de ellos usaremos las siguientes herramientas<br>
 de Spring:

- **Spring Boot** →  Para construir los microservicios que manejen la lógica de nuestra aplicación.
- **Spring Cloud Config** →  Para construir el Config server.
- **Spring Cloud Netflix Zuul** →  Para construir el Gateway
- **Spring Cloud Netflix Eureka** →  Para construir el Service discover. 


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>



<img src="/img/mongodb.png" height="110" width="200" align="right"/>
<br>

## MongoDB:
MongoDB es una base de datos no relacional, y será la utilizada para almacenar los datos de la aplicación.




<img src="/img/aws.png" height="110" width="100" align="right"/>
<br>

## AWS:
Es una colección de servicios cloud que ofrece amazon, y será donde se realizará el despliegue de la aplicación.




<img src="/img/react.png" height="110" width="400" align="right"/>
<br>

## React:
Es una colección de servicios cloud que ofrece amazon, y será donde se realizará el despliegue de la aplicación.




<img src="/img/nodejs.png" height="110" width="100" align="right"/>
<br>

## Node.Js:
Gestor de paquetes




<br>
<br>

<a name="3"></a>
# Entorno de desarrollo.




<br>
<br>

<a name="4"></a>
# Despliegue de la aplicación.





<a name="5"></a>
# Análisis de la aplicación.



<a name="5.1"></a>
# Requisitos funcionales.



<a name="5.1.1"></a>
## Diagrama de casos de uso.

<br>
<img src="/img/diagramauso.jpg" height="600" width="800"/>
<br>
<br>
<br>


<a name="5.1.2"></a>
## Descripción de casos de uso.


### Descripción: Crear actividad.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_1.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Usuario Identificado.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>Un usuario identificado en el sistema crea una nueva actividad.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>El usuario está identificado en el sistema.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td><p>1. El usuario rellena los datos mínimos necesarios ("Una fecha y un lugar, fecha límite, descripción, título, participativa y pública")".</p>
				<p>2. El usuario agreaga las fechas y lugares extras que desee (hasta un máximo de 5 posibilidades si la actividad se marca como 
				<br>no participativa, y un máximo de 2 en caso de ser marcada como participativa).</p>
				<p>3. El usuario publica la actividad.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>Se crea una nueva actividad.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativa 1:</b></p>
		     <p>El usuario no configura los detalles mínimos.</p>
		</td>
		<td>
			<p>1. El usuario no propone ningún detalle mínimo necesario.</p>
		    <p>2. El usuario agrega los datos extras que desee.</p>
			<p>3. El sistema no permite publicar la actividad.</p>
		</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativa 2:</b></p>
		     <p>El usuario no configura detalles extras.</p>
		</td>
		<td>
			<p>2. El usuario no agrega ninguna opción extra.</p>
			<p>3. El usuario publica la actividad.</p>
		</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativa 3:</b></p>
		     <p>El usuario no publica la actividad.</p>
		</td>
		<td>
			<p>3. El usuario no publica la actividad.</p>
		</td>
 	</tr>
</table>

<br>
<br>


### Descripción: Ver detalles de una actividad.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_2.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Usuario.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>Un usuario ve los detalles de una actividad.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>Ninguna.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td> 	
			<p>1. El usuaio clica en la miniatura de una actividad.</p>
     		<p>2. El sistema muestra los detalles de la actividad en una nueva ventana.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>Se muestran los detalles de una actividad.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativas:</b></p>
		<td>
		     <p>Ninguna.</p>
		</td>
 	</tr>
</table>

<br>
<br>

### Descripción: Unirse a una actividad.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_3.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Usuario.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>Un usuario se une a una actividad.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>El usuario está viendo los detalles de una actividad y está identificado en el sistema.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td>
			<p>1. El usuario clica en "Asistiré".</p>
			<p>2. El usuario se une a la actividad.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>El usuario se une a una actividad.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativas:</b></p>
		</td>
		<td>
			<p>Ninguna.</p>
		</td>
 	</tr>
</table>

<br>
<br>


### Descripción: Buscar una actividad.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_4.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Usuario.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>El usuario busca actividades por título.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>Ninguna.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td>
			<p>1. El usuario introduce en la barra de búsqueda el título que desea buscar".</p>
            <p>2. El sistema muestra una lista con las actividades que tengan un título que contenga el texto buscado.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>Se muestra un listado de actividades.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativas:</b></p>
		</td>
		<td>
		     <p>Ninguna.</p>
		</td>
 	</tr>
</table>

<br>
<br>


### Descripción: Registrarse.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_5.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Usuario.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>Un usuario se registra en el sistema.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>Ninguna.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td>
			<p>1. El usuaio clica en "Registrarse"</p>
			<p>2. El sistema abre una nueva ventana y muestra un formulario de registro.</p>
            <p>3. El usuario rellena el formulario y clica en "Registrarse".</p>
            <p>4. El sistema comprueba los datos introducidos por el usuario.</p>
            <p>5. El sistema registra al usuario.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>El usuario es registrado en el sistema.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativa 1:</b></p>
		     <p>El usuario no rellena el formulario correctamente.</p>
		</td>
		<td>
			<p>5. El sistema lanza un mensaje al usuario "Datos incorrectos".</p>
		</td>
 	</tr>
 		<tr>
  		<td>
		     <p><b>Alternativa 2:</b></p>
		     <p>El usuario introduce un nombre en uso</p>
		</td>
		<td>
			<p>5. El sistema lanza un mensaje al usuario "El nombre ya está en uso".</p>
		</td>
 	</tr>
</table>

<br>
<br>



### Descripción: Identificarse.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_6.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Usuario.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>Un usuario se identifica en el sistema.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>Ninguna.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td>
			<p>1. El usuaio introduce sus credenciales.</p>
            <p>2. El sistema comprueba los datos.</p>
            <p>3. El sistema muestra una pantalla de inicio personalizada con las actividades relacionadas al usuario.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>Se  muestra una pantalla de inicio personalizada con las actividades relacionadas al usuario.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativa 1:</b></p>
		     <p>El usuario no introduce las credenciales correctamente.</p>
		</td>
		<td>
			<p>4. El sistema lanza un mensaje "Nombre de usuario o contraseña incorrectos."</p>
		</td>
 	</tr>
</table>

<br>
<br>



### Descripción: Proponer detalles extras.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_7.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Usuario.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>Un usuario propone detalles extras para una actividad.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>El usuario está identificado en el sistema, apuntado para la actividad a la que va a hacer proposiciones, la organización de la actividad es participativa, y no se ha superado la fécha límite de organización.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td>
			<p>1. El usuario agrega las fechas y lugares extra que desee (un máximo de 2 fechas y 2 lugares).</p>
            <p>2. El usuario confirma las propuestas.</p>
            <p>3. El sistema añade las propuestas a la actividad.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>Se agregan los detalles extras propuestos.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativas:</b></p>
		</td>
		<td>
		     <p>Ninguna.</p>
		</td>
 	</tr>
</table>

<br>
<br>

### Descripción: Votar detalles extras.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_8.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Usuario.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>Un usuario vota detalles extras para una actividad.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>El usuario está identificado en el sistema, apuntado para la actividad en la que va a votar y no se ha superado la fécha límite de organización.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td>
			<p>1. El usuario vota los detalles extras que desee.</p>
            <p>2. El usuario confirma los votos.</p>
            <p>3. El sistema suma los votos.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>Se suman las votaciones realizadas por el usuario.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativas:</b></p>
		</td>
		<td>
		     <p>Ninguna.</p>
		</td>
 	</tr>
</table>

<br>
<br>

### Descripción: Creador borra una actividad.

<table>
	<tr>
		<td><b>Identificador:</b></td>
		<td>CU_9.1</td>
 	</tr>
	<tr>
		<td><b>Actores:</b></td>
		<td>Creador.</td>
 	</tr>
	<tr>
		<td><b>Descripción:</b></td>
		<td>Un usuario creador de una actividad, la cancela.</td>
 	</tr>
 	<tr>
  		<td><b>Precondición:</b></td>
   		<td>El usuario está identificado en el sistema y es el creador de la actividad.</td>
 	 	</tr>
	<tr>
  		<td><b>Secuencia normal:</b></td>
			<td>
			<p>1. El usuario está viendo una actividad.</p>
            <p>2. El pulsa en "Cancelar actividad".</p>
            <p>3. El sistema borra la actividad.</p>
		</td>
 	</tr>
	<tr>
  		<td><b>Postcondición:</b></td>
   		<td>Se elimina la actividad de la base de datos.</td>
 	</tr>
	<tr>
  		<td>
		     <p><b>Alternativas:</b></p>
		</td>
		<td>
		     <p>Ninguna.</p>
		</td>
 	</tr>
</table>

<br>
<br>



<a name="5.2"></a>
# Modelo de objeto de negocios.



<a name="5.2"></a>
# Diagrama de clases.



<br>


<a name="6"></a>
# Diseño de la aplicación

<a name="6.1"></a>
## Modelo de objetos de negocio.


### Diagrama de entidad-relación.

<br>
<img src="/img/er.jpg" height="180" width="750"/>
<br>
<br>
<br>
<br>

<h2>Explicación</h2>

<table>
<tr>
    <td>
        <b>Entidad:</b>
    </td>
    <td>
        Actividad
    </td>
</tr>
<tr>
    <td>
    </td>
    <td>
        Esta entidad representa las actividades que pueden crear y con las que pueden interactuar los usuarios de distintas formas, <br>
            ya sea apuntandose como partícipes, proponiendo nuevos detalles, votando detalles, viendo sus detalles o buscandolas.
    </td>
</tr>
<tr>
    <td>
        <b>Atributos:</b>
    </td>
    <td>
    </td>
<tr>
    <td>
        Cod
    </td>
    <td>
        <p>Codigo único que identifica a la actividad.</p>
    </td>
</tr>
    <td>
        Pública
    </td>
    <td>
        Este atributo será un booleano que nos indicará si la actividad es pública o privada.<br>
        De forma que si es pública puede ser encontrada mediante búsqueda, y si es privada tan sólo<br>
        puede ser accesible a través de una invitación.
    </td>
</tr>
<tr>
    <td>
        Participativa
    </td>
    <td>
        Este atributo será un booleano que nos indicará si la actividad tiene unos detalles cerrados o por<br>
        el contrario está abierta a que los participantes propongan detalles como la fecha, el lugar...
    </td>
</tr>
<tr>
    <td>
        Fecha
    </td>
    <td>
        Fecha en la que se realizará la actividad.
    </td>
</tr>
<tr>
    <td>
        Finalizada
    </td>
    <td>
        Booleano que indica si la actividad a alcanzado la fecha límite marcada.
    </td>
</tr>
<tr>
    <td>
        Fecha Límite
    </td>
    <td>
        En caso de que la actividad sea participativa, este atributo establece la fecha límite para<br>
        realizar propuestas y concretar los detalles.
    </td>
</tr>
<tr>
    <td>
        Descripción
    </td>
    <td>
        Texto que define el objetivo de la actividad.
    </td>
</tr>
</table>

<br>
<br>

<table>
<tr>
    <td>
        <b>Entidad:</b>
    </td>
    <td>
        Usuario
    </td>
</tr>
<tr>
    <td>
    </td>
    <td>
        Esta entidad representa a los usuarios que podran acceder al sistema.
    </td>
</tr>
<tr>
    <td>
        <b>Atributos:</b>
    </td>
    <td>
    </td>
<tr>
    <td>
        Nombre
    </td>
    <td>
        <p>Nombre único que identifica al usuario.</p>
    </td>
</tr>
<tr>
    <td>
        Contraseña
    </td>
    <td>
        <p>Código alfanumérico que permite el acceso a una cuenta de usuario.</p>
    </td>
</tr>
<tr>
    <td>
        E-mail
    </td>
    <td>
        <p>Dirección de correo electrónico de un usuario.</p>
    </td>
</tr>
</table>

<br>
<br>


<table>
<tr>
    <td>
        <b>Relación:</b>
    </td>
    <td>
        Asisten
    </td>
</tr>
<tr>
    <td>
    </td>
    <td>
        Los usuarios pueden asistir a ninguna o varias actividades, de la misma forma que a una actividad pueden<br>
        asistir uno (creador) o varios usuarios.
    </td>
</tr>
<tr>
    <td>
        <b>Atributos:</b>
    </td>
    <td>
    </td>
<tr>
    <td>
        Es creador
    </td>
    <td>
        Este atributo define cual es el usuario creador de la actividad.
    </td>
</tr>
<tr>
    <td>
        Participa lugar
    </td>
    <td>
        Este atributo indica si el usuario ha participado en la actividad votando o añadiendo lugares.
    </td>
</tr>
<tr>
    <td>
        Participa fecha
    </td>
    <td>
        Este atributo indica si el usuario ha participado en la actividad votando o añadiendo fechas.
    </td>
</tr>

</table>

<br>
<br>
<br>
<br>
<br>

<a name="6"></a>



<a name="7"></a>
# Codificación del proyecto.


# Interfaz

<br>

## Pantalla de identificación.

<br>
<img src="/img/login.jpg" height="400" width="750"/>
<br>

## Pantalla de registro.

<br>
<img src="/img/regist.jpg" height="400" width="750"/>
<br>

## Pantalla de actividad detallada.

<br>
<img src="/img/activity.jpg" height="627" width="592"/>
<br>


## Pantalla para la creación de una actividad.

<br>
<img src="/img/newactivity.jpg" height="623" width="992"/>
<br>





<a name="8"></a>
# Pruebas.


<a name="9"></a>
# Detalles técnicos.

<a name="10"></a>
# Problemas durante el desarrollo.



<a name="11"></a>
# Mejoras posibles.

<a name="12"></a>
# Conclusiones..

<a name="13"></a>
# Bibliografia/Webgrafía.

