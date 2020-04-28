---
title: Argumentos da lista de valores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd655bd745c3bb06923e047d4134b286cf64703e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306737"
---
# <a name="value-list-arguments"></a>Argumentos da lista de valor
Um argumento de lista de valores consiste em uma lista de valores separados por vírgulas a serem usados para correspondência. Há apenas um argumento de lista de valores nas funções de catálogo do ODBC: o argumento *TableName* em **SQLTables**. Definir *tabletype* como um ponteiro nulo é o mesmo que se estiver definido como SQL_ALL_TABLE_TYPES, que enumera todos os membros possíveis da lista de valores. Esse argumento não é afetado pelo atributo de instrução SQL_ATTR_METADATA_ID. Para obter mais informações, consulte a descrição da função [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) .
