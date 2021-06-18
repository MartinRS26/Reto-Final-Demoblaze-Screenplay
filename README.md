# Reto-Final-Demoblaze-Screenplay
Este reto se basa en la automatización sobre la página https://www.demoblaze.com/index.html de los procesos
Login, Seleccion de producto, verificación del producto, y verificación de la compra basandonos en los datos del 
usuario, fue realizado usando Gradle, Java, Serenity BDD y Cucumber, bajo Screenplay.

## Composición Código Fuente

| Capa| Definición |
| ------------- | ------------- |
| Tasks | Contiene las tareas que se ejecutarán en la automatización  |
| Interactions  | Contiene las interacciones que se ejecutarán en la automatización  |
| User Interfaces | Contiene los mapeos de los elementos de las diferentes interfaces |
| Models | Contiene los modelos que se usarán para la construcción de la automatización |
| Exceptions | Contiene las excepciones que se pueden presentar en la prueba |
| Questions | Contiene las preguntas que se verificarán en la prueba |
| Runners | Contiene el ejecutor de la prueba automatizada |
| Steps Definitions | Contiene los pasos de ejecución de la prueba |
| Features | Contiene los escenarios en lenguaje Gherkin |

## Tasks

### IrHaciaLoginDeUsuario
Dirige al usuario hacia la interfaz de Login.
```java
		
public class IrHaciaLoginDeUsuario implements Task {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(SeleccionarOpcionLogin.opcionLogin());
    }

    public static IrHaciaLoginDeUsuario DemoBlaze() {
        return instrumented(IrHaciaLoginDeUsuario.class);
    }
} 
```

### DiligenciarCredencialesUsuario
Permite diligenciar al usuario sus datos de acceso.
```java
public class DiligenciarCredencialesUsuario implements Task {


    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(IngresoCredencialesUsuario.CredencialesUsuario());
    }

    public static DiligenciarCredencialesUsuario DemoBlaze() {
        return instrumented(DiligenciarCredencialesUsuario.class);
    }
}

```

### IrAPerfilDeUsuario
Dirige al usuario hacia su cuenta
```java
public class IrAPerfilDeUsuario implements Task {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(ClickBotonLogin.botonLogin());
    }

    public static IrAPerfilDeUsuario Demoblaze() {
        return instrumented(IrAPerfilDeUsuario.class);
    }
}
```
### SeleccionarProducto
Permite elegir un producto o articulo al usuario

```java
   public class SeleccionarProducto implements Task {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(ElegirSamsungGalaxyS6.SeleccionarSamsungGalaxyS6());

    }

    public static SeleccionarProducto DemoBlaze() {
        return instrumented(SeleccionarProducto.class);
    }
}
```
### AgregarAlCarrito
Permite al usuario añadir el producto que seleccionó al carrito de la tienda

```java
public class AgregarAlCarrito implements Task {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(ClickBotonAgregarAlCarrito.agregarAlCarrito());
    }

    public static AgregarAlCarrito DemoBlaze() {
        return instrumented(AgregarAlCarrito.class);
    }
}
```
### IrAlCarrito
Dirige al usuario hacia el carrito en su cuenta

```java
   public class IrAlCarrito implements Task {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(AbrirCarrito.carrito());
    }

    public static IrAlCarrito DemoBlaze() {
        return instrumented(IrAlCarrito.class);
    }
}
```
### RealizarPedido
Permite realizar el pedido luego de la verificacion del articulo y dirige al usuario hacia el formulario de 
datos del pedido
```java
public class RealizarPedido implements Task {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(ClickBotonPlaceOrder.realizaPedido());
    }

    public static RealizarPedido DemoBlaze() {
        return instrumented(RealizarPedido.class);
    }
}
```
### DiligenciarDatosPedido

Permite al usuario diligenciar los datos del pedido

```java
public class DiligenciarDatosPedido implements Task {

    private Data data;

    public DiligenciarDatosPedido(Data data) {
        this.data = data;
    }

    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(IngresoDatosPedido.datosPedido(data));
    }

    public static DiligenciarDatosPedido DemoBlaze(Data data) {
        return instrumented(DiligenciarDatosPedido.class, data);
    }
}
```
### GenerarOrdenDePago
Dirige al usuario hacia la interfaz de la orden de pago generada

