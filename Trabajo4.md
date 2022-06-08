##Varray Telefonos
``` sql
CREATE TYPE TELEFONO AS VARRAY(2) OF VARCHAR2(15);
```
##Varray Notas
``` sql
CREATE TYPE NOTAS AS VARRAY(5) OF NUMBER(4,2);
```
##Tipo Asignaturas-Notas
``` sql
create or replace NONEDITIONABLE TYPE ASIG_NOTA AS OBJECT(
    ASIG TASIGNATURAS,
    NOTA NOTAS
); 
```
##Tabla anidada de Asignaturas-Notas
``` sql
create or replace NONEDITIONABLE TYPE ASIG_NOTA_ANIDADA AS TABLE OF ASIG_NOTA;

```
##Tipo Alumno
``` sql
create or replace NONEDITIONABLE TYPE ALUMNO2 UNDER PERSONA(
    DNI VARCHAR2(10),
    TELEF TELEFONO,
    ID_CURSO NUMBER(4),
    CURSO REF TCURSOS
    ANIDADA ASIG_NOTA_ANIDADA
);
NESTED TABLE ANIDADA STORE AS ASIGNOTA_ANIDADA
```
##Tabla Alumno
``` sql
CREATE TABLE TABLA_ALUMNOS OF ALUMNO2(
  DNI PRIMARY KEY
);
```
##Tipo Notas
``` sql
create or replace NONEDITIONABLE TYPE TNOTAS AS OBJECT(
    DNI VARCHAR2(10),
    COD_ASIG NUMBER(4),
    NOTA NOTAS
);
```
##Tipo Cursos
``` sql
create or replace NONEDITIONABLE TYPE TCURSOS AS OBJECT(
    ID_CURSO NUMBER(4),
    DESCRIPCION VARCHAR2(60),
    NIVEL VARCHAR2(30),
    TURNO CHAR(1),
    ALUMNO REF ALUMNO2
);
```

##Tabla Cursos
``` sql
CREATE TABLE TABLA_CURSOS OF TCURSOS(
    ID_CURSO PRIMARY KEY
);
```

##Tipo Asignaturas
``` sql
create or replace NONEDITIONABLE TYPE TASIGNATURAS AS OBJECT(
    COD_ASIG NUMBER(4),
    NOMBRE VARCHAR2(80),
    TIPO CHAR(1)
);
```
##Tabla Asignaturas
``` sql
CREATE TABLE TABLA_ASIGNATURAS OF TASIGNATURAS(
  COD_ASIG PRIMARY KEY
);
```
##Procedimieto Almacenado
``` sql
create or replace procedure show
(DNI IN VARCHAR2)
as
    begin
    SELECT NOMBRE,DIRECCION.CALLE,DIRECCION.CIUDAD,ANIDADA.ASIGNATURA,ANIDADA.NOTA FROM TABLA_ALUMNOS;
    
    end show;
    ```
