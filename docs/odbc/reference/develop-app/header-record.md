---
title: Registro de cabeçalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372185966cc1644147feb2683177ae3a5b69e788
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300176"
---
# <a name="header-record"></a>Registro de cabeçalho
Os campos no registro de cabeçalho contêm informações gerais sobre a execução de uma função, incluindo o código de retorno, a contagem de linhas, o número de registros de status e o tipo de declaração executada. O registro de cabeçalho é sempre criado a menos que a função retorne SQL_INVALID_HANDLE. Para obter uma lista completa de campos no registro de cabeçalho, consulte a descrição da função [SQLGetDiagField.](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)
