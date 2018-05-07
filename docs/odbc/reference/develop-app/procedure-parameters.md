---
title: Parâmetros de procedimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc7e82b134ef578907dc0b5e84aa0e1ed7224027
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="procedure-parameters"></a>Parâmetros de procedimento
Parâmetros em chamadas de procedimento podem ser de entrada, entradam/saídam ou parâmetros de saída. Isso é diferente de parâmetros em todas as outras instruções de SQL, que sempre são parâmetros de entrada.  
  
 Parâmetros de entrada são usados para enviar valores para o procedimento. Por exemplo, suponha que a tabela de peças possui colunas de PartID, descrição e preço. O procedimento InsertPart pode ter um parâmetro de entrada para cada coluna na tabela. Por exemplo:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Um driver não deve modificar o conteúdo de um buffer de entrada até **SQLExecDirect** ou **SQLExecute** retorna SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_NO_DATA. O conteúdo do buffer de entrada não deve ser modificado enquanto **SQLExecDirect** ou **SQLExecute** retorna SQL_NEED_DATA ou SQL_STILL_EXECUTING.  
  
 Parâmetros de entrada/saída são usados para enviar valores para os procedimentos e recuperar valores de procedimentos. Usar o mesmo parâmetro como uma entrada e um parâmetro de saída tende a ser confusas e deve ser evitado. Por exemplo, suponha que um procedimento aceita uma ID de ordem e retorna a ID do cliente. Isso pode ser definido com um único parâmetro de entrada/saída:  
  
```  
{call GetCustID(?)}  
```  
  
 Talvez seja melhor usar dois parâmetros: um parâmetro de entrada para a ID da ordem e uma saída ou um parâmetro de entrada/saída para a ID do cliente:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Parâmetros de saída são usados para recuperar o valor de retorno do procedimento e para recuperar valores de argumentos de procedimento; os procedimentos que retornam valores também são conhecidos como *funções*. Por exemplo, suponha que o **GetCustID** procedimento mencionados acima retorna um valor que indica se ele foi capaz de localizar o pedido. Na chamada a seguir, o primeiro parâmetro é um parâmetro de saída usado para recuperar o valor de retorno do procedimento, o segundo parâmetro é um parâmetro de entrada usado para especificar a ID da ordem e o terceiro parâmetro é um parâmetro de saída usado para recuperar a ID do cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 Drivers de lidar com valores de entrada e entradam/saídam parâmetros em procedimentos não Diferentemente de parâmetros de entrada em outras instruções SQL. Quando a instrução é executada, ele recuperar os valores das variáveis associadas a esses parâmetros e enviá-los para a fonte de dados.  
  
 Depois que a instrução foi executada, drivers de armazenam os valores retornados de entrada/saída e os parâmetros de saída nas variáveis associadas a esses parâmetros. Esses retornados valores não há garantia de ser definida até depois que todos os resultados retornados pelo procedimento foram buscados e **SQLMoreResults** retornou SQL_NO_DATA. Se a execução da instrução resulta em um erro, o conteúdo do buffer de parâmetro de entrada/saída ou buffers de parâmetro de saída é indefinido.  
  
 Um aplicativo chama **SQLProcedure** para determinar se um procedimento tem um valor de retorno. Ele chama **SQLProcedureColumns** para determinar o tipo (valor de retorno, entrado, entrada/saída ou saído) de cada parâmetro de procedimento.
