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
