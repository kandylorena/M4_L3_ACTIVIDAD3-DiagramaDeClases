# M4_L3_ACTIVIDAD3-DiagramaDeClases
Diagrama de clases

# Sistema Educacional - Documentación del Diagrama de Clases

Este documento detalla el diseño de la arquitectura de software para el Sistema Educacional, 
---

## 1. Herencia (La Estructura de Personas)

Para evitar la duplicación se aplica **herencia**. Creé una clase base general que luego se especializa en dos perfiles específicos.

* **Clase principal Persona:** Centraliza los atributos comunes que comparten todos los usuarios del sistema (como nombre, apellido y correo electrónico). Utilizo una visibilidad **protegida (`#`)** para que únicamente las clases hijas puedan acceder de manera directa a ellos, exponiendo un método **público (`+`)** para resolver el nombre completo.
* **Clases Hijas Alumno y Profesor:** Ambas heredan la estructura fundamental de `Persona` (vinculadas mediante una relación lógica 1 a 1 en persistencia). Sin embargo, cada una encapsula sus propios datos de forma estrictamente **privada (`-`)**:
    * El **Alumno** maneja de forma exclusiva su matrícula, promedio general y los métodos para inscribir asignaturas o consultar sus calificaciones.
    * El **Profesor** gestiona su especialidad, salario y los métodos operativos para registrar notas o listar sus cursos asignados.

* **Asignatura:** Almacena los datos públicos de las materias de la malla curricular (nombre, código identificador y créditos académicos) y provee un método para obtener sus detalles.
* **Aula:** Define físicamente los espacios del establecimiento, controlando el número de sala, la capacidad máxima de alumnos y el edificio de ubicación.
* **Horario:** Gestiona las ventanas de tiempo cronológicas, controlando los días de la semana y las horas exactas de inicio y fin de cada bloque.
* **Evaluación:** Modela las calificaciones, exámenes, proyectos o tareas correspondientes a cada materia.

---

## 2. Visibilidad y Encapsulamiento

Para garantizar la integridad del estado de los objetos y evitar alteraciones indebidas o accesos no autorizados.

* **Privado (-):** Atributos críticos y sensibles (como _matricula, _promedio_general o _salario) están completamente ocultos para el exterior. La única vía para interactuar con ellos.
* **Protegido (#):** Utilizado en la superclase Persona (_nombre, _apellido, _email). Esto me permite un acceso directo, limpio y eficiente desde las clases derivadas (Alumno y Profesor) 
* **Público (+):**los métodos de comunicación del objeto (como calcularPond(), calificar() o inscribir_asignatura()). 

---

## 3. Relaciones  Cardinalidad


* **Herencia:** Representa la relación estricta. Un `Alumno` **es una** `Persona` y un `Profesor` **es una** `Persona`. Permite una reutilización óptima de código y una estructura polimórfica clara.
* **Asociación:** Es una relación independiente entre `Profesor` y `Asignatura`. Un profesor dicta una materia, pero ambos objetos tienen ciclos de vida separados; si el docente se retira de la institución, la asignatura permanece activa para ser asignada a otro profesional. Su cardinalidad es de uno a muchos ($1..*$).
* **Agregación (Relación Débil):** Conecta a `Alumno` con `Asignatura`. Los alumnos se inscriben y pertenecen a una materia. Es una relación débil: si la asignatura se cancela o se elimina de la planificación, los alumnos no desaparecen del sistema; sus perfiles y registros generales permanecen intactos.
* **Composición (Relación Fuerte):** Existe estrictamente entre `Asignatura` y `Evaluación`. Una evaluación (un examen parcial o un test) no tiene sentido de existir de manera aislada en el sistema; vive única y exclusivamente dentro del contexto de una materia. Definí que sus ciclos de vida estén íntimamente ligados: si la `Asignatura` se elimina, todas sus `Evaluaciones` se destruyen en cascada de forma automática.
* **Modelado del Cronograma:** Para armar la agenda escolar diaria, las entidades de `Aula` y `Asignatura` se vinculan con la clase `Horario`, determinando con precisión matemática *qué* materia se imparte, *dónde* (en qué espacio físico) y *en qué momento* exacto.

```
Enlace git 
https://github.com/kandylorena/M4_L3_ACTIVIDAD3-DiagramaDeClases.git

```