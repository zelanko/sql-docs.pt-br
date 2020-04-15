---
title: Traçado Dinâmico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8cbd2dbae4f4b437f45845ce2791f4a9b0aa8c8b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305757"
---
# <a name="dynamic-tracing"></a>Rastreamento dinâmico
O rastreamento pode ser ativado ou desativado a qualquer momento em uma execução de aplicativo. Isso permite que um aplicativo rastreie qualquer número de chamadas de função.  
  
 A variável **ODBCSharedTraceFlag** está definida para permitir o rastreamento dinamicamente. Esta variável é compartilhada entre todas as cópias em execução do Driver Manager. Se algum aplicativo definir essa variável, o rastreamento será ativado para todos os aplicativos ODBC em execução atualmente. Para desativar o rastreamento quando o rastreamento dinâmico estiver ativado, um aplicativo chama **o SQLSetConnectAttr** para definir SQL_ATTR_TRACE para SQL_TRACE_OFF. Esta chamada desligará apenas o rastreamento para esse aplicativo. Os aplicativos vinculados ao Odbc32.lib podem modificar o uso desta variável. Os dados de rastreamento podem ser exibidos em uma janela em tempo real, em vez do arquivo de rastreamento, que deve ser aberto após a sessão ODBC. Os controles podem ser adicionados à tela de um aplicativo para ativar ou desativar o rastreamento à vontade.  
  
 O dll de rastreamento enviado com ODBC 3 *.x* não é seguro para rosca. Não é garantido que o arquivo de log seja gravado corretamente se o rastreamento global estiver ativado (a variável **ODBCSharedTraceFlag** está definida) e mais de um aplicativo grava no arquivo de rastreamento ao mesmo tempo. Esta condição não retorna um erro.
