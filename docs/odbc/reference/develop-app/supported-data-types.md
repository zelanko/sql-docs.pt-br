---
title: Tipos de dados com suporte | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5ec0f3943fd52540f094a23e9b3f9f3886e1371
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114078"
---
# <a name="supported-data-types"></a>Tipos de dados com suporte
Os tipos de dados com suporte pelos DBMSs variarem consideravelmente. Um aplicativo pode determinar os nomes e as características dos tipos de dados com suporte, chamando **SQLGetTypeInfo**. Devido a uma ampla variação nos nomes de tipo de dados, o aplicativo deve usar os nomes de tipo de dados retornados por **SQLGetTypeInfo** na **CREATE TABLE** instruções. Para obter mais informações, consulte [tipos de dados em ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
