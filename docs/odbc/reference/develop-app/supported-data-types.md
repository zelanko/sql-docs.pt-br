---
title: Tipos de dados com suporte | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b11c3df36ba36153f71721d9a10dee702ef745d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supported-data-types"></a>Tipos de dados com suporte
Os tipos de dados suportados pelo DBMSs variam consideravelmente. Um aplicativo pode determinar os nomes e as características dos tipos de dados com suporte chamando **SQLGetTypeInfo**. Devido à grande variação em nomes de tipo de dados, o aplicativo deve usar os nomes de tipo de dados retornados por **SQLGetTypeInfo** na **CREATE TABLE** instruções. Para obter mais informações, consulte [tipos de dados ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