```java
public class GenerarOrdenDePago implements Task {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(ClickBotonPurchase.comprar());
    }

    public static GenerarOrdenDePago DemoBlaze() {
        return instrumented(GenerarOrdenDePago.class);
    }
}
```

## Interactions

### SeleccionarOpcionLogin
Realiza un click sobre la opcion Login

```java
public class SeleccionarOpcionLogin implements Interaction {

    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Click.on(LOGIN_USER));
    }

    public static SeleccionarOpcionLogin opcionLogin() {
        return instrumented(SeleccionarOpcionLogin.class);
    }
}
```
### IngresoCredencialesUsuario
Realiza escritura de nombre de usuario y password 
```java
public class IngresoCredencialesUsuario implements Interaction {

    String nombreUsuario = "martin121314";
    String password = "12345678901234";

    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Enter.theValue(nombreUsuario).into(NOMBRE_USUARIO),
                Enter.theValue(password).into(PASSWORD_USUARIO));
    }

    public static IngresoCredencialesUsuario CredencialesUsuario() {
        return instrumented(IngresoCredencialesUsuario.class);
    }
}
```
### ClickBotonLogin
Realiza click en el boton Login de la interfaz de Login del usuario
```java
public class ClickBotonLogin implements Interaction {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Click.on(BOTON_LOGIN));
    }

    public static ClickBotonLogin botonLogin() {
        return instrumented(ClickBotonLogin.class);
    }
}
```
### ElegirSamsungGalaxyS6
Realiza click sobre el nombre del Samsung Galaxy S6 y dirige hacia su información
```java
public class ElegirSamsungGalaxyS6 implements Interaction {

    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Click.on(SAMSUNG_GALAXY_S6));
    }

    public static ElegirSamsungGalaxyS6 SeleccionarSamsungGalaxyS6() {
        return instrumented(ElegirSamsungGalaxyS6.class);
    }
}
```

### ClickBotonAgregarAlCarrito
Realiza click sobre el boton "Add to Cart" 
```java
public class ClickBotonAgregarAlCarrito implements Interaction {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Click.on(AGREGAR_AL_CARRITO));

    }

    public static ClickBotonAgregarAlCarrito agregarAlCarrito() {
        return instrumented(ClickBotonAgregarAlCarrito.class);
    }
}
```
### AbrirCarrito
Realiza Click sobre la opción Cart de la barra de navegación de la página
```java
public class AbrirCarrito implements Interaction {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Click.on(OPCION_CARRITO));

    }

    public static AbrirCarrito carrito() {
        return instrumented(AbrirCarrito.class);
    }
}
```
### ClickBotonPlaceOrder
Realiza click sobre el boton place order en la interfaz del carrito
```java
public class ClickBotonPlaceOrder implements Interaction {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Click.on(REALIZAR_PEDIDO));
    }

    public static ClickBotonPlaceOrder realizaPedido() {
        return instrumented(ClickBotonPlaceOrder.class);
    }
}
```
### IngresoDatosPedido
Escribe los datos del usuario que realiza el pedido que irán en la orden de pago
```java
public class IngresoDatosPedido implements Interaction {

    private Data data;


    public IngresoDatosPedido(Data data) {
        this.data = data;
    }

    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Enter.theValue(data.getName()).into(NOMBRE_PEDIDO),
                Enter.theValue(data.getCountry()).into(PAIS_PEDIDO),
                Enter.theValue(data.getCity()).into(CIUDAD_PEDIDO),
                Enter.theValue(data.getCardNumber()).into(TARJETA_CREDITO_PEDIDO),
                Enter.theValue(data.getMonth()).into(MES_PEDIDO),
                Enter.theValue(data.getYear()).into(YEAR_PEDIDO)
        );
    }

    public static IngresoDatosPedido datosPedido(Data data) {
        return instrumented(IngresoDatosPedido.class, data);
    }
}
```
### ClickBotonPurchase
Realiza click sobre el botón "Purchase" efectuando la compra
```java
public class ClickBotonPurchase implements Interaction {
    @Override
    public <T extends Actor> void performAs(T actor) {
        actor.attemptsTo(Click.on(COMPRAR));
    }

    public static ClickBotonPurchase comprar() {
        return instrumented(ClickBotonPurchase.class);
    }
}
```

