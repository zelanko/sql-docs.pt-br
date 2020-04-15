---
title: Múltiplas declarações e conexões ativas | Microsoft Docs
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
ms.openlocfilehash: 8259967942f47b06c50a9043158f8b3b45c58d7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302425"
---
# <a name="multiple-active-statements-and-connections"></a>Várias instruções e conexões ativas
Alguns drivers e DBMSs limitam o número de declarações e conexões que podem estar ativas ao mesmo tempo. Esses números podem ser tão pequenos quanto um. Para obter mais informações, consulte as opções de SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS na descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [alças de declaração](../../../odbc/reference/develop-app/statement-handles.md) e [alças de conexão](../../../odbc/reference/develop-app/connection-handles.md).
