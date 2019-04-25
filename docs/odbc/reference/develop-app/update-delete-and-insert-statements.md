---
title: Instruções INSERT, DELETE e UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00732de7eca32dc8b2984fdda14163c77c66ad43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632474"
---
# <a name="update-delete-and-insert-statements"></a>Instruções UPDATE, DELETE e INSERT
Aplicativos baseados em SQL fazer alterações em tabelas, executando o **atualização**, **excluir**, e **inserir** instruções. Essas instruções fazem parte do nível de conformidade de gramática SQL mínima e devem ser suportadas por todos os drivers e fontes de dados.  
  
 É a sintaxe dessas instruções:  
  
 **UPDATE** _table-name_  
  
 **SET** _column-identifier_ **=** {*expression* &#124; **NULL**}  
  
 [**,** _identificador de coluna_ **=** {*expressão* &#124; **nulo**}]...  
  
 [**WHERE** _search-condition_]  
  
 **DELETE FROM** _table-name_[**WHERE** _search-condition_]  
  
 **INSERT INTO** _nome da tabela_[**(** _identificador de coluna_ [**,** _deidentificadordecoluna_]... **)**]  
  
 {*query-specification* &#124; **VALUES (** _insert-value_ [**,** _insert-value_]...**)**}  
  
 Observe que o *especificação de consulta* elemento só é válido nas gramáticas do Core e SQL estendida e que o *expressão* e *critério de pesquisa* elementos se tornem mais complexo nas gramáticas do Core e SQL estendida.  
  
 Como outras instruções SQL, **atualização**, **excluir**, e **inserir** instruções são geralmente mais eficiente quando eles usam parâmetros. Por exemplo, a instrução a seguir pode preparada e executada repetidamente para inserir várias linhas na tabela Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Essa eficiência pode ser aumentada, passando matrizes de valores de parâmetro. Para obter mais informações sobre parâmetros de instrução e matrizes de valores de parâmetro, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).
