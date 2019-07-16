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
ms.openlocfilehash: c2a2787be1bf44e1f214d396444a73b938acf7ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942834"
---
# <a name="update-delete-and-insert-statements"></a>Instruções UPDATE, DELETE e INSERT
Aplicativos baseados em SQL fazer alterações em tabelas, executando o **atualização**, **excluir**, e **inserir** instruções. Essas instruções fazem parte do nível de conformidade de gramática SQL mínima e devem ser suportadas por todos os drivers e fontes de dados.  
  
 É a sintaxe dessas instruções:  
  
 **UPDATE** _table-name_  
  
 **SET** _column-identifier_ **=** {*expression* &#124; **NULL**}  
  
 [ **,** _identificador de coluna_ **=** {*expressão* &#124; **nulo**}]...  
  
 [**WHERE** _search-condition_]  
  
 **DELETE FROM** _nome da tabela_[**onde** _critério de pesquisa_]  
  
 **INSERT INTO** _nome da tabela_[ **(** _identificador de coluna_ [ **,** _deidentificadordecoluna_]... **)** ]  
  
 {*especificação de consulta* &#124; **valores (** _Inserir valor_ [ **,** _Inserir valor_]... **)** }  
  
 Observe que o *especificação de consulta* elemento só é válido nas gramáticas do Core e SQL estendida e que o *expressão* e *critério de pesquisa* elementos se tornem mais complexo nas gramáticas do Core e SQL estendida.  
  
 Como outras instruções SQL, **atualização**, **excluir**, e **inserir** instruções são geralmente mais eficiente quando eles usam parâmetros. Por exemplo, a instrução a seguir pode preparada e executada repetidamente para inserir várias linhas na tabela Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Essa eficiência pode ser aumentada, passando matrizes de valores de parâmetro. Para obter mais informações sobre parâmetros de instrução e matrizes de valores de parâmetro, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).
