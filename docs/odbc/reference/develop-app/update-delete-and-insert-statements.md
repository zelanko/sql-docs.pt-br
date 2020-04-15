---
title: ATUALIZAR, EXCLUIR E INSERIR Declarações | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f12682a5d012d6981afce0085e9c920ed2f2ffbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284256"
---
# <a name="update-delete-and-insert-statements"></a>Instruções UPDATE, DELETE e INSERT
Os aplicativos baseados em SQL fazem alterações nas tabelas executando as instruções **UPDATE,** **DELETE**e **INSERT.** Essas declarações fazem parte do nível mínimo de conformidade gramatical SQL e devem ser suportadas por todos os drivers e fontes de dados.  
  
 A sintaxe dessas declarações é:  
  
 **ATUALIZAR** _nome da tabela_  
  
 **Identificador** _column-identifier_ **=** de coluna SET {*expressão* &#124; **NULL**}  
  
 [**,** _foto-identificador_ **=** de coluna {*expressão* &#124; **NULL**}]...  
  
 [**ONDE** _condição de pesquisa_]  
  
 **EXCLUA do** _nome da tabela_**[ONDE** _a condição de pesquisa]_  
  
 **INSIRA NO** _nome da tabela_[**(** _identificador de coluna_ [**,** _identificador de coluna_]... **)**]  
  
 {*especificação de consulta* &#124; **VALORES** _(insert-value_ **[,** _insert-value_]... **)**}  
  
 Observe que o elemento *de especificação de consulta* é válido apenas nas gramáticas SQL Core e Extended, e que os elementos de *expressão* e condição *de pesquisa* se tornam mais complexos nas gramáticas Core e Extended SQL.  
  
 Como outras instruções SQL, AS instruções **UPDATE,** **DELETE**e **INSERT** são muitas vezes mais eficientes quando usam parâmetros. Por exemplo, a seguinte instrução pode ser preparada e executada repetidamente para inserir várias linhas na tabela Ordens:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Essa eficiência pode ser aumentada passando matrizes de valores de parâmetros. Para obter mais informações sobre parâmetros de declaração e matrizes de valores de parâmetros, consulte [Parâmetros de declaração](../../../odbc/reference/develop-app/statement-parameters.md).
