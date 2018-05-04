---
title: Lista de argumentos de valor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14c78f543f959e091e52db6881d49e4221667273
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="value-list-arguments"></a>Argumentos de lista
Um argumento de lista do valor consiste em uma lista de valores separados por vírgulas a ser usado para correspondência. Há argumento apenas um valor da lista nas funções de catálogo ODBC: o *TableType* argumento **SQLTables**. Configuração *TableType* para um ponteiro nulo é o mesmo que ele é definido como SQL_ALL_TABLE_TYPES, que enumera todos os membros possíveis da lista de valores. Esse argumento não é afetado pelo atributo de instrução SQL_ATTR_METADATA_ID. Para obter mais informações, consulte o [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) descrição da função.
