# 1-poligono-
import bpy
import math
CODIGO:
# Eliminar objetos existentes (opcional)
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros del polígono
num_lados = 6  # Cambia este valor para diferentes polígonos
radio = 2.0    # Tamaño del polígono
nombre_objeto = "Poligono_Regular"

# Crear datos de malla y objeto
malla = bpy.data.meshes.new(nombre_objeto + "_mesh")
objeto = bpy.data.objects.new(nombre_objeto, malla)

# Agregar objeto a la escena
colleccion = bpy.context.collection
colleccion.objects.link(objeto)
bpy.context.view_layer.objects.active = objeto
objeto.select_set(True)

# Calcular vértices del polígono
vertices = []
for i in range(num_lados):
    angulo = 2 * math.pi * i / num_lados
    x = radio * math.cos(angulo)
    y = radio * math.sin(angulo)
    z = 0.0
    vertices.append((x, y, z))

# Definir aristas (para contorno) o caras (para relleno)
aristas = []
for i in range(num_lados):
    aristas.append((i, (i + 1) % num_lados))
    
DESCRIPCION:
1. Preparación de la escena: Primero eliminE todos los objetos existentes (como el cubo inicial) para trabajar en una escena limpia, lo que me permitió centrarme únicamente en el nuevo polígono.
​
2. Definición de parámetros: Elegi configurar el polígono con los valores establecidos en el código: un total de 6 lados (formando un hexágono regular), un radio de 2.0 unidades para darle tamaño, y le asigne el nombre "Poligono_Regular" para identificarlo fácilmente en la escena.
​
3. Creación del objeto y malla: Genere una nueva malla de datos y la vincule a un objeto 3D. Luego agregue este objeto a la colección activa de la escena y lo seleccione como objeto activo, para que apareciera visible en el viewport.
​
4. Cálculo de vértices: Use cálculos matemáticos basados en funciones trigonométricas (coseno y seno) para determinar la posición de cada vértice alrededor de un centro común. Cada vértice se colocó a la misma distancia del centro (el radio definido) y separado por un ángulo igual (360° dividido entre el número de lados), garantizando que el polígono fuera regular.
​
5. Definición de aristas: Conecte cada vértice con el siguiente para formar los bordes del polígono, y asegure que el último vértice se uniera con el primero para cerrar la figura.
​
6. Generación y actualización de la malla: Finalmente, cree la malla del objeto usando los vértices y aristas calculados, y actualize los datos de la malla para que Blender mostrara el polígono correctamente en la escena.
# Crear malla con vértices y aristas
malla.from_pydata(vertices, aristas, [])
malla.update(calc_edges=True)
