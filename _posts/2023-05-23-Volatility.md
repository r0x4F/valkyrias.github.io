---
layout: post
title: Análisis de memoria con Volatility
subtitle: 
author: Lu
categories: "MemoryForensics"
banner:
  image: https://th.bing.com/th/id/OIP.pswcGUeOkJ9e9dNtV6Ka1QAAAA?pid=ImgDet&rs=1
  opacity: 0.618
  background: "#000"
  height: "100vh"
  min_height: "38vh"
  heading_style: "font-size: 4.25em; font-weight: bold; text-decoration: underline"
  subheading_style: "color: gold"
tags: volatility forensics memory 
top: 1
sidebar: []
---

En esta primera publicación de la categoría, se ha pensado en dar una pequeña guía de introducción a una herramienta muy usada en análisis de memoria RAM: Volatility.

Este post va a ser de un nivel muy introductorio, por lo que no es necesario tener conocimientos previos más allá de un uso mínimo de la instalación de paquetes, clonación de repositorios desde Github y uso de scripts en Python. Igualmente, las instrucciones vendrán detalladas y se proporcionarán los comandos necesarios para que todo transcurra sin problemas ni complicaciones.

Pero primero, daremos algo más de información sobre la herramienta.

## ¿Qué es Volatility?

Volatility es un framework de análisis forense especializado en la extracción de artefactos desde una captura de memoria RAM provenientes de sistemas operativos Windows, MacOS y diversas distribuciones Linux tanto de 64 como de 32 bits.

Se presenta en dos versiones: Volatility 2 y Volatility 3.

### Volatility 2

Está escrito en Python 2, por lo que será necesaria la instalación de Python 2.7. Además, también cabe destacar que no es compatible con las versiones más recientes de los sistemas operativos (soporta hasta Mac OSX 10.15.x Catalina, Windows 10 v10.0.19041 y versiones que usen el kernel v5.5 de Linux). Sin embargo, tiene varias funcionalidades que aún no se encuentran disponibles en Volatility 3, por lo que, a pesar de que su desarrollo está prácticamente discontinuado, si la captura de memoria objetivo se encuentra dentro del rango soportado, se recomienda instalar ambas versiones de Volatility.

### Volatility 3

Es la versión más reciente. Mantiene soporte con las versiones más recientes de los sistemas operativos y, en un futuro, tendrá disponibles todas las funcionalidades de v2.

A continuación, se detallarán los comandos para la instalación en una distribución Linux de la familia Ubuntu. Sin embargo, en otras distribuciones y en Windows el proceso es muy similar, por lo que solo será necesario realizar pequeñas adaptaciones.

## Preparaciones

Para instalar tanto la versión 2 como la versión 3 de Volatility, se realizarán ciertas preparaciones previas.

### Variables

Primero, definiremos la ruta base donde se instalarán los recursos necesarios. En mi caso he usado `“/home/$USER/programs/volatility”`, aunque podéis modificar $VOLATILITY_HOME para que contenga la ruta de cualquier carpeta válida, recomendando el uso de rutas absolutas.

`$VOLATILITY2_HOME` será la carpeta raíz de la instalación de Volatility2, de la misma manera que lo será `$VOLATILITY3_HOME` con v3.

$PY2ENV será la ruta a un entorno virtual de Python 2 que crearemos para evitar conflictos con otras versiones de paquetes.

Si queremos mantener las variables y alias que definiremos a continuación de manera permanente y no solo para la sesión y terminal actual, añadiremos al archivo /etc/enviroment (o ~/.profile si solo se quiere aplicar al usuario actual) las siguientes variables con el valor deseado.

- `VOLATILITY_HOME="/home/os/volatility"`
- `VOLATILITY2_HOME="/home/os/volatility/volatility" PY2ENV="/home/os/volatility/python2env"`
- `VOLATILITY3_HOME="/home/os/volatility/volatility3"`