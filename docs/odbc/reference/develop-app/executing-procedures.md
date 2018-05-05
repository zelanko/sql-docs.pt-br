---
title: Executando procedimentos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3eb4c4106eebe3fc63207f7029518df6afc457f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executing-procedures"></a>Executando procedimentos
ODBC define uma sequência de escape padrão para a execução de procedimentos. Para obter a sintaxe dessa sequência e um exemplo de código que usa, consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Para executar um procedimento, um aplicativo executa as seguintes ações:  
  
1.  Define os valores de quaisquer parâmetros. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
2.  Chamadas **SQLExecDirect** e passa uma cadeia de caracteres que contém a instrução SQL que executa o procedimento. Essa instrução pode usar a sequência de escape definida pela sintaxe ODBC ou específicos de DBMS; instruções que usam a sintaxe específica de DBMS não são interoperáveis.  
  
3.  Quando **SQLExecDirect** é chamado, o driver:  
  
    -   Recupera os valores de parâmetro atuais e converte-os conforme necessário. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
    -   Chama o procedimento na fonte de dados e envia os valores de parâmetro convertido. Como o driver chama o procedimento é específico do driver. Por exemplo, ele pode modificar a instrução SQL para usar a gramática SQL da fonte de dados e enviar essa instrução para execução ou ele pode chamar o procedimento diretamente, usando um mecanismo de chamada de procedimento remoto (RPC) que é definido no protocolo de fluxo de dados do DBMS.  
  
    -   Retorna os valores dos parâmetros de saída ou qualquer entrada/saída ou o valor de retorno do procedimento, supondo que o procedimento for bem-sucedido. Esses valores podem não estar disponíveis até após o processamento de todos os outros resultados (conjuntos de resultados e contagens de linhas) gerados pelo procedimento. Se o procedimento falhar, o driver retorna erros.
