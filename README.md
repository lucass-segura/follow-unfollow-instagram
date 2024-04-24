# Instagram Unfollower Detector

Este script te permite detectar quién no te sigue de vuelta en Instagram. Simplemente sigue los pasos a continuación para utilizarlo.


## Instrucciones

1. **Ve a tu perfil de Instagram.**
   
3. **Abre la Consola del Navegador:**
   - Presiona `F12` o haz clic derecho en cualquier parte de la página y selecciona "Inspeccionar" o "Inspeccionar elemento", luego ve a la pestaña "Consola".
     
4. **Pega el Código en la Consola:**
   - Copia todo el código proporcionado a continuación y pégalo en la consola del navegador.
     ```
     function getCookie(b){let c=`; ${document.cookie}`,a=c.split(`; ${b}=`);if(2===a.length)return a.pop().split(";").shift()}function sleep(a){return new Promise(b=>{setTimeout(b,a)})}function afterUrlGenerator(a){return`https://www.instagram.com/graphql/query/?query_hash=3dec7e2c57367ef3da3d987d89f9dbc8&variables={"id":"${ds_user_id}","include_reel":"true","fetch_mutual":"false","first":"24","after":"${a}"}`}function unfollowUserUrlGenerator(a){return`https://www.instagram.com/web/friendships/${a}/unfollow/`}let followedPeople,csrftoken=getCookie("csrftoken"),ds_user_id=getCookie("ds_user_id"),initialURL=`https://www.instagram.com/graphql/query/?query_hash=3dec7e2c57367ef3da3d987d89f9dbc8&variables={"id":"${ds_user_id}","include_reel":"true","fetch_mutual":"false","first":"24"}`,doNext=!0,filteredList=[],getUnfollowCounter=0,scrollCicle=0;async function startScript(){for(var c,d,e,b,f,g=Math.floor;doNext;){let a;try{a=await fetch(initialURL).then(a=>a.json())}catch(h){continue}followedPeople||(followedPeople=a.data.user.edge_follow.count),doNext=a.data.user.edge_follow.page_info.has_next_page,initialURL=afterUrlGenerator(a.data.user.edge_follow.page_info.end_cursor),getUnfollowCounter+=a.data.user.edge_follow.edges.length,a.data.user.edge_follow.edges.forEach(a=>{a.node.follows_viewer||filteredList.push(a.node)}),console.clear(),console.log(`%c Progress ${getUnfollowCounter}/${followedPeople} (${parseInt(100*(getUnfollowCounter/followedPeople))}%)`,"background: #222; color: #bada55;font-size: 35px;"),console.log("%c Estos ratas no te siguen (cargando...)","background: #222; color: #FC4119;font-size: 25px;"),filteredList.forEach(a=>{console.log(a.username)}),await sleep(g(400*Math.random())+1e3),scrollCicle++,6<scrollCicle&&(scrollCicle=0,console.log("%c Esperando 10 segundos, tomate un tecito de manzanilla...","background: #222; color: ##FF0000;font-size: 35px;"),await sleep(1e4))}c=JSON.stringify(filteredList),d="usersNotFollowingBack.json",e="application/json",b=document.createElement("a"),f=new Blob([c],{type:e}),b.href=URL.createObjectURL(f),b.download=d,b.click(),console.log("%c Todo listo, ya termino","background: #222; color: #bada55;font-size: 40px;") } startScript();
       ```
     
5. **Presiona Enter para Ejecutar el Script:**
   - Una vez que hayas pegado el código, presiona `Enter` para iniciar el script.
     
6. **Espera a que el Script Termine:**
   - El script recorrerá tus seguidores y mostrará aquellos que no te siguen de vuelta. Ten paciencia mientras se ejecuta.


## Código Explicado

El código proporcionado es un script JavaScript que utiliza la API de Instagram para obtener una lista de tus seguidores y determinar quién no te sigue de vuelta. Aquí hay una breve explicación de algunas partes clave del código:

- **Función `getCookie(b)`:** Esta función se utiliza para obtener el valor de una cookie específica del navegador.
- **Función `sleep(a)`:** Esta función devuelve una promesa que se resuelve después de un tiempo determinado, lo que permite pausar la ejecución del script.
- **Funciones `afterUrlGenerator(a)` y `unfollowUserUrlGenerator(a)`:** Estas funciones generan las URL necesarias para obtener más seguidores y para dejar de seguir a un usuario, respectivamente.
- **Variables `csrftoken` y `ds_user_id`:** Estas variables almacenan el token CSRF y el ID de usuario necesarios para realizar las solicitudes a la API de Instagram.
- **Función `startScript()`:** Esta función inicia el script, realiza solicitudes a la API de Instagram, recorre los seguidores y muestra aquellos que no te siguen de vuelta en la consola del navegador.

Una vez que el script haya terminado de ejecutarse, se descargará un archivo JSON con la lista de usuarios que no te siguen de vuelta.
