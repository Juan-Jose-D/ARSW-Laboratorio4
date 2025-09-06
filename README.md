# ARSW-Laboratorio4: Gestión de Planos Arquitectónicos Parte 2

[![Java](https://img.shields.io/badge/Java-17%2B-blue.svg)](https://www.oracle.com/java/)
[![Maven](https://img.shields.io/badge/Maven-Build-brightgreen.svg)](https://maven.apache.org/)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-brightgreen.svg)


## Descripción General

Este proyecto es una aplicación full-stack para la gestión de planos arquitectónicos, desarrollada con **Spring Boot**, **Java 17+**, **Maven**, y un frontend web moderno con **HTML, CSS y JavaScript (jQuery)**. Permite registrar, consultar, filtrar y visualizar planos, así como crear nuevos autores y planos desde la interfaz web.

[https://github.com/ARSW-ECI-archive/SpringBoot_REST_API_Blueprints_Part2](https://github.com/ARSW-ECI-archive/SpringBoot_REST_API_Blueprints_Part2)

---

## Tecnologías y dependencias

- **Backend:** Spring Boot 2.7.18, Java 17+, Maven
- **Frontend:** HTML5, CSS3, Bootstrap, jQuery
- **Pruebas:** JUnit 4
- **Persistencia:** En memoria (sin base de datos)

---

## Estructura del Proyecto

```
├── src/
│   ├── main/
│   │   ├── java/edu/eci/arsw/blueprints/
│   │   │   ├── controllers/           # Controladores REST
│   │   │   ├── model/                 # Entidades: Blueprint, Point
│   │   │   ├── persistence/           # Interfaces y persistencia en memoria
│   │   │   ├── services/              # Servicios y filtros
│   │   │   └── ui/                    # No se usa actualmente
│   │   └── resources/
│   │       ├── public/                # Frontend web (index.html, js, css)
│   │       └── applicationContext.xml # Configuración Spring
│   └── test/
│       └── java/edu/eci/arsw/blueprints/test/persistence/impl/
│           ├── InMemoryPersistenceTest.java
│           └── BlueprintFilterTest.java
├── pom.xml
├── README.md
├── img/                              # Diagramas y capturas
└── model.uml
```

---

## Instalación y Ejecución

### Requisitos
- Java 17 o superior
- Maven

### Backend (Spring Boot)
1. Instala dependencias y compila:
	```bash
	mvn clean package
	```
2. Ejecuta el backend:
	```bash
	mvn spring-boot:run
	```

### Frontend (Web)

Al ejecutar el backend el front estará disponible en `http://localhost:8080`.

---

## Funcionalidades

- **Registrar planos:** Desde la web, puedes crear nuevos planos y autores.
- **Consultar planos:** Buscar planos por autor.
- **Visualizar planos:** Ver los puntos del plano en un canvas interactivo.
- **Listar autores:** Ver todos los autores registrados y sus planos.
- **Filtrar planos:** El backend aplica filtros antes de retornar los datos.
- **Persistencia en memoria:** Los datos se almacenan temporalmente en memoria, sin base de datos.

---


## Uso de la Interfaz Web

1. **Listar autores:** Haz clic en "List all authors" para ver los autores disponibles.
2. **Consultar planos:** Ingresa el nombre de un autor y haz clic en "Get blueprints" para ver sus planos.
3. **Visualizar plano:** Haz clic en "Open" en la tabla para ver el plano en el canvas.
4. **Crear plano:** Completa el formulario y haz clic en "Create Blueprint". El formato de puntos es `x1,y1;x2,y2;...`.


![alt text](/img/image.png)

![alt text](/img/image-1.png)

---


## Filtros de Planos

El backend aplica uno de dos filtros configurables:
- **Redundancia:** Elimina puntos consecutivos repetidos.
- **Submuestreo:** Elimina 1 de cada 2 puntos.

### ¿Cómo alternar el filtro?
En el archivo `BlueprintsServices.java`, la inyección del filtro se realiza con:
```java
@Autowired
public BlueprintsServices(BlueprintsPersistence bpp,
	@Qualifier("redundancyFilter") BlueprintFilter blueprintFilter) {
	this.bpp = bpp;
	this.blueprintFilter = blueprintFilter;
}
```
Para usar el filtro de submuestreo, cambia el qualifier a:
```java
@Qualifier("subsamplingFilter")
```
Guarda el archivo y reinicia el back para aplicar el cambio.

### Uso desde la web
Al consultar planos desde la interfaz web, el filtro configurado en el backend se aplica automáticamente a los datos retornados y visualizados.

---

## Pruebas

Ejecuta las pruebas unitarias con:
```bash
mvn test
```
Incluyen pruebas de persistencia y de los filtros.

---




## Créditos y Autor

**Autor:** Juan José Díaz ([github](https://github.com/Juan-Jose-D))

**Institución:** Escuela Colombiana de Ingeniería Julio Garavito
