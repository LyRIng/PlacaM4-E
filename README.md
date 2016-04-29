## M4/E Placa de Entrada/Salida y su programación en C

###Introducción
La M4/E de L&R Ingeniería es una placa periférica orientada a su utilización en conjunto con el módulo de CPU CL2bm1, y funciona como unidad de expansión de entradas y salidas digitales y entradas analógicas en un formato compatible con gabinetes para riel DIN (modelo DIN840). Se basa en un controlador CY8C29466 de la línea PSoC 1 (Programmable System-on-Chip, de Cypress Semiconductor) [[1]] (https://github.com/LyRIng/PlacaM4-E/blob/master/README.md#Referencias) y cuenta con una interfase para programación ISP (In-System Programming). Esta familia de controladores cuenta internamente con módulos configurables analógicos y digitales, lo cual les da una gran flexibilidad para adaptarse a cambios de requerimientos y diseño. Un diagrama en bloques de la placa M4/E y sus componentes principales puede observarse en la Figura 1. La parte superior funciona como una expansión directa de la placa principal CL2bm1 (4 entradas y una salida a relay K2), mientras que la parte inferior incluye el controlador PSoC, un conector para bus I2C para interfase a la placa principal, las señales de entrada digitales y analógicas y las salidas digitales (entre ellas el relay KAUX, conectado al puerto P0.2). Además existe un puerto COM de niveles TTL.

#![Figura 1: Diagrama de M4/E, placa auxiliar modular con conexión I2C a la CL2bm1](https://raw.githubusercontent.com/LyRIng/PlacaM4-E/master/M4-Expansion_Board.jpg)
*Figura 1: Diagrama de M4/E, placa auxiliar modular con conexión I2C a la CL2bm1*

Como parte del presente proyecto se puede acceder en distintos directorios al esquemático eléctrico de la placa, y a información descriptiva de la placa principal. Además, se explica un programa típico residente en el controlador, y se da acceso al código fuente de dicho programa.

###Programación
La M4/E puede funcionar como periférico autónomo, o conectarse con una placa CPU principal. Requiere una fuente de alimentación de corriente continua típicamente de 9 a 16V, que es internamente regulada a 5V. En cualquier caso, debe programarse el controlador PSoC para realizar alguna función útil, y esto se logra utilizando el software gratuito PSoC Designer [2] (corre bajo Windows) que incluye un compilador de lenguaje C, y alguna interfase de programación que convierta desde USB a las señales ISP (In System Programming) del controlador, que cuenta con 32 KB de memoria Flash interna para almacenamiento de programas del usuario. Dichas interfases son económicas (por ejemplo el Cypress MiniProg1, alrededor de usd 30). Desde el punto de vista del programador, la placa M4/E aparece como se indica en la Figura 2.

#![Figura 2](https://raw.githubusercontent.com/LyRIng/PlacaM4-E/master/Diagr_l%C3%B3gico.jpg)
*Figura 2: Diagrama lógico de E/S de la placa M4/E*

En este proyecto se proporciona un archivo ZIP que es posible importar en el PSoC Designer, que configura el controlador PSoC para una aplicación típica, consistente de un lazo de monitoreo de entradas y actualización en registros de su estado, y recepción de cambios ordenados por el control principal en las salidas. Dichos registros se agrupan en forma de tabla y son accesibles vía el bus I2C, a través de una API (Application Program Interface). Asimismo, el estado interno se envía continuamente a través del puerto serie configurado en el controlador PSoC.

En la Figura 3 se muestra una placa M4/E en operación. Varias de estas placas [3] se encuentran en operación continua desde 2010 en diversos proyectos, en la mayoría de las aplicaciones relacionadas con energías renovables (solar, eólica de baja potencia).

#![Figura 3](https://raw.githubusercontent.com/LyRIng/PlacaM4-E/master/Foto_M4E.jpg)
*Figura 3: Foto en detalle del M4/E, en conexión con la CL2bm1 a través de I2C.*

###Referencias
[1 - http://www.cypress.com/products/psoc-1] (http://www.cypress.com/products/psoc-1)

[2 - http://www.cypress.com/documentation/software-and-drivers/psoc-designer-54-sp1?source=search&cat=software_tools] (http://www.cypress.com/documentation/software-and-drivers/psoc-designer-54-sp1?source=search&cat=software_tools)

[3 - http://www.lyr-ing.com/Embedded/LyRAVR_CySp.htm] (http://www.lyr-ing.com/Embedded/LyRAVR_CySp.htm)

