---
title: Chamadas de procedimento | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4ca9347cae8227885237882117ae3f486309093
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="procedure-calls"></a>Chamadas de procedimento
Um *procedimento* é um objeto executável armazenado na fonte de dados. Em geral, é uma ou mais instruções SQL que foram pré-compiladas. É a sequência de escape para chamar um procedimento  
  
 **{**[**? =**]**chamar** *nome do procedimento*[**(**[*parâmetro*] [**,**[*parâmetro*]]... **)**]**}**  
  
 onde *nome do procedimento* Especifica o nome de um procedimento e *parâmetro* Especifica um parâmetro de procedimento.  
  
 Para obter mais informações sobre a sequência de escape de chamada de procedimento, consulte [sequência de Escape Call do procedimento](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) na gramática do apêndice c: SQL.  
  
 Um procedimento pode ter zero ou mais parâmetros. Ele também pode retornar um valor, conforme indicado pelo marcador de parâmetro opcional **? =** no início da sintaxe. Se *parâmetro* é uma entrada ou um parâmetro de entrada/saída, ele pode ser um literal ou um marcador de parâmetro. No entanto, os aplicativos interoperáveis sempre devem usar marcadores de parâmetro porque algumas fontes de dados não aceita valores de parâmetro literal. Se *parâmetro* é um parâmetro de saída, ele deve ser um marcador de parâmetro. Marcadores de parâmetro devem ser associados com **SQLBindParameter** antes da chamada de procedimento instrução é executada.  
  
 Parâmetros de entrada e entrada/saída podem ser omitidos das chamadas de procedimento. Se um procedimento é chamado com parênteses, mas sem parâmetros, como {chamar *nome do procedimento*()}, o driver instruirá a fonte de dados para usar o valor padrão para o primeiro parâmetro. Se o procedimento não tem nenhum parâmetro, isso pode causar falha no procedimento. Se um procedimento for chamado sem parênteses, como {chamar *nome do procedimento*}, o driver não enviará nenhum valor de parâmetro.  
  
 Literais podem ser especificados para parâmetros de entrada e de entrada/saída em chamadas de procedimento. Por exemplo, suponha que o procedimento **InsertOrder** tem cinco parâmetros de entrada. A seguinte chamada para **InsertOrder** omite o primeiro parâmetro, fornece um literal para o segundo parâmetro e usa um marcador de parâmetro para o terceiro, quarto e quinto parâmetros:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 Observe que, se um parâmetro for omitido, a vírgula separa de outros parâmetros ainda deverá aparecer. Se um parâmetro de entrada ou entrada/saída for omitido, o procedimento usará o valor padrão do parâmetro. Outra maneira de especificar que o valor padrão de um parâmetro de entrada ou entrada/saída é definir o valor do buffer de comprimento/indicador associado ao parâmetro como SQL_DEFAULT_PARAM.  
  
 Se um parâmetro de entrada/saída for omitido ou se for fornecido um literal para o parâmetro, o driver descartará o valor de saída. De forma semelhante, se o marcador de parâmetro para o valor de retorno de um procedimento for omitido, o driver descartará o valor de retorno. Finalmente, se um aplicativo especificar um parâmetro de valor de retorno para um procedimento que não retorna um valor, o driver definirá o valor do buffer de comprimento/indicador associado ao parâmetro como SQL_NULL_DATA.  
  
 Suponha que o procedimento PARTS_IN_ORDERS cria um conjunto de resultados que contém uma lista de pedidos que contêm um número de peça específica. O código a seguir chama esse procedimento para o número de peça 544:  
  
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
  
 Para determinar se uma fonte de dados oferece suporte a procedimentos, um aplicativo chama **SQLGetInfo** com a opção SQL_PROCEDURES.  
  
 Para obter mais informações sobre procedimentos, consulte [procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).
