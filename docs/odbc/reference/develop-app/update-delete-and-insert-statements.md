---
title: Instruções UPDATE, DELETE e INSERT | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942834"
---
# <a name="update-delete-and-insert-statements"></a>Instruções UPDATE, DELETE e INSERT
Os aplicativos baseados em SQL fazem alterações nas tabelas executando as instruções **Update**, **delete**e **Insert** . Essas instruções fazem parte do nível mínimo de conformidade da gramática do SQL e devem ter suporte de todos os drivers e fontes de dados.  
  
 A sintaxe dessas instruções é:  
  
 **Atualizar** _tabela-nome_  
  
 **Definir** _coluna-identificador_ **=** {*expressão* &#124; **NULL**}  
  
 [**,** **=** o _identificador de coluna_ {*expression* &#124; **NULL**}]...  
  
 [**Onde** _condição de pesquisa_]  
  
 **Excluir do** _table-name_[**em que** _Search-Condition_]  
  
 **Inserir em** _table-name_[**(** _coluna-identificador_ [**,** _coluna-identificador_]... **)**]  
  
 {a*especificação de consulta* &#124; **valores (** _Inserir-valor_ [**,** _Inserir valor_]... **)**}  
  
 Observe que o elemento de *especificação de consulta* é válido somente nas gramáticas de núcleo e SQL estendidas e que os elementos de *expressão* e de *condição de pesquisa* se tornam mais complexos no núcleo e nas gramáticas de SQL estendidas.  
  
 Como outras instruções SQL, as instruções **Update**, **delete**e **Insert** são geralmente mais eficientes quando usam parâmetros. Por exemplo, a instrução a seguir pode ser preparada e executada repetidamente para inserir várias linhas na tabela Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Essa eficiência pode ser aumentada passando-se matrizes de valores de parâmetro. Para obter mais informações sobre parâmetros de instrução e matrizes de valores de parâmetro, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).
