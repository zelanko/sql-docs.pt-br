---
title: Várias instruções ativas e conexões | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b2a1edbf9947aff01ef6d4688959352986cf672d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745714"
---
# <a name="multiple-active-statements-and-connections"></a>Várias instruções e conexões ativas
Alguns drivers e DBMSs limitam o número de instruções e conexões que podem estar ativas simultaneamente. Esses números podem ser tão pequenos quanto um. Para obter mais informações, consulte as opções SQL_MAX_CONCURRENT_ACTIVITIES e SQL_MAX_DRIVER_CONNECTIONS na [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição, da função e [instrução trata](../../../odbc/reference/develop-app/statement-handles.md) e [ Identificadores de Conexão](../../../odbc/reference/develop-app/connection-handles.md).
