
## Configuración inicial
Obtener una clave de API de OpenWeatherMap.

1.  Regístrarse en el sitio web de OpenWeatherMap en [https://openweathermap.org](https://openweathermap.org/) si aún no se tiene una cuenta.
2.  Inicia sesión y navega a la sección "API Keys" (Claves de API) en tu perfil.
3.  Generar una nueva clave de API y copiarla, ya que se necesitara más adelante en el código.

## Estructura del código

A continuación se muestra el código JavaScript necesario para realizar la solicitud a la API de OpenWeatherMap y mostrar los datos del clima en tu aplicación. 

## Explicación del código

El código consta de dos funciones principales: `fetchDatosClima(ciudad)` y `mostrarDatosClima(data)`.

1.  `fetchDatosClima(ciudad)`: Esta función se encarga de hacer una solicitud a la API de OpenWeatherMap para obtener los datos del clima de la ciudad especificada. Recibe el nombre de la ciudad como parámetro. Utiliza la función `fetch()` para enviar una solicitud GET a la URL de la API, incluyendo la ciudad y tu clave de API. Luego, convierte la respuesta en formato JSON utilizando el método `json()`. Finalmente, llama a la función `mostrarDatosClima(data)` pasando los datos obtenidos como argumento.

    function fetchDatosClima(ciudad){
        fetch(`${urlBase}?q=${ciudad}&appid=${api_key}`)
        .then(data => data.json())
        .then(data => mostrarDatosClima(data))
    }
    
2.  `mostrarDatosClima(data)`: Esta función se encarga de mostrar los datos del clima en la página. Recibe los datos del clima en formato JSON como parámetro. Primero, obtiene las diferentes propiedades relevantes de los datos, como el nombre de la ciudad, el nombre del país, la temperatura, la humedad, la descripción y el icono del clima. Luego, crea elementos HTML apropiados, como encabezados y párrafos, y les asigna el contenido correspondiente utilizando la propiedad `textContent`. También crea un elemento de imagen para mostrar el icono del clima. Finalmente, agrega todos los elementos creados al elemento `<div>` con el ID "datosClima" en tu página.

    function mostrarDatosClima(data){
        const divDatosClima = document.getElementById('datosClima')
        divDatosClima.innerHTML=''
    
        const ciudadNombre = data.name
        const paisNombre = data.sys.country
        const temperatura = data.main.temp
        const humedad = data.main.humidity
        const descripcion = data.weather[0].description
        const icono = data.weather[0].icon
    
        const ciudadTitulo = document.createElement('h2')
        ciudadTitulo.textContent = `${ciudadNombre}, ${paisNombre}`
    
        const temperaturaInfo = document.createElement('p')
        temperaturaInfo.textContent = `La temperatura es: ${Math.floor(temperatura-difKelvin)}ºC`
        
        const humedadInfo = document.createElement('p')
        humedadInfo.textContent = `La humedad es: ${humedad}%`
    
        const iconoInfo = document.createElement('img')
        iconoInfo.src= `https://openweathermap.org/img/wn/${icono}@2x.png`
    
        const descripcionInfo = document.createElement('p')
        descripcionInfo.textContent = `La descripción meteorológica es: ${descripcion}`
    
        divDatosClima.appendChild(ciudadTitulo)
        divDatosClima.appendChild(temperaturaInfo)
        divDatosClima.appendChild(humedadInfo)
        divDatosClima.appendChild(iconoInfo)
        divDatosClima.appendChild(descripcionInfo)
    }
    

## Uso de la aplicación

1.  Inserta un campo de entrada de texto en tu página con el ID "ciudadEntrada" para que los usuarios puedan ingresar el nombre de la ciudad.
2.  Agrega un botón con el ID "botonBusqueda" para permitir a los usuarios buscar el clima de la ciudad ingresada.
3.  Cuando un usuario haga clic en el botón de búsqueda, se llamará a la función `fetchDatosClima(ciudad)` con el valor ingresado en el campo de entrada de texto.
4.  La función `fetchDatosClima(ciudad)` realizará una solicitud a la API de OpenWeatherMap y obtendrá los datos del clima correspondientes a la ciudad ingresada.
5.  Una vez que se obtengan los datos del clima, la función `mostrarDatosClima(data)` mostrará los detalles relevantes del clima en la página.