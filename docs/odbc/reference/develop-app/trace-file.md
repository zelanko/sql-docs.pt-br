---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e0ca79b64cafcd2ac34c14af120f29781a7ae22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148916"
---
# <a name="trace-file"></a>Arquivo de rastreamento
Um aplicativo especifica o arquivo de rastreamento, definindo o **TraceFile** palavra-chave na entrada do registro ini ou chamando **SQLSetConnectAttr** com o atributo de conexão SQL_ATTR_TRACEFILE. Se o arquivo não existir quando o rastreamento está habilitado, o Gerenciador de Driver criará o arquivo. Cada aplicativo deve ter seu próprio arquivo de rastreamento dedicado para evitar a contenção. Um aplicativo pode usar mais de um arquivo de rastreamento; o programa de instalação do aplicativo pode fornecer ao usuário com uma opção de arquivos de rastreamento. Se o rastreamento é habilitado dinamicamente, um aplicativo também pode exibir resultados de rastreamento, em vez de registro em log para o arquivo de rastreamento.  
  
 O arquivo de rastreamento fornece um log de cada chamada de função ODBC com os tipos de dados e valores de todos os argumentos. Registra todas as entrada de funções e registra em log todas as funções retornadas com códigos de retorno e os estados de erro.  
  
 Em ODBC 3 *. x*, parâmetros para funções de conexão não são fornecidos para a DLL de rastreamento.
