---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76b74ff748a62a401955e4ea4a995f507314124e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942823"
---
# <a name="multiple-active-statements-and-connections"></a>Várias instruções e conexões ativas
Alguns drivers e DBMSs limitam o número de instruções e conexões que podem estar ativas ao mesmo tempo. Esses números podem ser tão pequenos quanto um. Para obter mais informações, consulte as opções SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS na descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md) e [identificadores de conexão](../../../odbc/reference/develop-app/connection-handles.md).
