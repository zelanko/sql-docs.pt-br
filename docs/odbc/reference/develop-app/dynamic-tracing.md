---
description: Rastreamento dinâmico
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1618d1b2837c5169f03b07900aba3921bc98659
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482989"
---
# <a name="dynamic-tracing"></a>Rastreamento dinâmico
O rastreamento pode ser habilitado ou desabilitado em qualquer ponto em uma execução de aplicativo. Isso permite que um aplicativo rastreie qualquer número de chamadas de função.  
  
 A variável **ODBCSharedTraceFlag** é definida para habilitar o rastreamento dinamicamente. Essa variável é compartilhada entre todas as cópias em execução do Gerenciador de driver. Se qualquer aplicativo definir essa variável, o rastreamento será habilitado para todos os aplicativos ODBC em execução no momento. Para desativar o rastreamento quando o rastreamento dinâmico está habilitado, um aplicativo chama **SQLSetConnectAttr** para definir SQL_ATTR_TRACE como SQL_TRACE_OFF. Essa chamada ativará o rastreamento somente para esse aplicativo. Os aplicativos que estão vinculados a Odbc32. lib podem modificar o uso dessa variável. Os dados de rastreamento podem ser exibidos em uma janela em tempo real, em vez do arquivo de rastreamento, que deve ser aberto após a sessão ODBC. Os controles podem ser adicionados à tela de um aplicativo para ativar ou desativar o rastreamento no.  
  
 A DLL de rastreamento fornecida com ODBC 3 *. x* não é thread-safe. Não há garantia de que o arquivo de log será gravado corretamente se o rastreamento global estiver habilitado (a variável **ODBCSharedTraceFlag** está definida) e mais de um aplicativo gravar no arquivo de rastreamento ao mesmo tempo. Essa condição não retorna um erro.
