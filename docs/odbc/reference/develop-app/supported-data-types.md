---
title: Tipos de dados com suporte | Microsoft Docs
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
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d76b98635cdc183f08f205374f8e7e0e66a4cb5f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="supported-data-types"></a>Tipos de dados com suporte
Os tipos de dados suportados pelo DBMSs variam consideravelmente. Um aplicativo pode determinar os nomes e as características dos tipos de dados com suporte chamando **SQLGetTypeInfo**. Devido à grande variação em nomes de tipo de dados, o aplicativo deve usar os nomes de tipo de dados retornados por **SQLGetTypeInfo** na **CREATE TABLE** instruções. Para obter mais informações, consulte [tipos de dados ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).

