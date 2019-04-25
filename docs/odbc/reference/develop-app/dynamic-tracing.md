---
title: Rastreamento dinâmico | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63dbfda01d96cad53e5830e598b5812ed79d8f04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468773"
---
# <a name="dynamic-tracing"></a>Rastreamento dinâmico
O rastreamento pode ser habilitado ou desabilitado em qualquer ponto em um aplicativo execute. Isso permite que um aplicativo rastrear qualquer número de chamadas de função.  
  
 A variável **ODBCSharedTraceFlag** é definido para habilitar o rastreamento dinamicamente. Essa variável é compartilhada entre todas as cópias em execução do Gerenciador de Driver. Se qualquer aplicativo define essa variável, o rastreamento está habilitado para todos os aplicativos ODBC em execução no momento. Para ativar o rastreamento desativado quando o rastreamento dinâmico está habilitado, um aplicativo chama **SQLSetConnectAttr** definir SQL_ATTR_TRACE como SQL_TRACE_OFF. Essa chamada ativará o rastreamento para o aplicativo apenas. Aplicativos que estão vinculados com Odbc32.lib podem modificar o uso dessa variável. Dados de rastreamento podem ser exibidos em uma janela em tempo real, em vez do arquivo de rastreamento, que deve ser aberta após a sessão ODBC. Controles podem ser adicionados à tela do aplicativo para ativar ou desativar o rastreamento no será.  
  
 O rastreamento de DLL acompanha o ODBC 3 *. x* não é thread-safe. Não há garantia de que o arquivo de log é gravado corretamente se o rastreamento global é habilitado (a variável **ODBCSharedTraceFlag** é definido) e mais de um aplicativo grava no arquivo de rastreamento ao mesmo tempo. Essa condição não retorna um erro.
