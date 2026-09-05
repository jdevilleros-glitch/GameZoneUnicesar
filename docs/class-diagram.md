---
config:
  layout: elk
---
classDiagram
direction TB

namespace Model {
    class User {
        <<abstract>>
        #String id
        #String name
        #String cellphone
        +getId() String
        +getName() String
        +getCellphone() String
    }

    class Client {
        -String email
        -List~Sell~ purchaseHistory
        +getEmail() String
        +getPurchaseHistory() List~Sell~
        +addPurchase(sell: Sell) void
    }

    class Seller {
        -String employeeCode
        -String shift
        +getEmployeeCode() String
        +getShift() String
    }

    class Product {
        <<abstract>>
        #String id
        #String title
        #decimal price
        #int stock
        #String description
        +getId() String
        +getPrice() decimal
        +getStock() int
        +hasStock(quantity: int) boolean
        +decreaseStock(quantity: int) void
        #formatDescription() String*
    }

    class Videogame {
        -String platform
        -String genre
        -String ageRating
        #formatDescription() String
    }

    class Console {
        -String brand
        -String model
        -int generation
        #formatDescription() String
    }

    class Sell {
        -String id
        -Date date
        -decimal total
        -List~Product~ productsSold
        +addProduct(product: Product) void
        +validateProducts() boolean
        +calculateTotal() decimal
        +getTotal() decimal
        +register() void
    }
}

namespace UserInterface {
    class Main {
        +main(args: String[]) void$
    }

    class Menu {
        -ClientUI clientUI
        -ProductUI productUI
        -SellUI sellUI
        +show() void
        +selectOption() void
    }

    class ClientUI {
        -ClientService clientService
        +createClient() void
        +showClientList() void
    }

    class ProductUI {
        -ProductService productService
        +createProduct() void
        +showInventory() void
    }

    class SellUI {
        -SellService sellService
        +registerSell() void
        +showSellHistory() void
    }
}

namespace Services {
    class ClientService {
        -ClientRepository clientRepository
        +createClient(client: Client) void
        +getAllClients() List~Client~
        +getClientHistory(clientId: String) List~Sell~
    }

    class ProductService {
        -ProductRepository productRepository
        +createProduct(product: Product) void
        +getInventory() List~Product~
        +updateStock(product: Product, quantity: int) void
    }

    class SellService {
        -SellRepository sellRepository
        -ProductService productService
        -ClientService clientService
        +registerSell(sell: Sell) boolean
        +getSellHistory() List~Sell~
        +getSellsByClient(clientId: String) List~Sell~
        +getSellsBySeller(employeeCode: String) List~Sell~
    }
}

namespace Persistence {
    class ClientRepository {
        -String filePath
        +save(client: Client) void
        +findAll() List~Client~
        +findById(id: String) Client
    }

    class ProductRepository {
        -String filePath
        +save(product: Product) void
        +findAll() List~Product~
        +findById(id: String) Product
    }

    class SellRepository {
        -String filePath
        +save(sell: Sell) void
        +findAll() List~Sell~
        +findByClient(clientId: String) List~Sell~
        +findBySeller(employeeCode: String) List~Sell~
    }
}

User <|-- Client
User <|-- Seller
Product <|-- Videogame
Product <|-- Console

Client "1" --> "0..*" Sell : purchases
Seller "1" --> "0..*" Sell : registers
Sell "0..*" --> "1..*" Product : productsSold
Client "1" o-- "0..*" Sell : purchaseHistory

Main "1" *-- "1" Menu : starts
Menu "1" o-- "1" ClientUI : accesses
Menu "1" o-- "1" ProductUI : accesses
Menu "1" o-- "1" SellUI : accesses

ClientUI ..> ClientService : uses
ProductUI ..> ProductService : uses
SellUI ..> SellService : uses

ClientService ..> ClientRepository : persists
ProductService ..> ProductRepository : persists
SellService ..> SellRepository : persists
SellService ..> ProductService : updates stock
SellService ..> ClientService : updates history

ClientRepository ..> Client : stores
ProductRepository ..> Product : stores
SellRepository ..> Sell : stores
