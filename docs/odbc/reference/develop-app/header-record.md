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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7b6ffacb618dd2b7714be59814f3f1a88a52228
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813914"
---
# <a name="header-record"></a>Registro de cabeçalho
Os campos no registro de cabeçalho contêm informações gerais sobre a execução de uma função, incluindo o código de retorno, contagem de linhas, o número de registros de status e tipo de instrução executada. O registro de cabeçalho sempre é criado, a menos que a função retorne SQL_INVALID_HANDLE. Para obter uma lista completa dos campos no registro de cabeçalho, consulte o [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrição da função.
