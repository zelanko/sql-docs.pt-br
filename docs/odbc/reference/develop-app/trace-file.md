---
title: Arquivo de rastreamento | Microsoft Docs
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
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17820a03e062feb24e3b10e58cbcf29b3feb8ba3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="trace-file"></a>Arquivo de rastreamento
Um aplicativo especifica o arquivo de rastreamento, definindo o **TraceFile** palavra-chave na entrada do registro Odbc.ini ou chamando **SQLSetConnectAttr** com o atributo de conexão SQL_ATTR_TRACEFILE. Se o arquivo não existir quando o rastreamento está habilitado, o Gerenciador de Driver criará o arquivo. Cada aplicativo deve ter seu próprio arquivo de rastreamento dedicado para evitar uma contenção. Um aplicativo pode usar mais de um arquivo de rastreamento; o programa de instalação do aplicativo pode fornecer ao usuário uma opção de arquivos de rastreamento. Se o rastreamento está habilitado dinamicamente, um aplicativo também pode exibir os resultados do rastreamento, em vez de registro em log para o arquivo de rastreamento.  
  
 O arquivo de rastreamento fornece um log de cada chamada de função ODBC com os tipos de dados e valores de todos os argumentos. Registra todas as entrada de funções e registra em log todas as funções retornadas com códigos de retorno e estados de erro.  
  
 Em ODBC 3*. x*, parâmetros para funções de conexão não são fornecidos para a DLL de rastreamento.
