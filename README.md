# Convenciones para realizar el parcial grupal


**Nota 1:** Todas las funciones, triggers y procedimientos almacenados deben empezar con **DELIMITER $$;** y terminar con **DELIMITER ;**

**Nota 2:** Antes del DELIMITER $$; siempre se debe DROPEAR lo que se está creando, para evitar errores al ejecutar el script completo.

***

**Estructura Procedimientos Almacenados**
```
DROP PROCEDURE IF EXISTS SP_[NombreProcedimiento];
DELIMITER $$;
CREATE PROCEDURE SP_[NombreProcedimiento](IN [NombreParam] [Tipo], OUT [NombreParam] [Tipo])
BEGIN
    -- Cuerpo del procedimiento    
END $$;
DELIMITER ;
```
***
**Estructura Funciones Almacenadss**
```
DROP FUNCTION IF EXISTS FN_[NombreFunción];
DELIMITER $$;
CREATE FUNCTION FN_[NombreFunción]([NombreParam] [Tipo], [NombreParam] [Tipo])
RETURNS [Tipo] DETERMINISTIC
BEGIN
    -- Cuerpo de la función
    RETURN [Variable];
END $$;
DELIMITER ;
```
***
**Estructura Triggers**
```
DROP TRIGGER IF EXISTS [NombreTrigger];
DELIMITER $$;
CREATE TRIGGER [NombreTrigger]
    AFTER INSERT ON [NombreTabla] FOR EACH ROW
BEGIN
    -- Cuerpo del trigger
END $$;
DELIMITER ;
```
***
**Estructura Transacción**
```
START TRANSACTION;
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        -- Guardamos informacion del error
        GET DIAGNOSTICS CONDITION 1
            state = RETURNED_SQLSTATE,
            errorNumber    = MYSQL_ERRNO,
            message    = MESSAGE_TEXT;
        -- Cancelamos la transaccion
        ROLLBACK;
        -- El SP devuelve la info del error o NULL en esas variables si no hubo errores
        SELECT state, errorNumber, message;
    END;

    -- Cuerpo de la transacción (Los Insert/Update/Delete)

COMMIT;
END;
```



```
SELECT [Alias.NombreColumna]
FROM [NombreTabla] AS [Alias]
WHERE

```

