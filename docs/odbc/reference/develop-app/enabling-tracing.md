---
title: Habilitando o rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb6d8eaf4a1f4eaadc4e8e9a7030b81c373d8377
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819914"
---
# <a name="enabling-tracing"></a>Habilitar o rastreamento
O rastreamento pode ser ativado a seguir três maneiras:  
  
-   Defina as **rastreamento** e **TraceFile** palavras-chave na entrada do registro ini. Isso habilita ou desabilita o rastreamento quando **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV é chamado. Essas opções são definidas na guia rastreamento da caixa de diálogo Administrador de fonte de dados ODBC, exibida durante a instalação da fonte de dados. Para obter mais informações, consulte [entradas do registro para fontes de dados](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chame **SQLSetConnectAttr** para definir o atributo de conexão SQL_ATTR_TRACE como SQL_OPT_TRACE_ON. Isso habilita ou desabilita o rastreamento durante a conexão. Para obter mais informações, consulte o [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descrição da função.  
  
-   Use **ODBCSharedTraceFlag** para ativar ou desativar o rastreamento dinamicamente. (Para obter mais informações, consulte o próximo tópico, [rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md).)
