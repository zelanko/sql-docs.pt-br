---
title: Várias instruções ativas e conexões | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccd501bb5ed41d1b8a841fd8e49a236fde69c586
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="multiple-active-statements-and-connections"></a>Várias instruções ativas e conexões
Alguns drivers e DBMSs limitam o número de conexões que podem estar ativas simultaneamente e instruções. Esses números podem ser tão pequenos quanto uma. Para obter mais informações, consulte as opções SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição, da função e [instrução trata](../../../odbc/reference/develop-app/statement-handles.md) e [ Identificadores de Conexão](../../../odbc/reference/develop-app/connection-handles.md).
