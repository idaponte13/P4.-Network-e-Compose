# P4.-Network e compose

**1. Crear unha rede en docker**

Para crear unha rede en docker poñemos o comando `docker network create <nome da red>`. 

**2. Crear dous contenedores unidos a esa rede**

Para crear dous contenedores debemos facer o comando `docker run -dit --name <nome do contenedor> --network <nome da rede> <nome da imaxe>`.  

**3. Comprobar que os contenedores están na rede**

Para comprobar que ambos contenedores estan na rede debemos facer o seguinte comando ```docker network inspect iago_rede```. 

**4. Comprobar que os contenedores poden verse entre eles**  

Para facer este paso poden xurdir problemas como que o comando ping non esté instalado.  
Para solucionalo, debemos poñer na terminal do contenedor que acabamos de abrir o comando ```apt update```  e posteriormente ```apt install -y iputils-ping```.    
Unha vez na terminal dun contenedor facemos o comando ```ping contenedor2``` neste caso "contenedor" xa que este é o nome dado ao segundo contenedor e se vai todo correcto, deberian conectarse.

**5. Listar os contenedores conectados á rede**

Para listar os contenedores debemos poñer o comando ```docker network inspect iago_rede```.     
No mensaxe da terminal, na sección de "Containers", poderanse ver os contedores conectados a esa rede.

**6. Listar as propiedades da rede**

As propiedades da rede pódense ver usando o mesmo comando que no paso anterior ```docker network inspect iago_rede```.

**7. Crea outra rede**

Para crear outra rede facemos o mesmo que no primeiro paso ```docker network create <nome da red>```.  

**8. Lanza dous contenedores novos conectados a esa nova rede**

Para facer este apartado escribiremos o mesmo comando que no apartado 2 cambiando unicamente os nomes e a rede á que está conectada.

**9. Comproba as posibles conexións entre os 4 contenedores**

Como se fixo no punto 4, debemos facer ping entre todos os contenedores.Primeramente faremolo na terminal do "contenedor1".      
Facemos o comando ```ping contenedor2``` e como está na mesma rede pode conectarse.  
Logo facemos o ping ao contenedor 3 e neste caso non se encontran xa que o contenedor 3 xunto co contenedor 4 estan na rede iago_rede2, é dicir, a segunda rede que creamos anteriormente.  

Para comprobar se o contenedor 3 e 4 poden facerse ping mutuamente realizaremolo dende calquera das terminais destes e comprobaremos que ao contenedor 1 e 2 da erro pero ao 4 non.

**Docker compose:**

**1. Segue os pasos da guía de iniciación de docker-compose, e explica coas túas palabras os pasos que segues e qué fan**

O primeiro que se fai é crear un directorio que será utilizado para gardar tanto a páxina web, como os requerimentos como a posterior instalación destes.  
O segundo que imos facer é crear o documento ```app.py``` onde se aloxará o código que ensina cómo crear unha aplicación web simple en Python utilizando Flask, e cómo interactuar con unha base de datos Redis para almacenar un contador de visitas que persiste entre solicitudes. É un exemplo sinxelo en Docker para amosar cómo conectar múltiples servizos.  
E por último faremos un ```docker compose up``` o cal é utilizado para iniciar e administrar a aplicación.

**2. Agora que sabes algo máis de docker-compose, crea un arquivo (ou varios arquivos) de configuración que ó ser lanzados cun docker-compose up, resulten nunha rede docker á que estean conectados 3 contenedores, explica os parámetros do .yaml usado**

Os parametros utilizados neste comando son os seguinte:
- nome do contenedor.
- image: para definir a imaxe utilizada.  
- container name: onde se especificará o nome do contenedor.  
- netwotks: onde escribiremos o nome da rede.    

**3. Busca e proba 4 parámetros e configuracións diferentes que podes incluir no arquivo compose, explica qué fan. (por exemplo diferentes cousas que facer coa opción RUN)**

Primeiro de todo falremos do parámetro ```environment```, o cal permite establecer variables de contorno para un contenedor.  
O segundo do cal falaremos será ```volumes```, este monta un directorio no contenedor acutal para que o código esté disponible.   
Posteriormente o parámetro ```ports```, para o mapeado dos portos.  
E por ultimo veremos o parámetro ```depends_on```, este define dependencias entre servizos, é dicir, especifica que contenedores deben estar activos antes de que se inicie un servicio en concreto.