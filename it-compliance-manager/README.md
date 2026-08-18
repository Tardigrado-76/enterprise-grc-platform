# IT Compliance Manager

## Propósito Operativo
Este módulo es el **CLI Engine de evaluación continua de conformidad**. Está diseñado para auditar infraestructuras IT de forma automatizada, contrastar configuraciones técnicas contra regulaciones de alto nivel, y mapear los hallazgos a controles estandarizados.

## Pipeline de Evaluación

```mermaid
flowchart TD
    %% Node styles
    classDef input fill:#333,stroke:#fff,stroke-width:2px,color:#fff;
    classDef process fill:#1f4287,stroke:#fff,stroke-width:2px,color:#fff;
    classDef framework fill:#a00,stroke:#fff,stroke-width:2px,color:#fff;
    classDef output fill:#278ea5,stroke:#fff,stroke-width:2px,color:#fff;

    Input[Input Target\nConfig / Cloud / Sys]:::input --> Parser[Parser\nAST / SysConfig]:::process
    
    Parser --> Evaluators[Evaluators]:::process
    
    Evaluators -.-> DORA[DORA]:::framework
    Evaluators -.-> NIS2[NIS2]:::framework
    Evaluators -.-> ENS[ENS]:::framework
    
    DORA --> Mapping[ISO/SOC2 Mapping Engine]:::process
    NIS2 --> Mapping
    ENS --> Mapping
    
    Mapping --> Sealer[Sealer\nIntegrity Signature]:::process
    Sealer --> Output[Output Reports]:::output
```

## Documentación de Parámetros CLI

El motor principal se invoca a través de una interfaz de línea de comandos, que acepta los siguientes argumentos:

- `--input`: Ruta al archivo, directorio o URI de nube que se auditará.
- `--framework`: Regulaciones a aplicar en la evaluación (ej. `dora`, `nis2`, `ens`). Puede ser una lista separada por comas.
- `--company`: Identificador o nombre de la organización para el etiquetado de reportes.
- `--output`: Ruta de destino para la exportación de resultados.
- `--format`: Formato de salida deseado (`json`, `csv`, `pdf`, `html`).

## Mapeo Automático de Hallazgos
Una característica clave del `IT Compliance Manager` es su capacidad para traducir hallazgos técnicos crudos a controles auditables por terceros:
- **ISO/IEC 27001:2022:** Transposición automática de vulnerabilidades hacia los controles del Anexo A (ej. A.8.12 Prevención de fuga de información).
- **SOC 2:** Vinculación directa con los *Trust Services Criteria* (Seguridad, Disponibilidad, Integridad de procesamiento, Confidencialidad, Privacidad).
