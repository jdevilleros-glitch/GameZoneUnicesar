Personas
    (nombre, id, telefono)
- Clientes
    (correo, historial)
- Vendedores
    (codemp, turno)

Productos
    (id, titulo, precio, stock, descripcion)
- Videojuego
    (plataforma, genero, edadrating)
- Consolas
    (marca, modelo, generacion)

Ventas (al menos un productosVenta, debe descontar del inventario cada producto vendido y si es insuficiente tampoco deja hacer la compra, el total es la suma de todos los productos duh)
    (fecha, cliente, vendedor, productosVenta)

Consultar:
    - Inventario
    - Listado de clientes
    - Listado de vendedores
    - Historial de ventas (total, de un cliente y de un vendedor)

Debe guardar todas las acciones hechas en archivos cada vez que se ejecute una accion

debe estar en modelo vista - servicio - dao - model

1) According to the context of the project, every user must have an id, a name and a phone number. Then its said that a client needs an email, and a purchase history.
Since User contains the common attributes between client and seller, this attributes are inherited and the specific attributes are added for each one.

2) It should exist but only if its abstract, because we need specific roles in this project to make it more easy to mantain and to understand.

3) Every product has its own id, title or name, price, stock number in inventory and a description of itself.
Videogames need to have a platform where its played or developed, a genre and a age rating.
Consoles must have its brand´s name, a model name or tag and the number of the generation that they are.

4) It should be declared as an abstract method that gets overrided in every subclass because every desciption can be made different. Here we use abstraction, inheritance and polymorphism.

5) Client -> Sell, Seller -> Sell, Sell -> Product have both Asociation relations since they need to know each other but dont depend on the other one to exist.
 Client -> User, Seller -> User and Product -> (Each product type) all have inherited relations because they ARE what their parent class is but specialized.

6) Sell itself should do its own sell total since it is one of the characteristics that is contained on the sell.

7) It has to make sure that the number of products that are sold isn´t 0, the validation must be made before the sell is registered

8) User -> UI -> SellService -> Sell -> Product -> (Stock Updated) -> (Update File)
The classes involved are mainly: Sell, Product, SellService, ProductService and ProductDAO (or the file that saves the Products)

9) The main criteria is knowing what is the responsability of the class.

If it represets some object of the project or bussiness, it is a model. Models like User, Client, Seller, Product, Videogame, Console, Sell.
                            |
                            v
If it interacts directly with the user, it is part of the user interface. User interface will have files like Menu, Main, ClientUI, ProductIU and SellUI.
                            |
                            v
If it manages the operations and the bussiness rules, it is part of the services. Service will have classes like ClientService, ProductService and SellService.
                            |
                            v
If it saves or loads data, it part of the persistency. Persistecy files could be like ClientRepository, ProductRepository and SellRepository.

10) Because we would be mixing responsabilities, this would make the code more difficult to mantain, to read and to make tests.

11) The general idea is that all of the three layers depends on Model, then the Service layer depends on the UI layer and finally the Persistecy layer depends on the Service layer.
This makes the project more organized and understandable, while still following a logical sense.
