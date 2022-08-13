Apache Benchmark
 

rver:~# ab -k -n1000 -c100 -H 'Accept-Encoding: gzip,deflate' http://www.example.com.ve/sitio/
Donde:
-k (KeepAlive). Realizar múltiples solicitudes dentro de una sesión HTTP, funcionalidad de los navegadores por la naturaleza
-n (requests). Número total de solicitudes para ejecutar
-c (concurrency). Cantidad de conexiones concurrentes
-H ‘Accept-Encoding: gzip,deflate’ (custom-header). Anexar encabezados adicionales a la solicitud. Imita la peticiones típica que un navegador enviará