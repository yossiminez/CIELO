# Listas de usuarios (DNI), contraseñas y roles
lst_users = ["12345678", "87654321", "45678912"]  # DNIs
lst_pass = ["admin123", "cliente123", "cliente456"]
lst_rol = [1, 2, 2]  # 1=Administrador, 2=Cliente

# Función de inicio de sesión
def login():
    swt_user = False
    swt_pass = False
    print("[__Login__]")
    dni = input("\tIngrese su DNI: ")
    while not swt_user:
        if dni in lst_users:
            swt_user = True
        else:
            print("***ALERTA! El DNI", dni, "NO EXISTE.")
            dni = input("\tIngrese otro DNI: ")

    idx = lst_users.index(dni)
    pasw = input("\tIngrese su clave: ")
    while not swt_pass:
        if pasw == lst_pass[idx]:
            swt_pass = True
        else:
            print("***ALERTA! Contraseña INCORRECTA.")
            pasw = input("\tIngrese su clave CORRECTA: ")

    return lst_rol[idx]

# Función para crear una nueva cuenta
def crear_sesion():
    print("[__Crear Cuenta__]")
    while True:
        nuevo_dni = input("\tIngrese su DNI (8 dígitos): ")
        if len(nuevo_dni) != 8 or not nuevo_dni.isdigit():
            print("***ALERTA! El DNI debe tener 8 dígitos numéricos.")
        elif nuevo_dni in lst_users:
            print("***ALERTA! El DNI ya está registrado. Intente con otro.")
        else:
            break
    nuevo_pass = input("\tIngrese una nueva contraseña: ")
    lst_users.append(nuevo_dni)
    lst_pass.append(nuevo_pass)
    lst_rol.append(2)  # Por defecto, los nuevos usuarios son clientes
    print("Cuenta creada con éxito. ¡Ahora puede iniciar sesión!")

# Menú del administrador
def m_adm():
    print("\n>>> BIENVENIDO ADMINISTRADOR")
    print("[1] Ver lista de clientes ingresados")
    print("[2] Registrar nuevo evento")
    print("[3] Modificar precios de entradas")
    print("[4] Gestionar menú de tragos")
    print("[5] Consultar ingresos totales")
    print("[0] Cerrar Sesión...")
    opc = input("Seleccione una opción: ")
    return opc

# Menú del cliente
def m_cli():
    print("\n>>> BIENVENIDO CLIENTE")
    print("[1] Ver eventos disponibles")
    print("[2] Comprar entradas")
    print("[3] Comprar tragos")
    print("[4] Ver carrito de compras")
    print("[5] Pagar")
    print("[0] Cerrar Sesión...")
    opc = input("Seleccione una opción: ")
    return opc

# Programa principal
def main():
    while True:
        print("\n[__Menú Principal__]")
        print("[1] Iniciar Sesión")
        print("[2] Crear Cuenta")
        print("[0] Salir")
        opc = input("Seleccione una opción: ")

        if opc == "1":  # Iniciar sesión
            rol = login()
            if rol == 1:  # Administrador
                while True:
                    opc_adm = m_adm()
                    if opc_adm == "0":
                        print("Cerrando sesión del administrador...\n")
                        break
                    else:
                        print(f"Ejecutando opción {opc_adm} del administrador...")
            else:  # Cliente
                while True:
                    opc_cli = m_cli()
                    if opc_cli == "0":
                        print("Cerrando sesión del cliente...\n")
                        break
                    else:
                        print(f"Ejecutando opción {opc_cli} del cliente...")
        elif opc == "2":  # Crear nueva cuenta
            crear_sesion()
        elif opc == "0":  # Salir
            print("Saliendo del programa. ¡Hasta luego!")
            break
        else:
            print("***ALERTA! Opción no válida. Intente nuevamente.")

# Ejecutar el programa
main()
