---
title: "Instruções INSERT, DELETE e UPDATE | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 592d135ccf66f8a9fde2cc064a51dc25617cf127
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="update-delete-and-insert-statements"></a>Instruções INSERT, DELETE e UPDATE
Aplicativos baseados em SQL fazem alterações em tabelas, executando o **atualização**, **excluir**, e **inserir** instruções. Essas instruções são parte do nível de conformidade de gramática SQL mínima e devem ser suportadas por todos os drivers e fontes de dados.  
  
 A sintaxe das instruções a seguir é:  
  
 **UPDATE**  *table-name*  
  
 **SET** *column-identifier* **=** {*expression* &#124; **NULL**}  
  
 [**,** *column-identifier* **=** {*expression* &#124; **NULL**}]...  
  
 [**Onde** *critério de pesquisa*]  
  
 **DELETE FROM** *table-name*[**WHERE** *search-condition*]  
  
 **INSERT INTO** *nome de tabela*[**(* identificador da coluna* [* *,** *identificador de coluna*]... **)**]  
  
 {*query-specification* &#124; **VALUES (***insert-value* [**,** *insert-value*]...**)**}  
  
 Observe que o *especificação de consulta* elemento só é válido em gramáticas Core e SQL estendida e que o *expressão* e *critério de pesquisa* elementos se tornem mais complexo em gramáticas Core e estendida do SQL.  
  
 Como outras instruções SQL, **atualização**, **excluir**, e **inserir** instruções são geralmente mais eficientes quando o uso de parâmetros. Por exemplo, a instrução a seguir pode preparada e executada repetidamente para inserir várias linhas na tabela:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Para obter essa eficiência pode ser aumentada passando matrizes de valores de parâmetro. Para obter mais informações sobre os parâmetros de instrução e matrizes de valores de parâmetro, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).
