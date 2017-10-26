---
title: "Registro de cabeçalho | Microsoft Docs"
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
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0e4b73bf94c2d90f34c1d06240cbcceb07702c7a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="header-record"></a>Registro de cabeçalho
Os campos no registro de cabeçalho contêm informações gerais sobre a execução de uma função, incluindo o código de retorno, contagem de linhas, número de registros de status e o tipo da instrução executada. O registro de cabeçalho sempre é criado, a menos que a função retorne SQL_INVALID_HANDLE. Para obter uma lista completa dos campos no registro de cabeçalho, consulte o [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrição da função.

