---
title: Procedimientos para solucionar los errores de runtime de U-SQL de Azure Data Lake Analytics
description: Obtenga información sobre cómo solucionar los errores de runtime de U-SQL.
ms.reviewer: jasonh
ms.service: data-lake-analytics
ms.topic: troubleshooting
ms.date: 10/10/2019
ms.openlocfilehash: 41b7c80c85331f288343351749e6b2e5292b30c6
ms.sourcegitcommit: 30906a33111621bc7b9b245a9a2ab2e33310f33f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2020
ms.locfileid: "95241614"
---
# <a name="learn-how-to-troubleshoot-u-sql-runtime-failures-due-to-runtime-changes"></a>Información sobre cómo solucionar errores de runtime de U-SQL debido a cambios en el runtime

El runtime U-SQL de Azure Data Lake, incluidos el compilador, el optimizador y el administrador de trabajos, es lo que procesa el código de U-SQL.

## <a name="choosing-your-u-sql-runtime-version"></a>Elección de la versión de runtime de U-SQL

Al enviar trabajos de U-SQL desde Visual Studio, el SDK de ADL o el portal de Azure Data Lake Analytics, el trabajo utilizará el runtime predeterminado disponible actualmente. Las versiones nuevas del runtime de U-SQL se publican de forma regular e incluyen tanto las actualizaciones secundarias como las correcciones de seguridad.

También se puede optar por una versión de runtime personalizada, ya sea porque quiere probar una nueva actualización, debe permanecer en una versión anterior de un runtime o bien porque se le ha proporcionado una revisión para un problema notificado que no puede esperar a la nueva actualización periódica.

> [!CAUTION]
> La elección de un runtime diferente del predeterminado tiene la posibilidad de interrumpir los trabajos de U-SQL. Use estas otras versiones solo para pruebas.

En raras ocasiones, Soporte técnico de Microsoft puede anclar una versión distinta de un runtime como valor predeterminado para su cuenta. Asegúrese de revertir este anclaje lo antes posible. Si se permanece anclado a esa versión, expirará más adelante.

### <a name="monitoring-your-jobs-u-sql-runtime-version"></a>Supervisión de la versión de runtime de los trabajos de U-SQL

Puede ver el historial de la versión en tiempo de ejecución que han usado los trabajos pasados en el historial de trabajos de su cuenta mediante el explorador de trabajos de Visual Studio o el historial de trabajos de Azure Portal.

1. En Azure Portal, vaya a la cuenta de Data Lake Analytics.
2. Seleccione **Ver todos los trabajos**. Aparece una lista de todos los trabajos activos y finalizados recientemente en la cuenta.
3. De forma opcional, haga clic en **Filtrar** para encontrar los trabajos por los valores **Intervalo de tiempo**, **Nombre del trabajo** y **Autor**.
4. Puede ver el runtime que se usa en los trabajos completados.

![Visualización de la versión de runtime de un trabajo anterior](./media/runtime-troubleshoot/prior-job-usql-runtime-version-.png)

Las versiones disponibles de runtime cambian con el tiempo. El tiempo de ejecución predeterminado siempre se denomina "predeterminado". El tiempo de ejecución anterior se mantiene disponible durante algún tiempo, junto con otros tiempos de ejecución especiales, por diversos motivos. Los runtimes con nombres explícitos suelen seguir el formato siguiente (las partes variables se ponen en cursiva y [] indica partes opcionales):

release_YYYYMMDD_adl_buildno[_modifier]

Por ejemplo, release_20190318_adl_3394512_2 se refiere a la segunda versión de la compilación 3394512 de la versión de runtime del 18 de marzo de 2019 y release_20190318_adl_3394512_private se refiere a una compilación privada de la misma versión. Nota: La fecha se relaciona con el momento en que se ha realizado la última inserción en el repositorio para esa versión y no necesariamente en la fecha de lanzamiento oficial.


## <a name="troubleshooting-u-sql-runtime-version-issues"></a>Solución de incidencias de versión de runtime de U-SQL

Hay dos incidencias posibles de versión de runtime que se pueden encontrar:

1. Un script o algún código de usuario está cambiando el comportamiento de una versión a la siguiente. Estos cambios importantes se comunican normalmente de antemano con la publicación de notas de la versión. Si encuentra un cambio importante, póngase en contacto con Soporte técnico de Microsoft para informar de este comportamiento significativo (en caso de que no se haya documentado todavía) y envíe los trabajos con la versión de runtime anterior.

2. Ha estado usando un runtime no predeterminado, ya sea explícita o implícitamente, cuando se ha anclado a su cuenta, y ese runtime se ha quitado después de un tiempo. Si encuentra runtimes que faltan, actualice los scripts para que se ejecuten con el runtime predeterminado actual. Si necesita más tiempo, póngase en contacto con Soporte técnico de Microsoft.

## <a name="known-issues"></a>Problemas conocidos

* La referencia al archivo Newtonsoft.json, versión 12.0.3 o posterior, en un script USQL provocará el siguiente error de compilación:

    *"Es probable que los trabajos que se ejecutan en la cuenta de Data Lake Analytics funcionen con lentitud o no se completen. Un problema inesperado nos impide restaurar automáticamente esta funcionalidad en la cuenta de Azure Data Lake Analytics, pero nos hemos puesto en contacto con los ingenieros de Azure Data Lake para que lo investiguen".*  

    Donde la pila de llamadas contendrá:  
    `System.IndexOutOfRangeException: Index was outside the bounds of the array.`  
    `at Roslyn.Compilers.MetadataReader.PEFile.CustomAttributeTableReader.get_Item(UInt32 rowId)`  
    `...`

    **Solución**: Use el archivo Newtonsoft.json v12.0.2 o inferior.


## <a name="see-also"></a>Consulte también

- [Información general de Análisis de Azure Data Lake](data-lake-analytics-overview.md)
- [Administración de Azure Data Lake Analytics con Azure Portal](data-lake-analytics-manage-use-portal.md)
- [Supervisión de trabajos en Azure Data Lake Analytics mediante Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
