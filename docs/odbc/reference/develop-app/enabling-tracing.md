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
ms.openlocfilehash: 24f80e0e81e4be8895d59256492b868c53aab7b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046795"
---
# <a name="enabling-tracing"></a>Habilitar o rastreamento
O rastreamento pode ser habilitado das três maneiras a seguir:  
  
-   Defina as palavras-chave **trace** e **TraceFile** na entrada do registro ODBC. ini. Isso habilita ou desabilita o rastreamento quando **SQLAllocHandle** com um *handletype* de SQL_HANDLE_ENV é chamado. Essas opções são definidas na guia rastreamento da caixa de diálogo administrador de fonte de dados ODBC exibida durante a configuração da fonte de dados. Para obter mais informações, consulte [entradas de registro para fontes de dados](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chame **SQLSetConnectAttr** para definir o atributo de conexão SQL_ATTR_TRACE como SQL_OPT_TRACE_ON. Isso habilita ou desabilita o rastreamento para a duração da conexão. Para obter mais informações, consulte a descrição da função [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) .  
  
-   Use **ODBCSharedTraceFlag** para ativar ou desativar o rastreamento dinamicamente. (Para obter mais informações, consulte o próximo tópico, [rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md).)
