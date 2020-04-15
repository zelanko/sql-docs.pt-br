---
title: Chamadas de procedimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9c52e72512c8b81c6872461207f235ea2731ac5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282226"
---
# <a name="procedure-calls"></a>Chamadas de procedimento
Um *procedimento* é um objeto executável armazenado na fonte de dados. Em geral, é uma ou mais instruções SQL que foram pré-compiladas. A seqüência de fuga para chamar um procedimento é  
  
 **{****[ ?=**] nome *de procedimento de***chamada** [**[**[*parâmetro***][ [***parâmetro*]... **)**]**}**  
  
 onde *o nome do procedimento* especifica o nome de um procedimento e o *parâmetro* especifica um parâmetro do procedimento.  
  
 Para obter mais informações sobre o procedimento chamada seqüência de fuga, consulte [Procedure Call Escape Sequence](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) no apêndice C: Gramática SQL.  
  
 Um procedimento pode ter zero ou mais parâmetros. Ele também pode retornar um valor, como indicado pelo marcador de parâmetro opcional **?=** no início da sintaxe. Se *o parâmetro* for um parâmetro de entrada ou de entrada/saída, pode ser um marcador literal ou de parâmetro. No entanto, as aplicações interoperáveis devem sempre usar marcadores de parâmetros porque algumas fontes de dados não aceitam valores de parâmetros literais. Se *o parâmetro* é um parâmetro de saída, deve ser um marcador de parâmetro. Os marcadores de parâmetro devem ser vinculados ao **SQLBindParameter** antes que a declaração de chamada do procedimento seja executada.  
  
 Parâmetros de entrada e entrada/saída podem ser omitidos das chamadas de procedimento. Se um procedimento for chamado de parênteses, mas sem quaisquer parâmetros, como {call *procedure-name*()}), o driver instrui a fonte de dados a usar o valor padrão para o primeiro parâmetro. Se o procedimento não tiver parâmetros, isso pode fazer com que o procedimento falhe. Se um procedimento for chamado sem parênteses, como {call *procedure-name*}, o motorista não envia nenhum valor de parâmetro.  
  
 Literais podem ser especificados para parâmetros de entrada e de entrada/saída em chamadas de procedimento. Por exemplo, suponha que o procedimento **InsertOrder** tenha cinco parâmetros de entrada. A chamada a seguir para **InsertOrder** omite o primeiro parâmetro, fornece um literal para o segundo parâmetro e usa um marcador de parâmetro para o terceiro, quarto e quinto parâmetros:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 Observe que se um parâmetro for omitido, a comma que o delimita de outros parâmetros ainda deve aparecer. Se um parâmetro de entrada ou entrada/saída for omitido, o procedimento usará o valor padrão do parâmetro. Outra maneira de especificar o valor padrão de um parâmetro de entrada ou entrada/saída é definir o valor do buffer comprimento/indicador vinculado ao parâmetro para SQL_DEFAULT_PARAM.  
  
 Se um parâmetro de entrada/saída for omitido ou se um literal for fornecido para o parâmetro, o driver descartará o valor de saída. De forma semelhante, se o marcador de parâmetro para o valor de retorno de um procedimento for omitido, o driver descartará o valor de retorno. Finalmente, se um aplicativo especificar um parâmetro de valor de retorno para um procedimento que não retorna um valor, o driver definirá o valor do buffer de comprimento/indicador associado ao parâmetro como SQL_NULL_DATA.  
  
 Suponha que o procedimento PARTS_IN_ORDERS cria um conjunto de resultados que contém uma lista de ordens que contêm um número de peça específico. O código a seguir chama este procedimento para a parte número 544:  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 Para determinar se uma fonte de dados suporta procedimentos, um aplicativo chama **sqlGetInfo** com a opção SQL_PROCEDURES.  
  
 Para obter mais informações sobre procedimentos, consulte [Procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).
