---
title: "SERVIDOR DE CORREO LINUX (Postfix + Dovecot + SSL)"
description: Configurar un servidor de correo en Linux con Postfix y Dovecot, permitiendo envío interno y externo de correos con seguridad SSL/TLS.
pubDatetime: 2026-01-18T10:00:00Z
tags:
  - postfix
  - dovecot
  - linux
  - thunderbird
  - virtualbox
draft: false
---

Implementación de un servidor de correo electrónico sobre Linux utilizando Postfix y Dovecot. El proyecto incluye la configuración de servicios SMTP e IMAP, gestión de usuarios locales, cifrado SSL/TLS y pruebas de comunicación entre cuentas para comprender el funcionamiento de una infraestructura de correo empresarial.


## Tabla de Contenidos

## Shell: Instalación de servicios

Antes de instalar cualquier servicio, se actualizaron los repositorios de Ubuntu para garantizar que los paquetes descargados fueran las versiones más recientes disponibles.

```bash
sudo apt update
```
<figure>
  <img
    src="/Terminal.png"
    alt="Actualizar paquetes de linux"
  />
  <figcaption class="text-center">
   Paquetes actualizados
  </figcaption>
</figure>



## Instalar Postfix y Dovecot

```bash
sudo apt install postfix dovecot-imapd dovecot-pop3d -y
```

<figure>
  <img
    src="/postfixInstall1.png"
    alt="Configuracion de Postifx"
  />
  <figcaption class="text-center">
    Instalacion de Postfix
  </figcaption>
</figure>

<figure>
  <img
    src="/postfixInstall2.png"
    alt="Segunda Pantalla de Configuracion de Postifx"
  />
  <figcaption class="text-center">
    Segunda Pantalla de Instalacion de Postfix
  </figcaption>
</figure>

<figure>
  <img
    src="/postInst3.png"
    alt="Segunda Pantalla de Configuracion de Postifx"
  />
  <figcaption class="text-center">
    Segunda Pantalla de Instalacion de Postfix
  </figcaption>
</figure>

<figure>
  <img
    src="/PostfixInstalado.png"
    alt="Instalacion terminada de Postfix"
  />
  <figcaption class="text-center">
    Instalacion Exitosa de Postfix
  </figcaption>
</figure>


## Verificación de servicios
```bash
systemctl status postfix
systemctl status dovecot

```
<figure>
  <img
    src="/postfixEnable.png"
    alt="Postfix habilitado"
  />
  <figcaption class="text-center">
    Postfix habilitado
  </figcaption>
</figure>

<figure>
  <img
    src="/DovecotEnable.png"
    alt="Dovecot habilitado"
  />
  <figcaption class="text-center">
    Dovecot habilitado
  </figcaption>
</figure>


## Creación de usuarios locales

```bash
sudo adduser usuario1
sudo adduser usuario2
sudo passwd usuario1
sudo passwd usuario2
```
## Configuración de Postfix

```bash
sudo nano /etc/postfix/main.cf
```
<figure>
  <img
    src="/ConfiguracionPostfix.png"
    alt="Configuracion Postfix"
  />
  <figcaption class="text-center">
   Se configuró Postfix para escuchar conexiones de red y no únicamente localhost. Se modificó el parámetro inet_interfaces = all. También se configuró el dominio local empresa.local.
  </figcaption>
</figure>


## Reinicio del servicio

```bash
sudo systemctl restart postfix
```
## Configuración de Dovecot
```bash
sudo nano /etc/dovecot/dovecot.conf
```

Se realizaron ajustes de autenticación para que los usuarios Linux pudieran acceder a sus buzones mediante IMAP.

## Configuración de Thunderbird

Se configuró Thunderbird como cliente de correo utilizando las credenciales de los usuarios Linux.



<figure>
  <img
    src="/Thunderbird1.png"
    alt="Actualizar paquetes de linux"
  />
  <figcaption class="text-center">
   
  </figcaption>
</figure>


<figure>
  <img
    src="/Thunderbird2.png"
    alt="Actualizar paquetes de linux"
  />
  <figcaption class="text-center">
   
  </figcaption>
</figure>



<figure>
  <img
    src="/Thunderbird3.png"
    alt="Actualizar paquetes de linux"
  />
  <figcaption class="text-center">
   
  </figcaption>
</figure>





<figure>
  <img
    src="/Thunderbird4.png"
    alt="Actualizar paquetes de linux"
  />
  <figcaption class="text-center">
   
  </figcaption>
</figure>




<figure>
  <img
    src="//Thunderbird5.png"
    alt="Actualizar paquetes de linux"
  />
  <figcaption class="text-center">
   
  </figcaption>
</figure>


<figure>
  <img
    src="//Thunderbird6.png"
    alt="Actualizar paquetes de linux"
  />
  <figcaption class="text-center">
   
  </figcaption>
</figure>




> El laboratorio permitió comprender el funcionamiento de una infraestructura de correo basada en Linux, incluyendo instalación de servicios, administración de usuarios, autenticación, protocolos SMTP e IMAP y pruebas reales de comunicación entre cuentas locales.
