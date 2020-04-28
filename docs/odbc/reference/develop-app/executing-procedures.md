---
title: Executando procedimentos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a796c615d7dfdec11a9acb90ab4b5129cf69717
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305707"
---
# <a name="executing-procedures"></a>Executar procedimentos
O ODBC define uma sequência de escape padrão para executar procedimentos. Para obter a sintaxe dessa sequência e um exemplo de código que a usa, consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Para executar um procedimento, um aplicativo executa as seguintes ações:  
  
1.  Define os valores de qualquer parâmetro. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
2.  Chama **SQLExecDirect** e passa uma cadeia de caracteres contendo a instrução SQL que executa o procedimento. Essa instrução pode usar a sequência de escape definida pela sintaxe específica de ODBC ou DBMS; as instruções que usam a sintaxe específica do DBMS não são interoperáveis.  
  
3.  Quando **SQLExecDirect** é chamado, o driver:  
  
    -   Recupera os valores de parâmetro atuais e os converte conforme necessário. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.  
  
    -   Chama o procedimento na fonte de dados e o envia os valores de parâmetro convertidos. Como o driver chama o procedimento é específico do driver. Por exemplo, ele pode modificar a instrução SQL para usar a gramática SQL da fonte de dados e enviar essa instrução para execução, ou pode chamar o procedimento diretamente usando um mecanismo de RPC (chamada de procedimento remoto) que é definido no protocolo de fluxo de dados do DBMS.  
  
    -   Retorna os valores de qualquer parâmetro de entrada/saída ou saída ou o valor de retorno do procedimento, supondo que o procedimento tenha sucesso. Esses valores podem não estar disponíveis até que todos os outros resultados (contagens de linhas e conjuntos de resultados) gerados pelo procedimento tenham sido processados. Se o procedimento falhar, o driver retornará erros.
