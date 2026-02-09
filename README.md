# 📊 Proyecto de Análisis de Datos – Wide World Importers

## 🧠 Introducción

Este proyecto utiliza la base de datos **Wide World Importers**, una base de datos de ejemplo oficial de **Microsoft SQL Server**, diseñada para simular la operación completa de una empresa mayorista moderna.

Wide World Importers cubre procesos reales de negocio como:

* Ventas (Sales)
* Compras (Purchasing)
* Almacén e inventario (Warehouse)
* Finanzas y transacciones

La base de datos es ampliamente utilizada para **aprendizaje, pruebas y demostraciones** en SQL Server, modelado de datos y herramientas de Business Intelligence como Power BI.

En este proyecto, la base se utiliza como **fuente transaccional (OLTP)** y se construye una **capa analítica optimizada (OLAP)** mediante *Stored Procedures* (SP), pensados específicamente para su consumo en Power BI.

---

## 🎯 Objetivo del Proyecto

El objetivo principal es:

* Analizar procesos clave del negocio (ventas, compras e inventario)
* Diseñar un modelo analítico claro y eficiente
* Crear *facts* y *dimensions* sin mezclar granularidades
* Optimizar consultas para su uso en Power BI
* Documentar el modelo de forma clara y reutilizable

> ⚠️ En esta primera etapa **no se incluye Power BI**. El enfoque está en:
>
> * Comprensión de la base de datos
> * Diseño del modelo analítico
> * Construcción de Stored Procedures

Power BI se integrará en una fase posterior del proyecto.

---

## 🧱 Enfoque de Modelado

Se sigue una **arquitectura tipo estrella (Star Schema)**:

* **Dimensions** → contexto descriptivo
* **Facts** → eventos medibles

### Principios clave

* ❌ No mezclar hechos con dimensiones
* ❌ No unir múltiples tablas de hechos en un solo fact
* ✅ Respetar la granularidad de cada proceso
* ✅ SP específicos por dominio (Sales, Purchasing, Warehouse)

---

## 🛒 Dominio: Sales

### 📄 `dbo.sp_dim_customer_powerBI`

**Dimensión de clientes**

Proporciona el contexto necesario para analizar ventas por cliente.

Campos principales:

* Cliente
* Ciudad
* Categoría
* Condiciones de pago

---

### 📊 `dbo.sp_fact_sales_powerBI`

**Fact de ventas (Invoice Lines)**

Representa cada línea facturada como evento de negocio.

🎯 Preguntas de negocio que cubre este fact

✔ ¿Cuánto se vende?
✔ ¿Cuántas ventas se realizan?
✔ ¿Cuánto se vende por cliente?
✔ ¿Cuánto se vende por producto?
✔ ¿Cómo evolucionan las ventas en el tiempo?

---

### 📦 `dbo.sp_fact_orders_powerBI`

**Fact de órdenes**

Permite analizar el proceso previo a la venta.

🎯 Preguntas de negocio que cubre este fact

✔ ¿Cuántas órdenes se crean?
✔ ¿Cuántas se convierten en ventas?
✔ ¿Cuántas órdenes quedan pendientes?
✔ ¿Cuánto tiempo tarda una orden en facturarse?

---

### 💰 `dbo.sp_fact_customer_transactions_powerBI`

**Fact de transacciones financieras de clientes**

Analiza el comportamiento financiero posterior a la venta.

🎯 Preguntas de negocio que cubre este fact

✔ ¿Cuánto pagan los clientes?
✔ ¿Qué clientes tienen saldos pendientes?
✔ ¿Cuáles son los montos con y sin impuestos?
✔ ¿Cómo se comportan los pagos en el tiempo?

---

## 🚚 Dominio: Purchasing

### 🏷 `dbo.sp_dim_supplier_powerBI`

**Dimensión de proveedores**

Describe a los proveedores desde una perspectiva analítica.

Incluye:

* Nombre del proveedor
* Categoría
* Ciudad de entrega
* Condiciones de pago

---

### 💸 `dbo.sp_fact_supplier_transactions_powerBI`

**Fact de transacciones con proveedores**

Analiza los movimientos financieros asociados a compras.

🎯 Preguntas de negocio que cubre este fact

✔ ¿Cuánto se compra a proveedores?
✔ ¿Cuánto se paga en impuestos?
✔ ¿Qué transacciones están finalizadas?
✔ ¿Cómo evolucionan las compras en el tiempo?

---

### 📦 `dbo.sp_fact_purchases_powerBI`

**Fact de órdenes de compra**

Permite evaluar el desempeño del proceso de abastecimiento.

🎯 Preguntas de negocio que cubre este fact

✔ ¿Cuántas órdenes de compra se crean?
✔ ¿Cuántas se finalizan?
✔ ¿Cuántas están pendientes?
✔ ¿Se cumple la fecha estimada de entrega?
✔ ¿Qué proveedores cumplen y cuáles no?

---

## 🏭 Dominio: Warehouse

### 🧾 `dbo.sp_dim_stock_item_powerBI`

**Dimensión de productos (stock items)**

Describe los productos desde el punto de vista del inventario.

Incluye:

* Producto
* Marca
* Proveedor
* Tipo de empaque
* Requiere cadena de frío
* Tiempo de reposición (Lead Time)

---

### 📊 `dbo.sp_fact_stock_levels_powerBI`

**Fact de niveles de inventario**

Mide el estado actual del stock.

🎯 Preguntas de negocio que cubre este fact

✔ ¿Qué items tenemos en stock?
✔ ¿Qué cantidades hay disponibles?
✔ ¿Cuál es el valor aproximado del inventario?
✔ ¿Dónde está ubicado cada producto?
✔ ¿Qué productos requieren refrigeración?

---

### 🔄 `dbo.sp_fact_stock_transactions_powerBI`

**Fact de movimientos de inventario**

Analiza la rotación y dinámica del almacén.

🎯 Preguntas de negocio que cubre este fact

✔ ¿Qué productos rotan más?
✔ ¿Con qué frecuencia se mueven?
✔ ¿Cómo varía el inventario en el tiempo?
✔ ¿Qué productos tienen mayor movimiento?

---


📌 *Este proyecto está diseñado con fines educativos y de aprendizaje avanzado en análisis de datos, SQL Server y Power BI.*
