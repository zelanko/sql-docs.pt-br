---
title: "Várias instruções ativas e conexões | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 97976df0d7f0a237abd2e67ed71202ba4d518f3b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="multiple-active-statements-and-connections"></a>Várias instruções ativas e conexões
Alguns drivers e DBMSs limitam o número de conexões que podem estar ativas simultaneamente e instruções. Esses números podem ser tão pequenos quanto uma. Para obter mais informações, consulte as opções SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição, da função e [instrução trata](../../../odbc/reference/develop-app/statement-handles.md) e [ Identificadores de Conexão](../../../odbc/reference/develop-app/connection-handles.md).

