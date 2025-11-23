# Writeup Meow machine HTB

## Introducción

En esta entrada vamos a resolver la máquina **Meow** de HackTheBox, una de las más básicas y perfectas para empezar a calentar motores en el mundo del pentesting. Vamos a ir paso a paso: primero responderemos al **cuestionario inicial**, luego realizaremos la **enumeración**, encontraremos el vector de acceso y finalmente obtendremos la **flag**. Todo explicado de forma sencilla para que cualquiera pueda seguir el proceso sin perderse.

## Resolución de la máquina

Lo primero que hago siempre antes de empezar a enumerar es comprobar si la máquina la podemos ver. Para ello, simplemente le hago un **ping** a la IP que nos da HackTheBox. Tal y como se ve en la captura, la máquina responde correctamente, así que sabemos que está activa y accesible desde nuestra VPN. Con eso confirmado, ya podemos pasar a la siguiente fase: **enumerar puertos y servicios** para ver qué está ofreciendo la máquina y por dónde podemos empezar a trabajar.

`ping 10.129.26.246`

Para empezar con la enumeración de puertos, lanzo un **nmap -sV** contra la IP de la máquina. Con este escaneo obtenemos qué puertos están abiertos y qué servicios están corriendo en cada uno.

En los resultados  aparece el **puerto 23** abierto, que corresponde al servicio **Telnet**. Este servicio es antiguo, inseguro y transmite todo en claro, así que suele ser un vector bastante evidente para empezar. Con esa información, ya tenemos un punto de entrada claro: **vamos a atacar la máquina a través de Telnet**.

`sudo nmap -sV 10.129.26.246`

A veces, por malas configuraciones o por pura pereza, algunas (realmente muchas…) cuentas importantes en un sistema pueden quedar con la **contraseña en blanco**. Esto sigue ocurriendo en muchos dispositivos de red y en máquinas básicas, lo que las deja expuestas a ataques ridículamente simples: probar a iniciar sesión con usuarios comunes sin poner ninguna contraseña.

Las cuentas típicas que siempre merece la pena probar primero son las de toda la vida:

- **root**

- **admin**

- **administrator**

En servicios inseguros como **Telnet**, donde todo va en claro, basta con introducir uno de estos nombres de usuario cuando el sistema lo pide y pulsar *Enter* sin escribir ninguna contraseña.

En mi caso, he probado con **root**… y mágicamente hemos accedido :)

![]([/home/oxy/.config/marktext/images/2025-11-23-17-12-11-image.png](https://xanross.com/wp-content/uploads/2025/11/image.png))

Como se ve en la captura, una vez dentro lanzo un **ls** para listar el contenido del directorio. Ahí aparece un archivo llamado **flag.txt**, que obviamente es el objetivo principal de esta máquina. Al abrirlo, encontramos la **bandera**, así que ya habríamos completado la máquina **Meow** de HTB sin ninguna complicación.

Con la flag obtenida, ya podemos ir directos a rellenar el **cuestionario** y dar la máquina por finalizada.

![]([/home/oxy/.config/marktext/images/2025-11-23-17-12-47-image.png](https://xanross.com/wp-content/uploads/2025/11/image-1.png))

## Cuestionario

- What does the acronym VM stand for?
  
  `virtual machine`

- What tool do we use to interact with the operating system in order to issue commands via the command line, such as the one to start our VPN connection? It's also known as a console or shell.
  
  `terminal`

- What service do we use to form our VPN connection into HTB labs?
  
  `openvpn`

- What tool do we use to test our connection to the target with an ICMP echo request?
  
  `ping`

- What is the name of the most common tool for finding open ports on a target?
  `nmap`

- What service do we identify on port 23/tcp during our scans?
  
  `telnet`

- What username is able to log into the target over telnet with a blank password?
  
  `root`

- Submit root flag
  
  `b40abdfe23665f766f9c61ecba8a4c19`

## Conclusión

La máquina **Meow** es un clásico para quienes empiezan en HackTheBox: muy sencilla, pero ideal para interiorizar dos ideas clave en cualquier pentest. La primera es que la **enumeración** lo es todo; incluso en máquinas fáciles, identificar correctamente los servicios y sus configuraciones marca la diferencia. La segunda es recordar que muchos sistemas siguen siendo vulnerables simplemente por **credenciales por defecto o contraseñas en blanco**, algo más común de lo que debería.

En este caso, bastó con revisar los puertos, encontrar un servicio inseguro como **Telnet** y probar cuentas típicas sin contraseña. A partir de ahí, obtener la flag fue trivial. Aun así, es un buen ejercicio para familiarizarse con la metodología básica que luego se aplica en máquinas más avanzadas.

## Bibliografía

- HackTheBox – Máquina **Meow**  
  [https://app.hackthebox.com](https://app.hackthebox.com)

- Documentación oficial de **nmap**  
  [Chapter 15. Nmap Reference Guide | Nmap Network Scanning](https://nmap.org/book/man.html)

- RFC 854 – *Telnet Protocol Specification*  
  https://datatracker.ietf.org/doc/html/rfc854

- Cheat Sheet de Linux (comandos básicos)  
  [Command-line shell - ArchWiki](https://wiki.archlinux.org/title/Command-line_shell)

- Guía básica de enumeración en pentesting  
  https://owasp.org/www-project-testing/


