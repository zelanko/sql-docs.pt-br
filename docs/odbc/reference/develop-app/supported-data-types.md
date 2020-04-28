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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d19cde2d531819a60229dd7a780181571e169503
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307776"
---
# <a name="supported-data-types"></a>Tipos de dados com suporte
Os tipos de dados com suporte de DBMSs variam consideravelmente. Um aplicativo pode determinar os nomes e as características dos tipos de dados com suporte chamando **SQLGetTypeInfo**. Devido à grande variação em nomes de tipos de dados, o aplicativo deve usar os nomes de tipo de dados retornados por **SQLGetTypeInfo** em instruções **CREATE TABLE** . Para obter mais informações, consulte [tipos de dados em ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
