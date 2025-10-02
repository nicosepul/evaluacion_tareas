Consultas del ORM


Abre shell:
python manage.py shell


Ejemplos de consultas y comandos

from tareas.models import Tarea
from django.utils import timezone


# 1. Crear una tarea
Tarea.objects.create(titulo='Comprar pan', descripcion='Ir a la panadería', prioridad=2, vigente=True, fecha_limite='2025-10-05')


# 2. Crear con instancia y save
t = Tarea(titulo='Estudiar Django', descripcion='Practicar vistas genéricas', prioridad=1)
t.save()


# 3. Listar todas las tareas
Tarea.objects.all()


# 4. Filtrar vigentes
Tarea.objects.filter(vigente=True)


# 5. Ordenar por prioridad ascendente
Tarea.objects.all().order_by('prioridad')


# 6. Obtener una tarea por pk
Tarea.objects.get(pk=1)


# 7. Actualizar un campo
Tarea.objects.filter(pk=1).update(prioridad=5)


# 8. Incrementar prioridad (ejemplo usando F)
from django.db.models import F
Tarea.objects.filter(pk=2).update(prioridad=F('prioridad') + 1)


# 9. Borrar una tarea
Tarea.objects.filter(pk=3).delete()


# 10. Consultas más útiles
# Tareas con prioridad mayor a 2
Tarea.objects.filter(prioridad__gt=2)


# 11. Buscar en título/descripción (icontains)
Tarea.objects.filter(titulo__icontains='django')


# 12. Conteo
Tarea.objects.count()


# 13. Agregar o actualizar con setOnInsert equivalente (get_or_create)
Tarea.objects.get_or_create(titulo='Tarea única', defaults={'descripcion':'auto creada', 'prioridad':3})