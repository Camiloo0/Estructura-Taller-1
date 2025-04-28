#Camilo Andres Alvarez log
import re
import json

# Función para extraer coincidencias usando expresiones regulares
def extractFromRegularExpression(regex, data): 
    if data: 
        return re.findall(regex, data)  # Retorna todas las coincidencias de la expresión regular
    return []  # Si no hay datos, retorna una lista vacía

# Abrir y leer el archivo de logs
with open(r"C:\Users\Servidorcamilo\Downloads\access.log", "r", encoding="utf-8") as file: 
    data = file.read()  # Leemos todo el contenido del archivo y lo guardamos en la variable 'data'

# Expresión regular para capturar el User-Agent (el último grupo entre comillas)
regex = r'\"([^\"]+)\"'  # Captura todo el texto dentro de las comillas dobles

# Extraer los User-Agents
resultados = extractFromRegularExpression(regex, data) or []  # Extraemos los User-Agents, si no hay resultados, usamos una lista vacía

# Si no se encuentran resultados, informar
if not resultados: 
    print("No se encontraron coincidencias. Verifica el formato del archivo o la expresión regular.") 
else: 
    # Diccionario para contar los navegadores
    navegadores_contados = {}

    # Clasificar los User-Agents por tipo de navegador
    for agente in resultados: 
        if "Chrome" in agente and "Edg" not in agente:  # Si es Chrome y no es Edge
            navegador = "Chrome"
        elif "Firefox" in agente:  # Si es Firefox
            navegador = "Firefox"
        elif "Safari" in agente and "Chrome" not in agente:  # Si es Safari (sin Chrome)
            navegador = "Safari"
        elif "Edge" in agente or "Edg" in agente:  # Si es Edge
            navegador = "Edge"
        elif "Googlebot" in agente:  # Si es Googlebot (bot de Google)
            navegador = "Googlebot"
        elif "Feedfetcher" in agente or "FeedBurner" in agente:  # Si es un bot de feed
            navegador = "Feedfetcher"
        else:  # Si no se clasifica en ninguna de las anteriores, se clasifica como 'Otros'
            navegador = "Otros"

        # Si el navegador no ha sido contado, inicializamos su contador
        if navegador not in navegadores_contados: 
            navegadores_contados[navegador] = 0 
        # Incrementamos el contador del navegador
        navegadores_contados[navegador] += 1 

    # Mostrar los resultados en formato JSON
    print(json.dumps(navegadores_contados, indent=4, ensure_ascii=False))
