---
title: archivo de inclusión
description: archivo de inclusión
services: virtual-machines
author: roygara
ms.service: virtual-machines
ms.topic: include
ms.date: 03/05/2020
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: f4af8a150b062526f08c1d15581ec26e2fe12d8c
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "95992916"
---
- Las instantáneas incrementales no se pueden mover entre suscripciones.
- En este momento, solo se pueden generar URI de SAS de hasta cinco instantáneas de una determinada familia de instantáneas en un momento dado.
- No se puede crear una instantánea incremental para un disco determinado fuera de la suscripción de ese disco.
- Se pueden crear hasta siete instantáneas incrementales por disco cada cinco minutos.
- Se pueden crear un total de 200 instantáneas incrementales para un único disco.
- No se pueden obtener los cambios entre las instantáneas tomadas antes y después de cambiar el tamaño del disco primario en un límite de 4 TB. Por ejemplo, tomó una instantánea incremental denominada instantánea-a cuando el tamaño de un disco era de 2 TB. Ahora ha aumentado el tamaño del disco a 6 TB y se ha tomado otra instantánea incremental denominada instantánea-b. No se pueden obtener los cambios entre la instantánea-a y la instantánea-b. Es preciso volver a descargar la copia completa de la instantánea-b creada después del cambio de tamaño. Posteriormente, se pueden obtener los cambios entre la instantánea denominada instantánea-b y las instantáneas creadas después de la instantánea denominada instantánea-b. 
