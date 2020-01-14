---
layout: page
title: Contacta
sidebar_link: true
permalink: /contact/
sidebar_sort_order: 3
show_wave: true
---

¿Se te ocurre que podamos colaborar de alguna manera? ¿Tienes algún proyecto en mente en el que crees que podría serte de ayuda? Escríbeme contándome un poco y me pondré en contacto de vuelta en cuanto lo lea!


<form action="https://getsimpleform.com/messages?form_api_token=615f2d6dcb943d333e3cf30acb8a77eb" method="post">
  <!-- the redirect_to is optional, the form will redirect to the referrer on submission -->
  <input type="hidden" name="redirect_to" value="{{site.url}}/contact_success/" />
  <!-- all your input fields here.... -->
  <label for="nombre">_nombre <i class="fas fa-user-astronaut"></i></label>
  <input type="text" name="nombre" />

  <label for="email">_email <i class="far fa-envelope"></i></label>
  <input type="email" name="email" />

  <label for="titulo">_título <i class="far fa-sticky-note"></i></label>
  <input type="text" name="titulo" />

  <label for="mensaje">_mensaje <i class="fas fa-pen-fancy"></i></label>
  <textarea name="mensaje" rows="8"></textarea> 

  <input type="submit" value="enviar" />
</form>

