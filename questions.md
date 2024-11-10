### ¿Qué pasa si no hago el link simbólico entre sites-available y sites-enabled de mi sitio web?

Lo que ocurriría basicamente es que a la hora de nginx servir paginas al cliente que se conecte no serviria tu sitio web puesto que no esta dado de alta como sitio permitido en sites-enabled. Con el link simbolico estamos dandolo de alta en sitios permitidos por nginx.

### ¿Qué pasa si no le doy los permisos adecuados a /var/www/nombre_web?
Que no te dejará acceder a la pagina web, y por lo tanto te pedira un nombre y una contraseña para que te identifiques y saber si eres un usuario que esta autorizado para ver las paginas que te va a servir. en caso de fallar al pedirte nombre y contraseña te mostrara una pagina en blanco con un mensaje de "Unauthorized" que indica que no estas autorizado para ver el contenido de la pagina web.