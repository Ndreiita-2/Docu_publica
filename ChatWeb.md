# 1. CHATBOT WEB CON CHATWOOT

Mi Chatwoot está instalado en una máquina virtual con Ubuntu y docker. La página WEB que estoy usando de pruebas, está en internet mediante Visual Studio Code con la herramienta de Live Server.

## 1.1 Crear Inbox Website

Chatwoot:

Settings → Inboxes → Add Inbox → Website

<img width="953" height="549" alt="Image" src="https://github.com/user-attachments/assets/f3072f85-0da5-408f-8ec2-0c3c866be818" />


Una vez el inbox creado, vamos a su configuración, arriba donde pone Settings, metemos en Website Domain la URL de nuestra WEB:


<img width="1404" height="932" alt="Image" src="https://github.com/user-attachments/assets/630c8e6c-574c-4891-9b78-dd9e83a36b46" />

Copiar Website Token.

---

## 1.2 Insertar Script en la Web

A la derecha, en Configuration, encontramos el script que va a ir en el HTML de nuestra WEB. Debe contener:

- URL de nuestro Chatwoot
- Token que nos da Chatwoot

<img width="1385" height="941" alt="Image" src="https://github.com/user-attachments/assets/f76693b0-8a89-4fbd-bfc1-05c6091de1d5" />

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

<img width="1912" height="977" alt="Image" src="https://github.com/user-attachments/assets/77202e1d-4578-455e-81d7-8c821e48b018" />

<img width="471" height="761" alt="Image" src="https://github.com/user-attachments/assets/e45c4551-1645-4e56-9a96-b8b5ba9a9649" />


# 2. ¿Y con módulos para Magento?

## Estructura básica del módulo

Dentro de Magento:

```
app/code/TuEmpresa/Chatwoot/
├── registration.php
├── etc/module.xml
└── view/frontend/layout/default.xml
```

---

## Registrar el módulo

### `registration.php`

```php
<?php
use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'TuEmpresa_Chatwoot',
    __DIR__
);
```

---

### `etc/module.xml`

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="TuEmpresa_Chatwoot" setup_version="1.0.0"/>
</config>
```

---

## Insertar el script (la clave)

### `view/frontend/layout/default.xml`

Esto hace que el script se cargue en todo el frontend:

```xml
<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 layout="1column"
 xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    
    <body>
        <referenceContainer name="before.body.end">
            <block class="Magento\Framework\View\Element\Template"
                   name="chatwoot.script"
                   template="TuEmpresa_Chatwoot::chatwoot.phtml"/>
        </referenceContainer>
    </body>
</page>
```

---

## Crear el template con tu script

### `view/frontend/templates/chatwoot.phtml`

Aquí metes EXACTAMENTE el mismo script que ya usaste:

```php
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

## Activar el módulo

```bash
bin/magento setup:upgrade
bin/magento cache:flush
```
