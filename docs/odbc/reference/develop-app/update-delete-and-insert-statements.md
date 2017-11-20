---
title: "Instruções INSERT, DELETE e UPDATE | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b150288c113b1aebf92abedbd6f7eabd0b4b7d24
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="update-delete-and-insert-statements"></a>Instruções INSERT, DELETE e UPDATE
Aplicativos baseados em SQL fazem alterações em tabelas, executando o **atualização**, **excluir**, e **inserir** instruções. Essas instruções são parte do nível de conformidade de gramática SQL mínima e devem ser suportadas por todos os drivers e fontes de dados.  
  
 A sintaxe das instruções a seguir é:  
  
 **ATUALIZAÇÃO***nome de tabela*   
  
 **DEFINIR** *identificador de coluna*  **=**  {*expressão* &#124; **Nulo**}  
  
 [**,** *identificador de coluna*  **=**  {*expressão* &#124; **Nulo**}]...  
  
 [**Onde** *critério de pesquisa*]  
  
 **DELETE FROM** *nome de tabela*[**onde** *critério de pesquisa*]  
  
 **INSERT INTO** *nome de tabela*[**(***identificador de coluna* [**,** *deidentificadordecoluna*] ... **)**]  
  
 {*especificação de consulta* &#124; **Valores (***Inserir valor* [**,** *Inserir valor*]... **)**}  
  
 Observe que o *especificação de consulta* elemento só é válido em gramáticas Core e SQL estendida e que o *expressão* e *critério de pesquisa* elementos se tornem mais complexo em gramáticas Core e estendida do SQL.  
  
 Como outras instruções SQL, **atualização**, **excluir**, e **inserir** instruções são geralmente mais eficientes quando o uso de parâmetros. Por exemplo, a instrução a seguir pode preparada e executada repetidamente para inserir várias linhas na tabela:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Para obter essa eficiência pode ser aumentada passando matrizes de valores de parâmetro. Para obter mais informações sobre os parâmetros de instrução e matrizes de valores de parâmetro, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).

