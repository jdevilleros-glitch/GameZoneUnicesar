---
config:
  layout: elk
---
flowchart LR
 subgraph UI["User Interface Layer"]
    direction LR
        Main["Main"]
        Menu["Menu"]
        ClientUI["ClientUI"]
        ProductUI["ProductUI"]
        SellUI["SellUI"]
  end
 subgraph Services["Services Layer"]
    direction LR
        ClientService["ClientService"]
        ProductService["ProductService"]
        SellService["SellService"]
  end
 subgraph Persistence["Persistence Layer"]
    direction LR
        ClientRepository["ClientRepository"]
        ProductRepository["ProductRepository"]
        SellRepository["SellRepository"]
  end
 subgraph Model["Model Layer"]
    direction LR
        User["User (abstract)"]
        Client["Client"]
        Seller["Seller"]
        Product["Product (abstract)"]
        Videogame["Videogame"]
        Console["Console"]
        Sell["Sell"]
  end
    Main --> Menu
    Menu --> ClientUI & ProductUI & SellUI
    ClientUI --> ClientService
    ProductUI --> ProductService
    SellUI --> SellService
    ClientService --> ClientRepository
    ProductService --> ProductRepository
    SellService --> SellRepository & ProductService & ClientService
    ClientService -.-> Client
    ProductService -.-> Product
    SellService -.-> Sell & Client & Seller & Product
    ClientRepository -.-> Client
    ProductRepository -.-> Product
    SellRepository -.-> Sell

     Main:::ui
     Menu:::ui
     ClientUI:::ui
     ProductUI:::ui
     SellUI:::ui
     ClientService:::service
     ProductService:::service
     SellService:::service
     ClientRepository:::persistence
     ProductRepository:::persistence
     SellRepository:::persistence
     User:::model
     Client:::model
     Seller:::model
     Product:::model
     Videogame:::model
     Console:::model
     Sell:::model
    classDef ui fill:#eef2ff,stroke:#818cf8,color:#1e1b4b
    classDef service fill:#f0fdfa,stroke:#2dd4bf,color:#042f2e
    classDef persistence fill:#fff7ed,stroke:#fb923c,color:#431407
    classDef model fill:#f5f3ff,stroke:#a78bfa,color:#2e1065
