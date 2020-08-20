---
description: Arquivo de rastreamento
title: Arquivo de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba45e44baaba68d1c203e83a25c9db305642e6d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487489"
---
# <a name="trace-file"></a>Arquivo de rastreamento
Um aplicativo especifica o arquivo de rastreamento definindo a palavra-chave **TraceFile** na entrada do registro Odbc.ini ou chamando **SQLSetConnectAttr** com o atributo de conexão SQL_ATTR_TRACEFILE. Se o arquivo não existir quando o rastreamento estiver habilitado, o Gerenciador de driver criará o arquivo. Cada aplicativo deve ter seu próprio arquivo de rastreamento dedicado para evitar a contenção. Um aplicativo pode usar mais de um arquivo de rastreamento; o programa de instalação de um aplicativo pode fornecer ao usuário uma opção de arquivos de rastreamento. Se o rastreamento for habilitado dinamicamente, um aplicativo também poderá exibir resultados de rastreamento, em vez de fazer logon no arquivo de rastreamento.  
  
 O arquivo de rastreamento fornece um log de cada chamada de função ODBC com os tipos de dados e valores de todos os argumentos. Ele registra todas as funções de entrada e registra em log todas as funções retornadas com códigos de retorno e Estados de erro.  
  
 No ODBC *3. x*, os parâmetros para as funções de conexão não são fornecidos para a DLL de rastreamento.
