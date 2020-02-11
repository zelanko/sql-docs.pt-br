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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 646d2724489140080a673f31e22429cc7ca39d4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022106"
---
# <a name="value-list-arguments"></a>Argumentos da lista de valor
Um argumento de lista de valores consiste em uma lista de valores separados por vírgulas a serem usados para correspondência. Há apenas um argumento de lista de valores nas funções de catálogo do ODBC: o argumento *TableName* em **SQLTables**. Definir *tabletype* como um ponteiro nulo é o mesmo que se estiver definido como SQL_ALL_TABLE_TYPES, que enumera todos os membros possíveis da lista de valores. Esse argumento não é afetado pelo atributo de instrução SQL_ATTR_METADATA_ID. Para obter mais informações, consulte a descrição da função [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) .
