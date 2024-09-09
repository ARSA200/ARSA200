import time
import requests

def create_account():
    # Aquí puedes personalizar los datos de la cuenta
    username = f"user_{int(time.time())}"
    password = "password123"
    email = f"{username}@gmail.com"

    # Crear la cuenta
    url = "https://www.instagram.com/sign_up/"
    headers = {
        "User-Agent": "Instagram 137.0.0.39.257 (iPhone11,4; iOS 13_5_1; en_US; en-US; i386)",
        "Referer": "https://www.instagram.com/"
    }
    data = {
        "phone_number": "",
        "email": email,
        "password": password,
        "username": username
    }
    response = requests.post(url, headers=headers, data=data)

    # Chequear si la cuenta se creó correctamente
    if "already exists" in response.text:
        print(f"Cuenta {username} ya existe")
    else:
        print(f"Cuenta {username} creada con éxito")
        # Aquí puedes seguir una cuenta en específico
        seguir_cuenta(username, "example_username")

def seguir_cuenta(username, seguir_username):
    url = f"https://www.instagram.com/web/friendships/{seguir_username}/follow/"
    headers = {
        "User-Agent": "Instagram 137.0.0.39.257 (iPhone11,4; iOS 13_5_1; en_US; en-US; i386)",
        "X-CSRFToken": response.cookies["csrftoken"],
        "Referer": f"https://www.instagram.com/{seguir_username}/"
    }
    response = requests.post(url, headers=headers, cookies=response.cookies)

    if "followed" in response.text:
        print(f"{username} siguiendo a {seguir_username}")
    else:
        print(f"{username} ya sigue a {seguir_username}")

# Crear 100 cuentas por segundo
for _ in range(100):
    create_account()
    time.sleep(1)
