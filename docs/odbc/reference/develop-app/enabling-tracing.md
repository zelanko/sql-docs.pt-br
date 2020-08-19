---
description: Habilitar o rastreamento
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af9a78989a80124fb9a7f475edf17022e7942bde
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482979"
---
# <a name="enabling-tracing"></a>Habilitar o rastreamento
O rastreamento pode ser habilitado das três maneiras a seguir:  
  
-   Defina as palavras-chave **trace** e **TraceFile** na entrada do registro Odbc.ini. Isso habilita ou desabilita o rastreamento quando **SQLAllocHandle** com um *handletype* de SQL_HANDLE_ENV é chamado. Essas opções são definidas na guia rastreamento da caixa de diálogo administrador de fonte de dados ODBC exibida durante a configuração da fonte de dados. Para obter mais informações, consulte [entradas de registro para fontes de dados](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chame **SQLSetConnectAttr** para definir o atributo de conexão SQL_ATTR_TRACE como SQL_OPT_TRACE_ON. Isso habilita ou desabilita o rastreamento para a duração da conexão. Para obter mais informações, consulte a descrição da função [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) .  
  
-   Use **ODBCSharedTraceFlag** para ativar ou desativar o rastreamento dinamicamente. (Para obter mais informações, consulte o próximo tópico, [rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md).)
