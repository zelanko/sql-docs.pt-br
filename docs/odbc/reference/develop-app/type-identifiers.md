---
title: Identificadores de tipo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79aa4de5d722208195477f7ffef53cac6c61a2de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093017"
---
# <a name="type-identifiers"></a>Identificadores de tipo
Para descrever os tipos de dados SQL e C, o ODBC define dois conjuntos de *identificadores de tipo*. Um identificador de tipo descreve o tipo de uma coluna SQL ou um buffer C. É um valor **#define** e geralmente é passado como um argumento de função ou retornado em metadados.  
  
 Por exemplo, a chamada a seguir para **SQLBindParameter** associa uma variável do tipo SQL_DATE_STRUCT a um parâmetro date em uma instrução SQL. O identificador do tipo C SQL_C_TYPE_DATE especifica o tipo da variável de *Data* e o identificador do tipo SQL SQL_TYPE_DATE especifica o tipo do parâmetro dinâmico.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
