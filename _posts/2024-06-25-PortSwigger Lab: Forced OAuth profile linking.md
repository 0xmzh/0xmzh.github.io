---
title: PortSwigger Lab - Forced OAuth profile linking
categories: [Web Hacking, Pentesting]
tags: [csrf, web, pentesting, burpsuite]     # TAG names should always be lowercase
author: [author_id]    
description: CSRF en OAuth.

---

[PortSwigger Lab: Forced OAuth profile linking](https://portswigger.net/web-security/oauth/lab-oauth-forced-oauth-profile-linking)

![Desktop View](assets/img/20240614114943.png){: width="700" height="400" }

Este laboratorio te da la opción de adjuntar un perfil de redes sociales a tu cuenta para que puedas iniciar sesión a través de OAuth en lugar de utilizar el nombre de usuario y la contraseña normal. Debido a la implementación insegura del flujo OAuth por parte de la aplicación cliente, un atacante puede manipular esta funcionalidad para obtener acceso a las cuentas de otros usuarios.

Menciona que para resolver el lab utilizemos un ataque CSRF para adjuntar nuestro perfil de redes sociales a la cuenta del usuario admin en el sitio web, luego que accedamos al panel de administración y eliminemos al user llamado "carlos".

## CSRF

La vulnerabilidad Cross-Site Request Forgery permite a un atacante forzar a los usuarios a realizar acciones que no tenían intención de realizar. Por ejemplo esto puede permitir al atacante cambiar la dirección de correo electrónico de la víctima y utilizar el restablecimiento de la contraseña para hacerse con el control de la cuenta.

![Desktop View](assets/img/csrf.png){: width="700" height="400" }

Accedemos al laboratorio y nos logueamos con nustras creds `wiener:peter`

En el perfil de nuestra cuenta hay un link que permite vincular nuestra red social con la cuenta.
(necesitaremos loguearnos a la social media para que podamos vincularla, las creds son:  `winer.peter:hotdog` )

![Desktop View](assets/img/20240614134842.png){: width="700" height="400" }

le damos a Attach a social profile e interceptamos la request con burp suite.

copiamos la request y le hacemos un drop para cancelar la peticion.

![Desktop View](assets/img/20240614140254.png){: width="700" height="400" }

En nuestro exploit server agregamos el siguiente codigo javascript que va hacer que se vincule nuestra red social con la cuenta del usuario que le de click, luego lo enviamos a la victima(Deliver exploit to victim).

![Desktop View](assets/img/20240614141048.png){: width="700" height="400" }

Nos deslogueamos y volvemos a acceder, pero esta vez utilizamos el login via social media y si todo salió correcto estaremos como admin, ya como administrador podremos eliminar el usuario carlos. 

![Desktop View](assets/img/20240614141131.png){: width="700" height="400" }
![Desktop View](assets/img/20240614141207.png){: width="700" height="400" }


