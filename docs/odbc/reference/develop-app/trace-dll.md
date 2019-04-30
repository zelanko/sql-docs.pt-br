---
title: DLL de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7a99f6c2960600d62a789471f68c1f5da89ae8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63148865"
---
# <a name="trace-dll"></a>DLL de rastreamento
A DLL que executa o rastreamento é um dos principais componentes de ODBC. O rastreamento de DLL no momento é fornecido como um exemplo de DLL no componente de ODBC do SDK do Windows e foi incluído anteriormente Microsoft Data Access Components (MDAC) do SDK. Portanto, a entrada do registro, a interface e o código de exemplo para a DLL de rastreamento estão disponíveis. Essa DLL pode ser substituído por um rastreamento DLL produzido por um usuário ODBC ou um fornecedor de terceiros. Uma DLL de rastreamento personalizado deve ser fornecido um nome diferente a DLL de rastreamento de exemplo original. DLLs de rastreamento devem ser instalados no diretório do sistema, ou eles serão carregados. As cadeias de caracteres de conexão não serão passadas para a DLL de rastreamento pelo Gerenciador de Driver.  
  
 A DLL de rastreamento rastreia SQLSTATEs, argumentos de saída, argumentos adiados, códigos de retorno e argumentos de entrada. Quando o rastreamento está habilitado, o Gerenciador de Driver chama a DLL de rastreamento em dois pontos: uma vez após a entrada da função (antes da validação de argumento) e novamente apenas antes que a função retorna.  
  
 Quando um aplicativo chama uma função, o Gerenciador de Driver chama uma função de rastreamento no rastreamento DLL antes de chamar a função no driver ou a própria chamada de processamento. Cada função ODBC tem uma função de rastreamento correspondente (prefixados com *rastreamento*) que é idêntica à função de ODBC com o nome a exceção. Quando a função de rastreamento é chamada, a DLL de rastreamento captura os argumentos de entrada e retorna um código de retorno. Como a DLL de rastreamento é chamado antes do Gerenciador de Driver valida argumentos, chamadas de função inválido são rastreadas para que erros de transição de estado e argumentos inválidos são registrados.  
  
 Depois de chamar a função de rastreamento no rastreamento de DLL, o Gerenciador de Driver chama a função ODBC no driver. Em seguida, ele chama **TraceReturn** no rastreamento de DLL. Essa função usa dois argumentos: o valor retornado pelo DLL de rastreamento para a função de rastreamento e o código de retorno retornados pelo driver para o Gerenciador de Driver para a função ODBC (ou o valor retornado pelo Gerenciador de Driver em si se ele tiver processado a função). A função usa o valor retornado para a função de rastreamento para manipular valores de argumento de entrada capturada. Ele escreve o código retornado para a função ODBC para o arquivo de log (ou exibe dinamicamente, se habilitado). Ele desreferencia os ponteiros de argumento de saída e registra em log os valores de argumento de saída.
