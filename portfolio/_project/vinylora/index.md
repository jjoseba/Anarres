---
layout: work
title: Vinylora
order: 5
permalink: /portfolio/vinylora/
gallery_folder: /portfolio/vinylora/
tags: [web, diseño, woocommerce, backend, python ]
external_link: https://vinylora.com/
external_text: Ver página web
description: |
    diseño de marca y desarrollo de una web y tienda online (con integración con el inventario y extracción de portadas de discos) para una tienda de vinilos en el centro de Vitoria-Gasteiz.
---

Vinylora es un proyecto de autoempleo en el que se han embarcado dos hermanos amantes de la música, con la idea de reivindicar el formato físico y disfrutar la música desde el sosiego. Les acompañé en un proceso colaborativo en el diseño del logotipo y la marca y cómo aplicarla en el local y redes sociales.

Desarrollamos una web principal un Wordpress aplicando el mismo diseño de marca y tratando de capturar el espíritu con el que se abrió la tienda. Para la parte de venta online utilizamos el módulo WooCommerce para el que hubo que configurar varios plugins adicionales para integrar los procesos de la tienda: el catálogo de la tienda online está sincronizado con el inventario del software de gestión que se utiliza en la tienda física, y se reciben notificaciones en la tienda cada vez que se hace una compra a través de la web. Una vez se cierra un pedido, si va a ser un envío a domicilio a través del propio panel de la web se puede gestionar con la empresa de mensajería el coste y los detalles del envío.

![Web responsive]({{site.baseurl}}/assets/img/static/vinylora-mockups.jpg "Web responsive"){: .mtop .mbottom}

Como el flujo de entrada y salida de vinilos y CDs es muy grande, un trabajo costoso para mostrar el catálogo de música en la tienda online es actualizar cada elemento con su imagen de portada. Para evitar tener que realizarlo de forma manual, se desarrolló un script de Python que obtiene el catálogo público y extrae las imágenes de cada carátula utilizando la API pública de Discogs [Discogs](https://www.discogs.com/developers). 

El script de Python para el procesamiento de las carátulas está liberado en GitHub como software libre bajo licencia GPLv3.
