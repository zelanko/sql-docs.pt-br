---
title: Lista de argumentos de valor | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a971da68a8f2a35df8fa513e68d1eba127e9c430
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695704"
---
# <a name="value-list-arguments"></a>Argumentos da lista de valor
Um argumento de valor de lista consiste em uma lista de valores separados por vírgulas a ser usado para correspondência. Há o argumento da lista de apenas um valor em funções de catálogo ODBC: a *TableType* argumento **SQLTables**. Definindo *TableType* como um ponteiro nulo é o mesmo como se ele é definido como SQL_ALL_TABLE_TYPES, que enumera todos os membros possíveis da lista de valores. Esse argumento não é afetado pelo atributo de instrução SQL_ATTR_METADATA_ID. Para obter mais informações, consulte o [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) descrição da função.
