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
ms.openlocfilehash: 6fe910c93beac676e5fb0f663b740c03a826c326
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67985228"
---
# <a name="trace-dll"></a>DLL de rastreamento
A DLL que executa o rastreamento é um dos componentes do ODBC Core. No momento, a DLL de rastreamento é fornecida como uma DLL de exemplo no componente ODBC do SDK do Windows e, anteriormente, incluiu o SDK do MDAC (Microsoft Data Access Components). Portanto, a entrada do registro, a interface e o código de exemplo para a DLL de rastreamento estão disponíveis. Essa DLL pode ser substituída por uma DLL de rastreamento produzida por um usuário ODBC ou por um fornecedor de terceiros. Uma DLL de rastreamento personalizada deve receber um nome diferente da DLL de rastreamento de exemplo original. As DLLs de rastreamento devem ser instaladas no diretório do sistema ou não serão carregadas. As cadeias de conexão não serão passadas para a DLL de rastreamento pelo Gerenciador de driver.  
  
 A DLL de rastreamento rastreia argumentos de entrada, argumentos de saída, argumentos adiados, códigos de retorno e sqlstates. Quando o rastreamento está habilitado, o Gerenciador de driver chama a DLL de rastreamento em dois pontos: uma vez na entrada da função (antes da validação do argumento) e novamente antes da função retornar.  
  
 Quando um aplicativo chama uma função, o Gerenciador de driver chama uma função de rastreamento na DLL de rastreamento antes de chamar a função no driver ou processar a chamada em si. Cada função ODBC tem uma função de rastreamento correspondente (prefixada com *trace*) que é idêntica à função ODBC com a exceção do nome. Quando a função de rastreamento é chamada, a DLL de rastreamento captura os argumentos de entrada e retorna um código de retorno. Como a DLL de rastreamento é chamada antes de o Gerenciador de driver validar argumentos, as chamadas de função inválidas são rastreadas e, portanto, erros de transição de estado e argumentos inválidos são registrados.  
  
 Depois de chamar a função trace na DLL de rastreamento, o Gerenciador de driver chama a função ODBC no driver. Em seguida, ele chama **TraceReturn** na DLL de rastreamento. Essa função usa dois argumentos: o valor retornado pela DLL de rastreamento para a função de rastreamento e o código de retorno retornado pelo driver para o Gerenciador de driver para a função ODBC (ou o valor retornado pelo próprio Gerenciador de driver se ele tiver processado a função). A função usa o valor retornado para a função de rastreamento para manipular valores de argumento de entrada capturados. Ele grava o código retornado para a função ODBC no arquivo de log (ou exibe-o dinamicamente, se estiver habilitado). Ele desreferencia os ponteiros do argumento de saída e registra os valores de argumento de saída.
