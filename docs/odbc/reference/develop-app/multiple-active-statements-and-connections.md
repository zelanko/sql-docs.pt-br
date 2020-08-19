---
description: Várias instruções e conexões ativas
title: Várias instruções e conexões ativas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56897dedbd1bf0d96dfa73f75a28db5f1ca46c43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429258"
---
# <a name="multiple-active-statements-and-connections"></a>Várias instruções e conexões ativas
Alguns drivers e DBMSs limitam o número de instruções e conexões que podem estar ativas ao mesmo tempo. Esses números podem ser tão pequenos quanto um. Para obter mais informações, consulte as opções SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS na descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md) e [identificadores de conexão](../../../odbc/reference/develop-app/connection-handles.md).
