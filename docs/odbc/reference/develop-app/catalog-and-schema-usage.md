---
title: Uso de Catálogo e Esquema | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 245bd007f070a94689283830ba7a1362e31353e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306247"
---
# <a name="catalog-and-schema-usage"></a>Catálogo e o uso do esquema
As fontes de dados não suportam necessariamente nomes de catálogo e esquemas como identificadores de nomes de objeto em todas as instruções SQL. As fontes de dados podem suportar nomes de catálogo e esquema em uma ou mais das seguintes classes de declarações SQL: Declarações de Linguagem de Manipulação de Dados (DML), chamadas de procedimento, declarações de definição de tabela, declarações de definição de índice e declarações de definição de privilégio. Para determinar as classes de instruções SQL nas quais nomes de catálogo e esquema podem ser usados, um aplicativo chama **SQLGetInfo** com as opções SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