## User Interfaces

### DemoBlazeHomePage
Esta clase contiene los mapeos de la página principal de DemoBlaze

```java
@DefaultUrl("https://www.demoblaze.com/index.html")
public class DemoBlazeHomePage extends PageObject {
    public static final Target LOGIN_USER = Target.the("Opcion login de usuario").located(By.id("login2"));
}
```

### CredencialesUsuarioPage
Esta clase contiene los mapeos de la interfaz de Login de usuario

```java
public class CredencialesUsuarioPage {
    public static final Target NOMBRE_USUARIO = Target.the("Espacio para nombre de usuario").located(By.id("loginusername"));
    public static final Target PASSWORD_USUARIO = Target.the("Espacio para password de usuario").located(By.id("loginpassword"));
    public static final Target BOTON_LOGIN = Target.the("Boton para realizar login").located(By.xpath("//*/div[@id=\"logInModal\"]/div/div/div[3]/button[2]"));
}
```
### ProductosPage
Esta clase contiene los mapeos de la interfaz de productos disponibles

```java
public class ProductosPage {
    public static final Target SAMSUNG_GALAXY_S6 = Target.the("Seleccionar Samsung Galaxy S6").located(By.xpath("//*[@id=\"tbodyid\"]/div[1]/div/div/h4/a"));
}
```
### SamsungGalaxyS6Page
Esta clase contiene los mapeos de la interfaz de información del producto
```java
public class SamsungGalaxyS6Page {
    public static final Target AGREGAR_AL_CARRITO = Target.the("Boton agregar al carrito").located(By.xpath("//*/a[@class=\"btn btn-success btn-lg\"]"));
    public static final Target OPCION_CARRITO = Target.the("Seleccionar opcion carrito").located(By.id("cartur"));
}
```
### CarritoPage
Esta clase contiene los mapeos de la interfaz del carrito para el usuario
```java
public class CarritoPage {
    public static final Target NOMBRE_PRODUCTO = Target.the("Nombre Producto del carrito").located(By.xpath("//*/tbody/tr[1]/td[2]"));
    public static final Target REALIZAR_PEDIDO = Target.the("Seleccionar Boton Place Order").located(By.xpath("//div[@class=\"col-lg-1\"]/button"));
}
```
### RealizarPedidoPage
Esta clase contiene los mapeos de la interfaz del formulario de los datos del usuario que realiza el pedido
```java
public class RealizarPedidoPage {
    public static final Target NOMBRE_PEDIDO = Target.the("Espacio para nombre en el pedido").located(By.xpath("//div[@class=\"form-group\"]/input[@id=\"name\"]"));
    public static final Target PAIS_PEDIDO = Target.the("Espacio para pais en el pedido").located(By.xpath("//div[@class=\"form-group\"]/input[@id=\"country\"]"));
    public static final Target CIUDAD_PEDIDO = Target.the("Espacio para ciudad en el pedido").located(By.xpath("//div[@class=\"form-group\"]/input[@id=\"city\"]"));
    public static final Target TARJETA_CREDITO_PEDIDO = Target.the("Espacio para tarjeta de credito en el pedido").located(By.xpath("//div[@class=\"form-group\"]/input[@id=\"card\"]"));
    public static final Target MES_PEDIDO = Target.the("Espacio para mes en el pedido").located(By.xpath("//div[@class=\"form-group\"]/input[@id=\"month\"]"));
    public static final Target YEAR_PEDIDO = Target.the("Espacio para year en el pedido").located(By.xpath("//div[@class=\"form-group\"]/input[@id=\"year\"]"));
    public static final Target COMPRAR = Target.the("Seleccion Boton purchase").located(By.xpath("//div[@id=\"orderModal\"]/div/div/div[3]/button[2]"));


}
```
### OrdenDePagoPage
Esta clase contiene los mapeos de la interfaz de la orden de pago generada
```java
public class OrdenDePagoPage {
    public static final Target NUMERO_TARJETA_ORDEN = Target.the("Numero de tarjeta de la orden de pago").located(By.xpath("/html/body/div[10]/p"));
    public static final Target NOMBRE_ORDEN = Target.the("Nombre de la orden de pago").located(By.xpath("/html/body/div[10]/p"));
}
```
