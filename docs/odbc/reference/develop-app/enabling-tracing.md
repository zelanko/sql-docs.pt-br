---
title: Habilitar o rastreamento | Microsoft Docs
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
helpviewer_keywords: tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 569c5b42c57bca4eff30225f5dcc1ff1176fe00e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="enabling-tracing"></a>A habilitação do rastreamento
O rastreamento pode ser ativado no exemplo a seguir três maneiras:  
  
-   Definir o **rastreamento** e **TraceFile** palavras-chave na entrada do registro Odbc.ini. Isso habilita ou desabilita o rastreamento quando **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV é chamado. Essas opções são definidas na guia de rastreamento da caixa de diálogo Administrador de fonte de dados ODBC exibida durante a instalação da fonte de dados. Para obter mais informações, consulte [entradas do registro para fontes de dados](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chamar **SQLSetConnectAttr** para definir o atributo de conexão SQL_ATTR_TRACE para SQL_OPT_TRACE_ON. Isso habilita ou desabilita o rastreamento durante a conexão. Para obter mais informações, consulte o [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descrição da função.  
  
-   Use **ODBCSharedTraceFlag** para ativar ou desativar o rastreamento dinamicamente. (Para obter mais informações, consulte o próximo tópico, [rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md).)
