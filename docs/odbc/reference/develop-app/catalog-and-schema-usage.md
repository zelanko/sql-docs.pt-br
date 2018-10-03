---
title: Uso do esquema e catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9476f4f928890514354f97ce604f871bd8a06d11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702824"
---
# <a name="catalog-and-schema-usage"></a>Catálogo e o uso do esquema
Fontes de dados não suportam necessariamente nomes de catálogo e o esquema como identificadores de nome de objeto em todas as instruções SQL. Fontes de dados podem dar suporte a nomes de catálogo e esquema em uma ou mais das seguintes classes de instruções SQL: instruções de linguagem de manipulação de dados (DML), chamadas de procedimento, instruções de definição de tabela, as instruções de definição de índice e definição de privilégio instruções. Para determinar as classes de instruções SQL em qual catálogo e esquema de nomes podem ser usados, um aplicativo chama **SQLGetInfo** com as opções SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
