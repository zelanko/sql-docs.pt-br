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
ms.openlocfilehash: 92fb7b0e9722c52c7f1e9fc071d434f531b2fc46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721904"
---
# <a name="update-delete-and-insert-statements"></a>Instruções UPDATE, DELETE e INSERT
Aplicativos baseados em SQL fazer alterações em tabelas, executando o **atualização**, **excluir**, e **inserir** instruções. Essas instruções fazem parte do nível de conformidade de gramática SQL mínima e devem ser suportadas por todos os drivers e fontes de dados.  
  
 É a sintaxe dessas instruções:  
  
 **UPDATE**  *table-name*  
  
 **SET** *column-identifier* **=** {*expression* &#124; **NULL**}  
  
 [**,** *identificador de coluna* **=** {*expressão* &#124; **nulo**}]...  
  
 [**Onde** *critério de pesquisa*]  
  
 **DELETE FROM** *nome da tabela*[**onde** *critério de pesquisa*]  
  
 **INSERT INTO** *nome da tabela*[**(* * * identificador da coluna* [* *,** *identificador de coluna*]... **)**]  
  
 {*especificação de consulta* &#124;  **valores (* * * Inserir valor* [* *,** *Inserir valor*]... **)**}  
  
 Observe que o *especificação de consulta* elemento só é válido nas gramáticas do Core e SQL estendida e que o *expressão* e *critério de pesquisa* elementos se tornem mais complexo nas gramáticas do Core e SQL estendida.  
  
 Como outras instruções SQL, **atualização**, **excluir**, e **inserir** instruções são geralmente mais eficiente quando eles usam parâmetros. Por exemplo, a instrução a seguir pode preparada e executada repetidamente para inserir várias linhas na tabela Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Essa eficiência pode ser aumentada, passando matrizes de valores de parâmetro. Para obter mais informações sobre parâmetros de instrução e matrizes de valores de parâmetro, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).
