---
title: Tipos de dados com suporte | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ef33aa4d21c322c0fce0a77799261a62f546f08
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="supported-data-types"></a>Tipos de dados com suporte
Os tipos de dados suportados pelo DBMSs variam consideravelmente. Um aplicativo pode determinar os nomes e as características dos tipos de dados com suporte chamando **SQLGetTypeInfo**. Devido à grande variação em nomes de tipo de dados, o aplicativo deve usar os nomes de tipo de dados retornados por **SQLGetTypeInfo** na **CREATE TABLE** instruções. Para obter mais informações, consulte [tipos de dados ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
