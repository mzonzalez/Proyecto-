# programacion-2.0
# -------------------------------------------------------------------------
# HERRAMIENTAS
# -------------------------------------------------------------------------

#Separadores para separar cada parte del programa 
def separador():
    print("*"*40) #Imprime astericos para separar multiplicados por 40

def separador_lineas():
    print("-"*40) #Imprime lineas para separar multiplicados por 40

def clear():
    print("\033[H\033[J", end="") #Expresion para limpiar la consola

# -------------------------------------------------------------------------
# SECCON DEL CLIENTE
# -------------------------------------------------------------------------

cliente = {}

def agregar_cliente():
    try: #Try contiene las sentencias que se ejecutaran del programa
        global cliente #Variable global para usarla en todo l programa
        global orden_de_venta
        nombre = input("Ingresar Nombre: ")
        cliente['Nombre'] = nombre
        vat = input("Ingresar Identificación: ")
        cliente['Identificacion'] = vat
        orden_de_venta['Cliente'] = nombre #En orden de venta, cliente ira el nombre del cliente
    except: #Pasara a ejecutarse el except cuando el try falle, 
        pass

def mostrar_cliente():
    clear() #Limpia la consola
    separador() #Llama a funcion separador para hacer una separacion de secciones
    for key, value in cliente.items():#Recorre la variable cliente para mostrar los cientes
        print(f'{key: <15}{value}') #Hace un print de maximo 15 lineas y lo imprime de forma tabulada
    separador()
    input("Presione Enter para continuar...")

# -------------------------------------------------------------------------
# PRODUCTOS
# -------------------------------------------------------------------------

productos = [ #Lista de diccionarios de productos, estos estaran almacenados en el programa
    {
        'ID': 1,
        'Nombre': 'Mueble 1',
        'Impuesto': 13.0,
        'Precio': 100.0
    },
    {
        'ID': 2,
        'Nombre': 'Mueble 2',
        'Impuesto': 13.0,
        'Precio': 200.0
    },
    {
        'ID': 3,
        'Nombre': 'Mueble 3',
        'Impuesto': 13.0,
        'Precio': 300.0
    }
]

def mostrar_productos():
    clear()
    for producto in productos:
        separador()
        for key, value in producto.items():
            print(f'{key: <15}{value}')
        separador()

    input("Presione Enter para continuar...")

# -------------------------------------------------------------------------
# ORDENES DE VENTA
# -------------------------------------------------------------------------

orden_de_venta = {
    'ID': 1,
    'Cliente': False,
    'Lineas': [],
    'Total': 0.0
}

def agregar_producto():
    try:
        global orden_de_venta
        global productos
        product_id = input("Indicar el ID del producto para agregarlo: ") 
        producto = next(item for item in productos if item["ID"] == int(product_id))
        orden_de_venta.get('Lineas').append(producto)
    except:
        pass

def calcular_totales():
    global orden_de_venta
    total = 0.0
    for linea in orden_de_venta['Lineas']:
        precio = linea.get('Precio')
        impuesto = linea.get('Impuesto')
        monto_impuesto = precio * impuesto / 100
        total += precio + monto_impuesto
    orden_de_venta['Total'] = total

def mostrar_order_de_venta():
    clear()
    separador()
    global orden_de_venta
    calcular_totales()
    for key, value in orden_de_venta.items():
        if key == 'Lineas':
            separador_lineas()
            for linea in value:
                for key_linea, value_linea in linea.items():
                    print(f'{key_linea: <15}{value_linea}')
                separador_lineas()
        else:
            print(f'{key: <15}{value}')
    separador()
    input("Presione Enter para continuar...")

# -------------------------------------------------------------------------
# CONTROLADOR
# -------------------------------------------------------------------------

def menu():
    print("1) - Agregar Cliente")
    print("2) - Mostrar Información de Cliente")
    print("3) - Listar Productos")
    print("4) - Agregar Producto en Orden de Venta")
    print("5) - Mostrar Orden de Venta")
    print("99) - Salir")

def manejar_menu():
    menu = input("Por favor ingrese una opción:\n")
    return int(menu)

def main_loop():
    mantener = 0
    while mantener != 99:
        separador()
        menu()
        separador()
        mantener = manejar_menu()
        if mantener == 1:
            agregar_cliente()
        if mantener == 2:
            mostrar_cliente()
        if mantener == 3:
            mostrar_productos()
        if mantener == 4:
            agregar_producto()
        if mantener == 5:
            mostrar_order_de_venta()
        clear()

main_loop() #Inicio de programa
