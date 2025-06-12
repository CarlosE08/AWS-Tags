
# 🏷️ AWS Resource Tag Manager

Este script en Python te permite **escanear recursos de AWS**, **aplicar etiquetas comunes**, **generar reportes Excel**, **eliminar/restaurar etiquetas** y mucho más usando el servicio `resourcegroupstaggingapi`. Todo está organizado por perfil de AWS y región (`us-east-1` por defecto).

---

## 🚀 Características principales

- ✅ **Escaneo de recursos etiquetados y no etiquetados**
- 📊 **Generación de reporte en Excel** con pestañas por tipo de recurso
- 🏷️ **Asignación inteligente de etiquetas** (solo a recursos sin etiquetas o con merge)
- ❌ **Eliminación controlada de etiquetas** agregadas por el script
- ♻️ **Restauración de etiquetas desde respaldo**
- 🔁 **Aplicación masiva de etiquetas a todos los recursos**
- 📁 Salidas organizadas por perfil en carpetas locales

---

## 📂 Estructura del proyecto

```
.
├── script.py
├── Etiquetas_Comunes.txt  # Archivo con etiquetas clave-valor a aplicar
└── <perfil AWS>/
    ├── reporte_etiquetas_aws_<perfil>.xlsx
    ├── recursos_etiquetados_<perfil>.txt
    └── respaldo_etiquetas_eliminadas_<perfil>.txt
```

---

## 📝 Formato de `Etiquetas_Comunes.txt`

Archivo plano donde cada línea representa una etiqueta:

```
Proyecto = MiProyecto
Ambiente = Producción
Owner = DevOps
```

También se añade automáticamente la etiqueta:

```
Added = Yes
```

---

## 📦 Requisitos

- Python 3.7+
- AWS CLI configurado con SSO y perfiles válidos
- Dependencias instaladas:

```bash
pip install boto3 openpyxl
```

---

## 🧭 Menú de operaciones

Al ejecutar el script, verás el siguiente menú:

```
📋 MENÚ DE OPERACIONES AWS
1. Escanear recursos y generar Excel
2. Asignar etiquetas comunes (solo recursos sin etiquetas)
3. Eliminar etiquetas comunes desde archivo
4. Asignar etiquetas comunes a todos (merge y sobrescribe claves coincidentes)
5. Restaurar etiquetas desde respaldo
```

---

## 🗂️ Detalles del reporte Excel

El archivo generado contiene 3 hojas:

- **ConEtiquetas**: Recursos organizados por tipo, con etiquetas mostradas en formato multi-línea.
- **SinEtiquetas**: Lista de recursos sin etiquetas.
- **Resumen**: Métricas globales del escaneo.

Además:
- Las celdas con `Added=Yes` se resaltan en verde.
- Las secciones de cada tipo de recurso tienen un encabezado gris con estilo.

---

## 🧠 Inteligencia del script

- Solo se etiquetan recursos que **no tienen etiquetas** o que **tienen `Added=Yes`** al eliminar.
- Detecta tipos de recurso a partir del ARN (S3, Lambda, EC2, etc.).
- Ignora recursos de `controltower`, `awsmanaged`, etc.

---

## 🔒 Seguridad y buenas prácticas

- No sobrescribe etiquetas ya existentes a menos que elijas la opción 4 (merge).
- Crea respaldos antes de eliminar etiquetas.
- Todos los cambios se registran en archivos `.txt`.

---

## 🛠️ Personalización

Puedes modificar:

- `AWS_REGION` si tu región no es `us-east-1`
- Colores en Excel (`COLOR_ADDED`)
- Palabras reservadas para evitar etiquetado (`es_recurso_etiquetable`)

---

## 📣 Créditos

Desarrollado por [Carlos Escobar](mailto:carlos.escobar@inbest.cloud) para facilitar el cumplimiento de políticas de etiquetado en AWS.

---

¡Etiqueta con confianza y genera visibilidad sobre tus recursos en la nube! ☁️✅
