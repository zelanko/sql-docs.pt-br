---
title: DLL de rastreamento | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b58f344839a0f8e74fa46c5e788b7835d3eadc2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="trace-dll"></a>DLL de rastreamento
A DLL que executa o rastreamento é um dos componentes centrais do ODBC. O rastreamento da DLL no momento é fornecido como um exemplo de DLL no componente de ODBC do SDK do Windows e foi incluído anteriormente Microsoft Data Access Components (MDAC) SDK. Portanto, a entrada do registro, a interface e o código de exemplo para a DLL de rastreamento estão disponíveis. Essa DLL pode ser substituída por um rastreamento de DLL produzido por um usuário ODBC ou um fornecedor de terceiros. Uma DLL de rastreamento personalizado deve ser fornecido um nome diferente a DLL de rastreamento de exemplo original. DLLs de rastreamento devem ser instalados no diretório do sistema ou não carregarão. As cadeias de caracteres de conexão não serão passadas para o rastreamento de DLL pelo Gerenciador de Driver.  
  
 A DLL de rastreamento rastreia SQLSTATEs, argumentos de saída, argumentos adiados, códigos de retorno e argumentos de entrada. Quando o rastreamento estiver habilitado, o Gerenciador de Driver chama o DLL de rastreamento em dois pontos: uma vez na entrada de função (antes da validação de argumento) e novamente apenas antes da função retorna.  
  
 Quando um aplicativo chama uma função, o Gerenciador de Driver chama uma função de rastreamento no rastreamento DLL antes de chamar a função no driver ou processar a chamada em si. Cada função ODBC tem uma função de rastreamento correspondente (prefixado com *rastreamento*) que é idêntica à função de ODBC com exceção do nome. Quando a função de rastreamento é chamada, a DLL de rastreamento captura os argumentos de entrada e retorna um código de retorno. Como a DLL de rastreamento é chamado antes do Gerenciador de Driver valida argumentos, chamadas de função inválido são rastreadas para que erros de transição de estado e argumentos inválidos são registrados.  
  
 Depois de chamar a função de rastreamento no rastreamento de DLL, o Gerenciador de Driver chama a função ODBC no driver. Depois, ele chama **TraceReturn** no rastreamento DLL. Essa função usa dois argumentos: o valor retornado pelo DLL de rastreamento para a função de rastreamento e o código de retorno retornados pelo driver para o Gerenciador de Driver para a função ODBC (ou o valor retornado pelo Gerenciador de Driver em si se processado a função). A função usa o valor retornado para a função de rastreamento para manipular valores de argumento de entrada capturada. Ele grava o código retornado para a função ODBC para o arquivo de log (ou exibe dinamicamente, se habilitado). Ele desreferências os ponteiros de argumento de saída e registra os valores de argumento de saída.
