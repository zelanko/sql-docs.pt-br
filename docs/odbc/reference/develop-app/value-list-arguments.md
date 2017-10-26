---
title: Lista de argumentos de valor | Microsoft Docs
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a8386d5ffbb4d492bc8489272596fb9f6d58d245
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="value-list-arguments"></a>Argumentos de lista
Um argumento de lista do valor consiste em uma lista de valores separados por vírgulas a ser usado para correspondência. Há argumento apenas um valor da lista nas funções de catálogo ODBC: o *TableType* argumento **SQLTables**. Configuração *TableType* para um ponteiro nulo é o mesmo que ele é definido como SQL_ALL_TABLE_TYPES, que enumera todos os membros possíveis da lista de valores. Esse argumento não é afetado pelo atributo de instrução SQL_ATTR_METADATA_ID. Para obter mais informações, consulte o [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) descrição da função.

