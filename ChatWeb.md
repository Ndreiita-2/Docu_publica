INFORMACIÓN ADICIONAL -> Mi Chatwoot está instalado en una máquina virtual con Ubuntu y docker. La página WEB que estoy usando de pruebas, está en internet mediante Visual Studio Code con la herramienta de Live Server.

# 1. CHATBOT WEB CON CHATWOOT

## 1.1 Crear Inbox Website

Chatwoot:

Settings → Inboxes → Add Inbox → Website

<img width="953" height="549" alt="Image" src="https://github.com/user-attachments/assets/61064062-ad5f-4044-942e-a0abace32406" />


Una vez el inbox creado, vamos a su configuración, arriba donde pone Settings, metemos en Website Domain la URL de nuestra WEB:

<img width="1404" height="932" alt="Image" src="https://github.com/user-attachments/assets/f783d13a-48a5-4b8a-9514-6e0e6dba3956" />

Copiar Website Token.

---

## 1.2 Insertar Script en la Web

A la derecha, en Configuration, encontramos el script que va a ir en el HTML de nuestra WEB. Debe contener:

- URL de nuestro Chatwoot
- Token que nos da Chatwoot

<img width="1385" height="941" alt="Image" src="https://github.com/user-attachments/assets/c39abf87-ce90-412a-b1c3-127d6f7e28f7" />

Lo añadimos en nuestra WEB, antes del cierre de body:

```html
<script>
(function(d,t) {
  var BASE_URL="https://chat.midominio.com";
  var g=d.createElement(t),s=d.getElementsByTagName(t)[0];
  g.src=BASE_URL+"/packs/js/sdk.js";
  s.parentNode.insertBefore(g,s);
  g.onload=function(){
    window.chatwootSDK.run({
      websiteToken: 'TOKEN_AQUI',
      baseUrl: BASE_URL
    })
  }
})(document,"script");
</script>
```
---

En la WEB, debería de quedar así:

<img width="1912" height="977" alt="Image" src="https://github.com/user-attachments/assets/4e29297e-75e9-4355-857a-94d3a353b785" />

<img width="471" height="761" alt="Image" src="https://github.com/user-attachments/assets/dd9b8c99-d454-45c2-b921-7a41e513dabe" />
