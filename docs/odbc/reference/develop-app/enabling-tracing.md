---
title: Habilitando o Rastreamento | Microsoft Docs
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
ms.openlocfilehash: 80bd4023a0260b67d11d7b4ded1bb810b81e0ab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287346"
---
# <a name="enabling-tracing"></a>Habilitar o rastreamento
O rastreamento pode ser ativado das seguintes três maneiras:  
  
-   Defina as palavras-chave **Trace** e **TraceFile** na entrada de registro Odbc.ini. Isso ativa ou desativa o rastreamento quando **o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_ENV é chamado. Essas opções estão definidas na guia Rastreamento da caixa de diálogo Administrador de origem de dados ODBC exibida durante a configuração da fonte de dados. Para obter mais informações, consulte [Entradas de registro para fontes de dados](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Ligue para **sqlsetconnectattr** para definir o atributo de conexão SQL_ATTR_TRACE para SQL_OPT_TRACE_ON. Isso permite ou desativa o rastreamento durante a duração da conexão. Para obter mais informações, consulte a descrição da função [SQLSetConnectAttr.](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   Use **ODBCSharedTraceFlag** para ativar ou desativar o rastreamento dinamicamente. (Para obter mais informações, consulte o próximo tópico, [Dynamic Tracing](../../../odbc/reference/develop-app/dynamic-tracing.md).)
