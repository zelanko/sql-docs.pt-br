---
title: Tipos de dados suportados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d19cde2d531819a60229dd7a780181571e169503
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307776"
---
# <a name="supported-data-types"></a>Tipos de dados com suporte
Os tipos de dados suportados pelos DBMSs variam consideravelmente. Um aplicativo pode determinar os nomes e características dos tipos de dados suportados ligando para **SQLGetTypeInfo**. Devido à grande variação nos nomes de tipos de dados, o aplicativo deve usar os nomes de tipo de dados retornados pelo **SQLGetTypeInfo** nas instruções **CREATE TABLE.** Para obter mais informações, consulte [Tipos de dados no ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
