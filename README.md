# Proyecto Cordova | Camara
Plugin para la cámara del móvil. Asignatura PMDM.


1. Creé un proyecto Cordova en blanco usando la línea de comandos:
```
cordova create MyApp
```
2. Una vez hecho esto, me situé en el directorio del proyecto. Y agregué la plataforma en la que quiero que se cree mi aplicación. En mi caso:
```
cd MyApp
cordova platform add browser
cordova platform add android
```
3. Instalé el plugin de la cámara
```
cordova plugin add cordova-plugin-camera
```

4. Código del programa:
- **index.js**
  - Agregamos la cámara al evento `deviceready`
  - Añadimos el "Listener" del botón para hacer la foto
```
 onDeviceReady: function() {
       //this.receivedEvent('deviceready');
	     console.log(navigator.camera);

	     //Listener botón hacer foto
	     document.getElementById('btnFoto').addEventListener('click',() -> {
		      navigator.camera.getPicture(this.onSuccess,this.onFail, {
			    quality: 50,
			    destinationType: Camera.DestinationType.DATA_URL
		   });
 });
```
-
   - Cuando la foto es sacada con éxito
   - Recoge los id's del html, y la ruta de la imagen
```
 onSuccess:function(imageData){
    document.getElementById('imagen').innerHTML=`<img id='myImage' src="" alt="Aquí va la foto" width="200" height="200"></img>`
    var image=document.getElementById('myImage');
    image.src="data:image/jpeg;base64,"+imageData;
 },
```
  - Cuando hubo algún fallo en la foto
  - salta una alerta con su mensaje de error
```
 //Foto fallida
    onFail:function(message){
    alert('Failed because: '+message);
 },
```
- **index.html**
  - Añadí al html un botón, con el que se saca la foto
  - Y un "div", donde se coloca la foto sacada
```
  <button id="btnFoto" type="button" class="camera">CAMARA</button>
  <div id="imagen">
  </div>
```
