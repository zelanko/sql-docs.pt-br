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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddd0ee24649592cf4a1a296a51404334145a3bab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298053"
---
# <a name="trace-file"></a>Arquivo de rastreamento
Um aplicativo especifica o arquivo de rastreamento, seja definindo a palavra-chave **TraceFile** na entrada de registro Odbc.ini ou ligando para **SQLSetConnectAttr** com o atributo de conexão SQL_ATTR_TRACEFILE. Se o arquivo não existir quando o rastreamento estiver ativado, o Gerenciador de driver criará o arquivo. Cada aplicativo deve ter seu próprio arquivo de rastreamento dedicado para evitar a contenção. Um aplicativo pode usar mais de um arquivo de rastreamento; o programa de configuração de um aplicativo pode fornecer ao usuário uma escolha de arquivos de rastreamento. Se o rastreamento estiver ativado dinamicamente, um aplicativo também poderá exibir resultados de rastreamento, em vez de fazer login no arquivo de rastreamento.  
  
 O arquivo de rastreamento fornece um registro de cada chamada de função ODBC com os tipos de dados e valores de todos os argumentos. Ele registra todas as funções de entrada e registra todas as funções retornadas com códigos de retorno e estados de erro.  
  
 Em ODBC *3.x,* os parâmetros para as funções de conexão não são fornecidos para o dLL de rastreamento.
