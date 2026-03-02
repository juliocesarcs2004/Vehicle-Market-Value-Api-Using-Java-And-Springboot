# 🚗 Vehicle Market FIPE API -- Spring Boot CLI Application

Java Spring Boot backend application to query and display average
vehicle prices (cars, motorcycles, and trucks) based on the official
FIPE public API.

------------------------------------------------------------------------

## 📌 Overview

This project is a command-line Spring Boot application that allows users
to consult average vehicle prices using the FIPE public API.

The application reproduces and improves the official FIPE website flow
by:

-   Allowing vehicle type selection (car, motorcycle, truck)
-   Listing brands dynamically from the API
-   Listing models by selected brand
-   Filtering models by partial name input
-   Displaying price evaluation for all available years of the selected
    model

All interactions occur through the terminal using `Scanner`.

------------------------------------------------------------------------

## 🏗 Architecture

    br.com.vehiclemarket
     ├── principal
     ├── service
     ├── model
     ├── util

### Main Components

-   **Principal** → Handles user interaction (CLI flow)
-   **Service Layer** → Responsible for API consumption
-   **Model Layer** → Represents Brands, Models, Years and Vehicle Data
-   **Jackson** → Used for JSON deserialization

------------------------------------------------------------------------

## 🔄 Application Flow

### 1️⃣ Vehicle Type Selection

The user selects:

-   `carros`
-   `motos`
-   `caminhoes`

Endpoint:

    https://parallelum.com.br/fipe/api/v1/{tipo}/marcas

------------------------------------------------------------------------

### 2️⃣ Brand Selection

The API returns:

``` json
[
  { "codigo": "21", "nome": "Fiat" }
]
```

Next endpoint:

    https://parallelum.com.br/fipe/api/v1/{tipo}/marcas/{codigoMarca}/modelos

------------------------------------------------------------------------

### 3️⃣ Model Filtering

Example filtering using Java Streams:

``` java
modelos.stream()
       .filter(m -> m.getNome().toUpperCase().contains("PALIO"))
       .toList();
```

------------------------------------------------------------------------

### 4️⃣ Year Retrieval

    https://parallelum.com.br/fipe/api/v1/{tipo}/marcas/{codigoMarca}/modelos/{codigoModelo}/anos

------------------------------------------------------------------------

### 5️⃣ Price Evaluation (All Years)

    https://parallelum.com.br/fipe/api/v1/{tipo}/marcas/{codigoMarca}/modelos/{codigoModelo}/anos/{codigoAno}

Example response:

``` json
{
  "Valor": "R$ 24.500,00",
  "Marca": "Fiat",
  "Modelo": "Palio Weekend Stile 1.6 mpi 16V 4p",
  "AnoModelo": 2003,
  "Combustivel": "Gasolina"
}
```

The application iterates over all years and prints a complete list of
evaluations.

------------------------------------------------------------------------

## 🔧 Technologies Used

-   Java 17+
-   Spring Boot
-   Jackson (JSON deserialization)
-   Java Streams API
-   REST API consumption
-   CLI interaction using `Scanner`

------------------------------------------------------------------------

## 📦 API Base URL

    https://parallelum.com.br/fipe/api/v1/

Supported endpoints:

-   `/carros`
-   `/motos`
-   `/caminhoes`

------------------------------------------------------------------------

## 🚀 How to Run

1.  Clone the repository
2.  Run the Spring Boot application
3.  Interact via terminal
4.  Follow the selection flow

------------------------------------------------------------------------

## 🎯 Key Concepts Applied

-   REST API consumption
-   JSON deserialization with Jackson
-   Java Streams filtering
-   Collection manipulation
-   Iteration and mapping
-   Layered architecture
-   CLI-based interaction
-   Clean code organization

------------------------------------------------------------------------

## 📖 Example Output

    Model: Palio Weekend Stile 1.6 mpi 16V 4p

    2001 - R$ 18.900,00
    2002 - R$ 21.300,00
    2003 - R$ 24.500,00
    2004 - R$ 26.100,00

