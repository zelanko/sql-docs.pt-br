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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282226"
---
# <a name="procedure-calls"></a>Chamadas de procedimento
Um *procedimento* é um objeto executável armazenado na fonte de dados. Em geral, é uma ou mais instruções SQL que foram pré-compiladas. A sequência de escape para chamar um procedimento é  
  
 **{**[**? =**]**chamar** *procedimento-nome*[**(**[*parâmetro*] [**,**[*parâmetro*]]... **)**]**}**  
  
 em que *procedure-name* especifica o nome de um procedimento e um *parâmetro* especifica um parâmetro de procedimento.  
  
 Para obter mais informações sobre a sequência de escape de chamada de procedimento, consulte [sequência de escape de chamada de procedimento](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) no Apêndice C: gramática SQL.  
  
 Um procedimento pode ter zero ou mais parâmetros. Ele também pode retornar um valor, conforme indicado pelo marcador de parâmetro opcional **? =** no início da sintaxe. Se o *parâmetro* for uma entrada ou um parâmetro de entrada/saída, ele poderá ser um marcador literal ou de parâmetro. No entanto, os aplicativos interoperáveis sempre devem usar marcadores de parâmetro porque algumas fontes de dados não aceitam valores de parâmetro literais. Se o *parâmetro* for um parâmetro de saída, ele deverá ser um marcador de parâmetro. Os marcadores de parâmetro devem ser associados a **SQLBindParameter** antes que a instrução de chamada de procedimento seja executada.  
  
 Parâmetros de entrada e entrada/saída podem ser omitidos das chamadas de procedimento. Se um procedimento for chamado com parênteses, mas sem parâmetros, como {chamar *procedure-name*()}, o driver instruirá a fonte de dados a usar o valor padrão para o primeiro parâmetro. Se o procedimento não tiver nenhum parâmetro, isso poderá causar falha no procedimento. Se um procedimento for chamado sem parênteses, como {chamar *procedure-name*}, o driver não enviará nenhum valor de parâmetro.  
  
 Literais podem ser especificados para parâmetros de entrada e de entrada/saída em chamadas de procedimento. Por exemplo, suponha que o procedimento **InsertOrder** tenha cinco parâmetros de entrada. A chamada a seguir para **InsertOrder** omite o primeiro parâmetro, fornece um literal para o segundo parâmetro e usa um marcador de parâmetro para o terceiro, o quarto e o quinto parâmetros:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 Observe que, se um parâmetro for omitido, a vírgula que está delimitando-o de outros parâmetros ainda deverá aparecer. Se um parâmetro de entrada ou entrada/saída for omitido, o procedimento usará o valor padrão do parâmetro. Outra maneira de especificar o valor padrão de um parâmetro de entrada ou de entrada/saída é definir o valor do buffer de comprimento/indicador associado ao parâmetro para SQL_DEFAULT_PARAM.  
  
 Se um parâmetro de entrada/saída for omitido ou se um literal for fornecido para o parâmetro, o driver descartará o valor de saída. De forma semelhante, se o marcador de parâmetro para o valor de retorno de um procedimento for omitido, o driver descartará o valor de retorno. Finalmente, se um aplicativo especificar um parâmetro de valor de retorno para um procedimento que não retorna um valor, o driver definirá o valor do buffer de comprimento/indicador associado ao parâmetro como SQL_NULL_DATA.  
  
 Suponha que o procedimento PARTS_IN_ORDERS crie um conjunto de resultados que contenha uma lista de pedidos que contenham um número de peça específico. O código a seguir chama esse procedimento para o número de peça 544:  
  
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
  
 Para determinar se uma fonte de dados dá suporte a procedimentos, um aplicativo chama **SQLGetInfo** com a opção SQL_PROCEDURES.  
  
 Para obter mais informações sobre procedimentos, consulte [procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).
