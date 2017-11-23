---
title: "Catálogo e o uso de esquema | Microsoft Docs"
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a7f0b16d97d5c82d113ac14c0cc6f84f48d004b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="catalog-and-schema-usage"></a>Catálogo e o uso do esquema
Fontes de dados não necessariamente dão suporte a nomes de catálogo e esquema como identificadores de nome de objeto em todas as instruções SQL. Fontes de dados podem dar suporte a nomes de catálogo e o esquema em uma ou mais das seguintes classes de instruções SQL: instruções de linguagem de manipulação de dados (DML), chamadas de procedimento, instruções de definição de tabela, instruções de definição de índice e definição de privilégio instruções. Para determinar as classes de instruções SQL em qual catálogo e o esquema de nomes podem ser usados, um aplicativo chama **SQLGetInfo** com as opções SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
