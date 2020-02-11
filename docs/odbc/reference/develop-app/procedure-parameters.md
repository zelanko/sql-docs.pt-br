---
title: Parâmetros do procedimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f85512a1686df26cad739dc906e49cc5499f62e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912299"
---
# <a name="procedure-parameters"></a>Parâmetros de procedimento
Parâmetros em chamadas de procedimento podem ser parâmetros de entrada, entrada/saída ou saída. Isso é diferente dos parâmetros em todas as outras instruções SQL, que são sempre parâmetros de entrada.  
  
 Os parâmetros de entrada são usados para enviar valores para o procedimento. Por exemplo, suponha que a tabela de partes tenha as colunas partid, descrição e preço. O procedimento InsertPart pode ter um parâmetro de entrada para cada coluna na tabela. Por exemplo:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Um driver não deve modificar o conteúdo de um buffer de entrada até **SQLExecDirect** ou **SQLExecute** retornar SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_NO_DATA. O conteúdo do buffer de entrada não deve ser modificado enquanto **SQLExecDirect** ou **SQLExecute** retorna SQL_NEED_DATA ou SQL_STILL_EXECUTING.  
  
 Os parâmetros de entrada/saída são usados para enviar valores para procedimentos e recuperar valores de procedimentos. Usar o mesmo parâmetro como uma entrada e um parâmetro de saída tende a ser confuso e deve ser evitado. Por exemplo, suponha que um procedimento aceite uma ID de pedido e retorne a ID do cliente. Isso pode ser definido com um único parâmetro de entrada/saída:  
  
```  
{call GetCustID(?)}  
```  
  
 Pode ser melhor usar dois parâmetros: um parâmetro de entrada para a ID do pedido e um parâmetro de saída ou entrada/saída para a ID do cliente:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Os parâmetros de saída são usados para recuperar o valor de retorno do procedimento e para recuperar valores de argumentos de procedimento; os procedimentos que retornam valores às vezes são conhecidos como *funções*. Por exemplo, suponha que o procedimento **Getcustid** que acabamos de mencionar retorna um valor que indica se foi capaz de encontrar o pedido. Na chamada a seguir, o primeiro parâmetro é um parâmetro de saída usado para recuperar o valor de retorno do procedimento, o segundo parâmetro é um parâmetro de entrada usado para especificar a ID do pedido, e o terceiro parâmetro é um parâmetro de saída usado para recuperar a ID do cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 Os drivers manipulam valores de entrada e parâmetros de entrada/saída em procedimentos diferentes dos parâmetros de entrada em outras instruções SQL. Quando a instrução é executada, elas recuperam os valores das variáveis associadas a esses parâmetros e as enviam para a fonte de dados.  
  
 Após a execução da instrução, os drivers armazenam os valores retornados dos parâmetros de entrada/saída e saída nas variáveis associadas a esses parâmetros. Esses valores retornados não têm garantia de serem definidos até que todos os resultados retornados pelo procedimento tenham sido buscados e **SQLMoreResults** tenha retornado SQL_NO_DATA. Se a execução da instrução resultar em um erro, o conteúdo do buffer do parâmetro de entrada/saída ou do buffer de parâmetros de saída será indefinido.  
  
 Um aplicativo chama **SqlProcedure** para determinar se um procedimento tem um valor de retorno. Ele chama **SQLProcedureColumns** para determinar o tipo (valor de retorno, entrada, entrada/saída ou saída) de cada parâmetro de procedimento.
