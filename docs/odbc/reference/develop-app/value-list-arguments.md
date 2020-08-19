---
description: Argumentos da lista de valor
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
ms.openlocfilehash: fd2f2e970ea94635cda0b43b741abfda1130645b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421410"
---
# <a name="value-list-arguments"></a>Argumentos da lista de valor
Um argumento de lista de valores consiste em uma lista de valores separados por vírgulas a serem usados para correspondência. Há apenas um argumento de lista de valores nas funções de catálogo do ODBC: o argumento *TableName* em **SQLTables**. Definir *tabletype* como um ponteiro nulo é o mesmo que se estiver definido como SQL_ALL_TABLE_TYPES, que enumera todos os membros possíveis da lista de valores. Esse argumento não é afetado pelo atributo de instrução SQL_ATTR_METADATA_ID. Para obter mais informações, consulte a descrição da função [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) .
