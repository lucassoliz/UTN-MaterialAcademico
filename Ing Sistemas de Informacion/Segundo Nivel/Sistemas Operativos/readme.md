# Sistemas Operativos -- Plug & Pray  
### Enunciado + TP + Pruebas
- [Plug & Pray Ultima version.pdf](https://github.com/user-attachments/files/30522500/Plug.Pray.Ultima.version.pdf)  (publicado dos semana despues de la primera clase)
- TP APROBADO: [tp-2026-1c-418-im-a-teapot-abace6173f924ee2c7ec192b14cbfe05e7665ab9.zip](https://github.com/user-attachments/files/30525293/tp-2026-1c-418-im-a-teapot-abace6173f924ee2c7ec192b14cbfe05e7665ab9.zip) 
- [1c2026 - Plug & Pray - Pruebas (.pdf](https://github.com/user-attachments/files/30525382/1c2026.-.Plug.Pray.-.Pruebas.pdf) (publicado una semana antes de la primera fecha de entrega)


<img width="2197" height="1240" alt="image" src="https://github.com/user-attachments/assets/28499e8c-4107-4473-a20e-88ee5342a2fb" />

# Desarrollo TP subido por ETAPAS  
Tener en cuenta que el TP fue escalando y claramente no voy a subir todas las etapas, solo las mas relevantes, ademas esta enfocado 
desde mi punto de vista como Kernel Scheduler (KS)

## Desarrollo Checkpoint 1  
#### Conexiones con KM y iniciar como servidor
- [tp-2026-1c-418-im-a-teapot-99eacacc602a58af7aab7b7542eaa04ffee12f19.zip](https://github.com/user-attachments/files/30522756/tp-2026-1c-418-im-a-teapot-99eacacc602a58af7aab7b7542eaa04ffee12f19.zip)


**ETAPA DE PLANEACIÓN(*Caja negra*)** : Se planeo el desarrollo de la comunicación entre los diferentes modulos detectando quienes son 
**SERVIDORES** y Quienes son **CLIENTES**, para que dos modulos se reconozcan, cada uno tendra un codigo de operación que lo identifica 
<img width="500" height="500" alt="577896401-83c59d97-939e-48e8-8e6f-6d500be50b34" src="https://github.com/user-attachments/assets/de2e2cf5-a2c5-4b08-8081-61b4c5fc5823" />

Es decir, que cuando un cliente se conecta, lo primero que hace es un **handshake**, basicamente se presenta enviando su código  
Ponele por ejemplo: El KS se conecta a KM, y le mando el codigo HANDSHAKE_KS, KM lo recibe, tendra que verificar que sea un modulo  
que entiende y le responde con un HANDSHAKE_OK para confirmar que la comunicación quedo establecida 
<img width="350" height="350" alt="lucas siles Ejemplo HANDSHAKE comunicacion" src="https://github.com/user-attachments/assets/a9cbba15-c659-4415-89a6-9194cf674262" />


Recien despues de ese OK confirmando, empiezan a intercambiar mensajes entre si

<img width="1282" height="737" alt="Lucas Siles Comunicacion entre modulos y protocolo" src="https://github.com/user-attachments/assets/ff9ca194-ac4c-485d-8ec0-78a6a2c94b1e" />

**ETAPA DE DESARROLLO (*Caja blanca*)**:  La circunferencia verde y amarilla indica que estoy repitiendo codigo y en la simagenes de abajo digo donde
<img width="1936" height="905" alt="577896077-0b154dcf-8f8c-4859-b4f1-1399353137ee" src="https://github.com/user-attachments/assets/1da06304-d965-433e-82d2-5a7989210e63" />
<img width="1079" height="591" alt="lucas siles inicializar_kernel_memory" src="https://github.com/user-attachments/assets/a0a7dc35-fb57-4bf8-ba82-3218012986fd" />

Se recomienda leer la pagina de la catedra (https://docs.utnso.com.ar/guias/linux/sockets), y  realizar el TP0 (https://github.com/lucassoliz/tp0), de ahi podes 
reutilizar codigo

 <img width="1434" height="575" alt="Lucas siles Reutilización codigo TP0" src="https://github.com/user-attachments/assets/feb5b5f8-d133-484c-8e20-a9df3a278aa3" />  
 
### Sobre las commons de la catedra    

yyy mira, es una biblioteca que te provee la catedra donde te puede brindar estructuras de datos como listas, diccionarios, colas, etc...  
Por ejemplo en mi caso como KS, use la t_list para todas las colas de estados, o el diccionario (t_dictionary) que use para saber por ejemplo  
que proceso ejecuta en cada CPU ponele, o tambien te brinda utilidades como el logger (t_list) para los logs obligatorios, el manejo de  
archivos de configuracion (t_config), funciones para strings (como string_itoa, que ojo hace internamente malloc y si no la liberas con free,  
tendras memory leak, lo digo por experiencia jaja)  
Pero eso, ayudan bastante porque te evita tenerlo que programar desde cero ponele una lista enlazada o un parser de configuracion  
usas una implementacion ya testeada y la concentras en el TP

No tiene sentido no usar las commons de la catedra y programes la logica vos, ahi te das cuenta facilmente quienes estan usando IA 

<img width="925" height="752" alt="image" src="https://github.com/user-attachments/assets/bdd43d3d-e3d3-4425-b573-a3f245427d89" />

### Sobre la organizacion del trabajo  

<img width="1165" height="742" alt="image" src="https://github.com/user-attachments/assets/d11eec35-62e8-4a3e-8dd6-922dcf4b22d0" />
Basicamente eso, hablamos entre el equipo de modularizar el codigo y dividirlo por responsabilidad, para que el trabajo sea escalable  
y llegar sin dificultad al checkpoint 3 (la ultima entrega)  

<img width="242" height="485" alt="image" src="https://github.com/user-attachments/assets/0b90aec3-e26d-413a-98fb-e28eff9d1b04" />   

### CHECKPOINT 1 FINALIZADO  
- [tp-2026-1c-418-im-a-teapot-48726846c14e319a419e35f2ccfb3e6798bcc09b.zip](https://github.com/user-attachments/files/30524582/tp-2026-1c-418-im-a-teapot-48726846c14e319a419e35f2ccfb3e6798bcc09b.zip)

## Desarrollo Checkpoint 2  
**ETAPA DE PLANEACIÓN:** Bueno, con el checkpoint 1 los modulos ya se conectan, todo bien, pero ahora toca definicir el protocolo  
de comunicación de que mensajes se manda cada módulo y en que orden  

Para eso tendras que leer una y otra e otra (varias veces) resaltando cada punto donde un modulo **le pide algo a otro o le responde**,  
y a cada uno de esos mensajes asignarle un codigo de operacion que lo identifique  
Ponele, cuando la CPU necesita ejecutar, le pide el contexto a memoria con SOLICITAR_CONTEXTP y memoria le responde con ENVIAR_CONTEXTO, asi de facil

<img width="392" height="936" alt="image" src="https://github.com/user-attachments/assets/0e7aeebd-e955-4159-8472-c0aaf164486d" />  

 Con todos esos codigos definidos, el siguiente paso fue modelar el recorrido completo de un proceso (ahi dejo mi diagrama de secuencia  
 medio raro jaja), mas que nada para saber como se encadenan los mensajes entre los demas modulos a lo largo de la vida del proceso, de paso 
 te ayuda a ver si te falto algun codigo de operacion o hay alguno que sobra 
<img width="1672" height="1133" alt="image" src="https://github.com/user-attachments/assets/322b12c9-3bda-46fc-b1c8-809001c2409e" />  
Definir bien los protocolos y que el equipo tambien entienda lo que estas agregando, porque puede pasar que agreguen protocolos de mas  
que signifiquen lo mismo pero lo unico que cambia es el nombre (para evitar el retrabajo)
<img width="2176" height="782" alt="image" src="https://github.com/user-attachments/assets/88623648-4119-49b3-8f85-7cddb7abdd47" />

 ### CHECKPOINT 2 FINALIZADO  
- [tp-2026-1c-418-im-a-teapot-9512aa5c4b01edc036605723193327b2b05f70af.zip](https://github.com/user-attachments/files/30525267/tp-2026-1c-418-im-a-teapot-9512aa5c4b01edc036605723193327b2b05f70af.zip)

## Desarrollo Checkpoint 3  
- [tp-2026-1c-418-im-a-teapot-abace6173f924ee2c7ec192b14cbfe05e7665ab9.zip](https://github.com/user-attachments/files/30525293/tp-2026-1c-418-im-a-teapot-abace6173f924ee2c7ec192b14cbfe05e7665ab9.zip)


# Aporte  
<img width="1617" height="907" alt="image" src="https://github.com/user-attachments/assets/07917ca1-87e3-4c41-b87a-fa91addf0e32" />  
<img width="1606" height="1198" alt="image" src="https://github.com/user-attachments/assets/fdd81146-674b-45b8-8c23-9b72a60c8a5c" />  
<img width="1607" height="1213" alt="image" src="https://github.com/user-attachments/assets/93ad97c8-7d1f-47cc-a9af-cbe7370b61c2" />  
<img width="1602" height="1215" alt="image" src="https://github.com/user-attachments/assets/c041723c-35f4-41ce-a2c9-a8336a1e11c0" />  
<img width="1613" height="475" alt="image" src="https://github.com/user-attachments/assets/2b81e000-975a-4715-9c1f-b5b4874a736f" />  
