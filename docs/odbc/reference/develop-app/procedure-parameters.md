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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35d43ca7cf6e603d7dabca9eacf1e026daa753b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306947"
---
# <a name="procedure-parameters"></a>Parâmetros de procedimento
Os parâmetros nas chamadas de procedimento podem ser parâmetros de entrada, entrada/saída ou de saída. Isso é diferente dos parâmetros em todas as outras instruções SQL, que são sempre parâmetros de entrada.  
  
 Parâmetros de entrada são usados para enviar valores para o procedimento. Por exemplo, suponha que a tabela Partes tenha colunas PartID, Descrição e Preço. O procedimento InsertPart pode ter um parâmetro de entrada para cada coluna na tabela. Por exemplo:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Um driver não deve modificar o conteúdo de um buffer de entrada até **que o SQLExecDirect** ou **o SQLExecute** retornem SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_NO_DATA. O conteúdo do buffer de entrada não deve ser modificado enquanto **o SQLExecDirect** ou **o SQLExecute** retornar SQL_NEED_DATA ou SQL_STILL_EXECUTING.  
  
 Parâmetros de entrada/saída são usados tanto para enviar valores aos procedimentos quanto para recuperar valores de procedimentos. Usar o mesmo parâmetro que uma entrada e um parâmetro de saída tende a ser confuso e deve ser evitado. Por exemplo, suponha que um procedimento aceite um ID de pedido e devolva o ID do cliente. Isso pode ser definido com um único parâmetro de entrada/saída:  
  
```  
{call GetCustID(?)}  
```  
  
 Pode ser melhor usar dois parâmetros: um parâmetro de entrada para o ID do pedido e um parâmetro de saída ou entrada/saída para o ID do cliente:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Os parâmetros de saída são usados para recuperar o valor de retorno do procedimento e para recuperar valores dos argumentos do procedimento; procedimentos que retornam valores são às vezes conhecidos como *funções*. Por exemplo, suponha que o procedimento **GetCustID** apenas mencionado retorna um valor que indica se ele foi capaz de encontrar o pedido. Na chamada a seguir, o primeiro parâmetro é um parâmetro de saída usado para recuperar o valor de retorno do procedimento, o segundo parâmetro é um parâmetro de entrada usado para especificar o ID da ordem e o terceiro parâmetro é um parâmetro de saída usado para recuperar o ID do cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 Os drivers manipulam valores para parâmetros de entrada e entrada/saída em procedimentos não diferentes dos parâmetros de entrada em outras instruções SQL. Quando a declaração é executada, eles recuperam os valores das variáveis vinculadas a esses parâmetros e os enviam para a fonte de dados.  
  
 Após a execução da declaração, os drivers armazenam os valores retornados dos parâmetros de entrada/saída e de saída nas variáveis vinculadas a esses parâmetros. Esses valores devolvidos não são garantidos a serem definidos até que todos os resultados devolvidos pelo procedimento tenham sido obtidos e **o SQLMoreResults** tenha retornado SQL_NO_DATA. Se a execução da declaração resultar em um erro, o conteúdo do buffer de parâmetro de entrada/saída ou do buffer de parâmetro de saída será indefinido.  
  
 Um aplicativo chama **SQLProcedure** para determinar se um procedimento tem um valor de retorno. Ele chama **SQLProcedureColumns** para determinar o tipo (valor de retorno, entrada, entrada/saída ou saída) de cada parâmetro de procedimento.
