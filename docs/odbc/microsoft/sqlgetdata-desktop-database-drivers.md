---
description: SQLGetData (Drivers de banco de dados de área de trabalho)
title: SQLGetData (drivers de banco de dados de desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cfce744c3f4a2e0e4d9fcb054a8226538537bdcf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340223"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (Drivers de banco de dados de área de trabalho)
Essa função pode recuperar dados de qualquer coluna, quer haja ou não colunas associadas depois dela e independentemente da ordem na qual as colunas são recuperadas.  
  
> [!NOTE]  
>  \*pcbValue em **SQLGetData** pode retornar duas vezes mais caracteres que realmente estão disponíveis ao associar dados ANSI com mais de 510 caracteres em um banco de dado Jet 4,0. Os valores de caractere de 510 ou menos retornarão o cbValue real.
