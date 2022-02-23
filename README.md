# GDADD
Gestión de administración de datos

-- Punto numero 1

-- Visualizacion de los precios y sus categorias 

select 

   p.precio,
   ca.nombre

from productos p

left join categorias ca on p.id_categoria = ca.id_categoria
where ca.nombre != 'Ferreteria'

-- Asignacion de incremento del 15% a categorias diferente a Ferreteria

update p 
set p.precio = p.precio*1.15
from productos p
left join categorias ca on p.id_categoria = ca.id_categoria
where ca.nombre != 'Ferreteria'

-- Punto numero 2


-- Visualizacion de productos pagados con bitcoin

select 

  mp.nombre,
  p.nombre,
  p.precio
  

from modo_pagos mp
join facturas f on mp.num_pago= f.num_pago
join detalles d on f.num_factura=d.id_factura
join productos p on d.id_producto=p.id_producto
where mp.nombre = 'bitcoin'

-- asignacion del decremento del 20% a productos pagados con bitcoin 

update p
set p.precio = p.precio*0.8
from productos p
join detalles d on p.id_producto=d.id_producto
join facturas f on d.id_factura = f.num_factura
join modo_pagos mp on f.num_pago = mp.num_pago
where mp.nombre = 'bitcoin'

-- punto numero 3

-- Visualizacion de clietes que no han realizado compras 

select

c.nombre
--f.num_factura

from clientes c
left join facturas f on c.id_cliente = f.id_cliente
where f.id_cliente is null  

-- eliminacion de los clientes que no han realizado compras 

delete c

from clientes c

left join facturas f on c.id_cliente = f.id_cliente
where f.id_cliente is null 



-- Punto numero 4

-- Visualizacion de productos que empiezan por 'C' y tienen metodo de pago diferente a tarjeta débito

select 
  mp.nombre,
  p.nombre,
  p.stock
    
from modo_pagos mp

join facturas f on mp.num_pago= f.num_pago
join detalles d on f.num_factura=d.id_factura
join productos p on d.id_producto=p.id_producto
where mp.nombre != 'tarjeta débito' and p.nombre like 'C%'

-- Asignacion de incremento del stock de los productos cuyo nombre inician con la letra 'C' y que no hayan sido pagados con 'tarjeta débito'



update p
 
 set p.stock = p.stock+1

from productos p

join detalles d on p.id_producto=d.id_producto
join facturas f on d.id_factura = f.num_factura
join modo_pagos mp on f.num_pago = mp.num_pago
where mp.nombre != 'tarjeta débito' and p.nombre like 'C%'




