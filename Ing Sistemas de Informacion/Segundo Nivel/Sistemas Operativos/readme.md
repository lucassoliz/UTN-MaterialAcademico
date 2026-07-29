# Sistemas Operativos -- Plug & Pray  
### Enunciado 
- [Plug & Pray Ultima version.pdf](https://github.com/user-attachments/files/30522500/Plug.Pray.Ultima.version.pdf)


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
