---
title: Recuperación de Información 🌺
---
# 9 Noviembre 2022 🍄

- Los buscadores ofrecen respuestas a preguntas. Explotan grafos de conocimiento para dar datos rápidamente
- La **recuperación de información** es el estudio y desarrollo de sistemas automatizados para que una persona pueda saber si hay información que satisfaga sus necesidades. Dicha información ha de estar ordenada.
- **Documento**: cualquier texto que seamos capaces de escribir
- **Colección**: conjunto de documentos que esperamos que satisfagan una necesidad de información
- **Búsqueda *ad hoc***: la persona tiene en mente una necesidad específica y formula una consulta personalizada que será ordenada según su relevancia por el sistema de recuperación de información
- **Consulta**: expresión que una persona construye para formular su necesidad de información

## Modelo conceptual de Recuperación de información
![](img/modelo%20conceptual.png|300)

**RI y SGBD** difieren en:
- los elementos que almacenan
- las consultas que aceptan
- la forma en que hacen el matching entre elementos y consultas
- los resultados que retornan

**RI**
- Almacenan textos escritos en lenguaje natural con poca o ninguna estructura y cuya semántica es totalmente ajena al sistema
- texto libre
- retornan resultados aproximados
- retornan resultados ordenados
**SGBD**
- Datos muy estructurados con distintos campos con una semántica bien definida
- lenguajes artificiales
- retornan coincidencias exactas
- retornan todos los ítems que hacen match con una consulta concreta y no necesitan estar ordenados

## Procesamiento de documentos
- tokenización
- se van a eliminar las palabras vacías

---
# 17 Noviembre 2022 🦾

## Normalización
- Se refiere a aquellos procesos que persiguen mejorar el matching de términos aunque no sean la misma secuencia exacta de caracteres -> hola/hi/chao
- Al proceso de convertir todo a minúsculas se le conoce como **case-folding**

---