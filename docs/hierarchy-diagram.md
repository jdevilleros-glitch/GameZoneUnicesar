---
config:
  layout: elk
---
classDiagram
direction TB
    class User {
    }

    class Client {
    }

    class Seller {
    }

    class Product {
    }

    class Videogame {
    }

    class Console {
    }

	<<abstract>> User
	<<abstract>> Product

    User <|-- Client
    User <|-- Seller
    Product <|-- Videogame
    Product <|-- Console
