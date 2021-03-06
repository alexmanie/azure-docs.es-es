---
title: Configuración de alertas de un servidor flexible de Azure Database for PostgreSQL mediante Azure Portal
description: En este artículo se describe cómo configurar alertas de métricas para un servidor flexible de Azure Database for PostgreSQL y cómo acceder a ellas mediante Azure Portal.
author: lfittl-msft
ms.author: lufittl
ms.service: postgresql
ms.topic: conceptual
ms.date: 09/22/2020
ms.openlocfilehash: ac252c3898eb014885bf9a6bf6bdedb7db74fb62
ms.sourcegitcommit: d767156543e16e816fc8a0c3777f033d649ffd3c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2020
ms.locfileid: "92545844"
---
# <a name="use-the-azure-portal-to-set-up-alerts-on-metrics-for-azure-database-for-postgresql---flexible-server"></a>Uso de Azure Portal para configurar alertas en las métricas de un servidor flexible de Azure Database for PostgreSQL

> [!IMPORTANT]
> La opción de implementación Servidor flexible de Azure Database for PostgreSQL está en versión preliminar

En este artículo se explica cómo configurar alertas de Azure Database for PostgreSQL mediante Azure Portal. Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure.

La alerta se desencadena cuando el valor de una métrica especificada cruza el umbral que se ha asignado. La alerta se desencadena tanto la primera vez que se cumple la condición como después, cuando dicha condición deja de cumplirse.

Puede configurar una alerta para realizar las siguientes acciones cuando se desencadene:

* Enviar notificaciones de correo electrónico al administrador y los coadministradores del servicio.
* Enviar un correo electrónico a direcciones de correo electrónico adicionales que especifique.
* Llamar a un webhook.

Puede obtener información sobre las reglas de alerta y configurarlas mediante:

* [Azure Portal](../../azure-monitor/platform/alerts-metric.md#create-with-azure-portal)
* [CLI de Azure](../../azure-monitor/platform/alerts-metric.md#with-azure-cli)
* [API de REST de Azure Monitor](/rest/api/monitor/metricalerts)

## <a name="create-an-alert-rule-on-a-metric-from-the-azure-portal"></a>Creación de una regla de alerta sobre una métrica desde Azure Portal

1. En [Azure Portal](https://portal.azure.com/), seleccione el servidor de Azure Database for PostgreSQL que quiera supervisar.

2. En la sección **Supervisión** de la barra lateral, seleccione **Alertas** , tal y como se muestra a continuación:

   :::image type="content" source="./media/howto-alert-on-metrics/2-alert-rules.png" alt-text="Selección de Reglas de alerta":::

3. Seleccione **Agregar alerta de métrica** (icono +).

4. Se abre la página **Crear regla** , tal y como se muestra a continuación. Rellene la información necesaria:

   :::image type="content" source="./media/howto-alert-on-metrics/4-add-rule-form.png" alt-text="Selección de Reglas de alerta":::

5. En la sección **Condición** , seleccione **Agregar condición** .

6. Seleccione una métrica de la lista de señales sobre las que desea recibir alertas. En este ejemplo, seleccione "Porcentaje de almacenamiento".

   :::image type="content" source="./media/howto-alert-on-metrics/6-configure-signal-logic.png" alt-text="Selección de Reglas de alerta":::

7. Configure la lógica de alerta incluida la **condición** (p. ej., "Mayor que") el **umbral** (p. ej., 85 %), la **agregación de tiempo** , el **período** de tiempo de la regla de métrica que debe transcurrir para que se desencadene la alerta (p. ej., "En los últimos 30 minutos") y la **frecuencia** .

   Seleccione **Listo** cuando haya terminado.

   :::image type="content" source="./media/howto-alert-on-metrics/7-set-threshold-time.png" alt-text="Selección de Reglas de alerta" para seleccionar los propietarios, colaboradores y lectores de la suscripción que recibirán las notificaciones.

    2. También puede indicar un identificador URI válido en el campo **Webhook** si quiere llamarlo cuando se active la alerta.

    3. Cuando haya terminado, seleccione **Aceptar** .

    :::image type="content" source="./media/howto-alert-on-metrics/10-action-group-type.png" alt-text="Selección de Reglas de alerta":::

11. Especifique el nombre de la regla de alertas, la descripción y la gravedad.

    :::image type="content" source="./media/howto-alert-on-metrics/11-name-description-severity.png" alt-text="Selección de Reglas de alerta"::: 

12. Seleccione **Crear regla de alerta** para crear la alerta.

    En cuestión de minutos, se activa la alerta y se desencadena tal como se describió anteriormente.

## <a name="manage-your-alerts"></a>Administración de alertas

Una vez que haya creado una alerta, puede seleccionarla y realizar las acciones siguientes:

* Ver un gráfico que muestre el umbral de las métricas y los valores reales del día anterior en relación con esta alerta.
* **Editar** o **eliminar** la regla de alerta.
* **Deshabilitar** o **habilitar** la alerta, si quiere detener temporalmente o reanudar la recepción de notificaciones.

## <a name="next-steps"></a>Pasos siguientes

* Obtenga más información sobre cómo [configurar webhooks en las alertas](../../azure-monitor/platform/alerts-webhooks.md).
* Obtenga [información general sobre la colección de métricas](../../azure-monitor/platform/data-platform.md) para garantizar que el servicio está disponible y que responder adecuadamente.