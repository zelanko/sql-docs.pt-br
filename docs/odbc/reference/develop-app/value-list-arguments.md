---
title: Argumentos de lista de valor | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306737"
---
# <a name="value-list-arguments"></a>Argumentos da lista de valor
Um argumento de lista de valores consiste em uma lista de valores separados por comma a serem usados para correspondência. Há apenas um argumento de lista de valor nas funções do catálogo ODBC: o argumento *TableType* em **SQLTables**. Definir *TableType* para um ponteiro nulo é o mesmo que se ele estiver definido como SQL_ALL_TABLE_TYPES, o que enumera todos os membros possíveis da lista de valores. Este argumento não é afetado pelo atributo de declaração SQL_ATTR_METADATA_ID. Para obter mais informações, consulte a descrição da função [SQLTables.](../../../odbc/reference/syntax/sqltables-function.md)
