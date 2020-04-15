---
title: Trace DLL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e1f9dc57415ad9865ca1b2ad02487b62a93f18f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298066"
---
# <a name="trace-dll"></a>DLL de rastreamento
A DLL que realiza o rastreamento é um dos componentes principais do ODBC. O DLL de rastreamento é atualmente fornecido como uma dLL de amostra no componente ODBC do Windows SDK, e foi anteriormente incluído o Microsoft Data Access Components (MDAC) SDK. Portanto, a entrada de registro, interface e código de amostra para o DLL de rastreamento estão disponíveis. Esta DLL pode ser substituída por um DLL de rastreamento produzido por um usuário ODBC ou por um fornecedor de terceiros. Um DLL de rastreamento personalizado deve receber um nome diferente do dLL de amostra original. Os DLLs de rastreamento devem ser instalados no diretório do sistema ou não serão carregados. As strings de conexão não serão passadas para o dLL de rastreamento pelo Gerenciador de Driver.  
  
 O trace DLL rastreia argumentos de entrada, argumentos de saída, argumentos diferidos, códigos de devolução e SQLSTATEs. Quando o rastreamento é ativado, o Driver Manager chama o DLL de rastreamento em dois pontos: uma vez após a entrada da função (antes da validação do argumento) e novamente pouco antes do retorno da função.  
  
 Quando um aplicativo chama uma função, o Driver Manager chama uma função de rastreamento no DLL de rastreamento antes de chamar a função no driver ou processar a chamada em si. Cada função ODBC tem uma função de rastreamento correspondente (prefixada com *Trace*) que é idêntica à função ODBC, com exceção do nome. Quando a função de rastreamento é chamada, o DLL de rastreamento captura os argumentos de entrada e retorna um código de retorno. Como o DLL de rastreamento é chamado antes que o Driver Manager valide argumentos, as chamadas de função inválidas são rastreadas, para que erros de transição de estado e argumentos inválidos sejam registrados.  
  
 Depois de chamar a função de rastreamento no DLL de rastreamento, o Driver Manager chama a função ODBC no driver. Em seguida, ele chama **TraceReturn** no trace DLL. Esta função leva a dois argumentos: o valor devolvido pelo DLL de rastreamento para a função trace e o código de retorno devolvido pelo driver ao Driver Manager para a função ODBC (ou o valor devolvido pelo próprio Driver Manager se ele processou a função). A função usa o valor retornado para a função trace para manipular os valores de argumento de entrada capturados. Ele grava o código retornado para a função ODBC para o arquivo de log (ou exibe-o dinamicamente, se isso estiver ativado). Ele defaz referência susta os ponteiros do argumento de saída e registra os valores do argumento de saída.
