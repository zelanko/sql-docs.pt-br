---
title: Habilitar o rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad1f3aa8fc8280748eb7e3a99a62c500e0b283dd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="enabling-tracing"></a>A habilitação do rastreamento
O rastreamento pode ser ativado no exemplo a seguir três maneiras:  
  
-   Definir o **rastreamento** e **TraceFile** palavras-chave na entrada do registro Odbc.ini. Isso habilita ou desabilita o rastreamento quando **SQLAllocHandle** com um *HandleType* SQL_HANDLE_ENV é chamado. Essas opções são definidas na guia de rastreamento da caixa de diálogo Administrador de fonte de dados ODBC exibida durante a instalação da fonte de dados. Para obter mais informações, consulte [entradas do registro para fontes de dados](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chamar **SQLSetConnectAttr** para definir o atributo de conexão SQL_ATTR_TRACE para SQL_OPT_TRACE_ON. Isso habilita ou desabilita o rastreamento durante a conexão. Para obter mais informações, consulte o [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descrição da função.  
  
-   Use **ODBCSharedTraceFlag** para ativar ou desativar o rastreamento dinamicamente. (Para obter mais informações, consulte o próximo tópico, [rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md).)
