---
title: SQLSetConnectAttr (Biblioteca cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a87c85d727fb9eb2fc27613b9eecd3fe0ec51b58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300536"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetConnectAttr** na biblioteca do cursor. Para obter informações gerais sobre **o SQLSetConnectAttr,** consulte [SQLSetConnectAttr Function](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Um aplicativo chama **SQLSetConnectAttr** com o atributo SQL_ATTR_ODBC_CURSORS para especificar se a biblioteca do cursor está sempre usada, usada se o driver não suporta cursors roláveis ou nunca usado. A biblioteca do cursor assume que um driver suporta cursores roláveis se ele retornar SQL_CA1_RELATIVE para o SQL_STATIC_CURSOR_ATTRIBUTES1 tipo de informação no **SQLGetInfo**.  
  
 O aplicativo deve ligar para **o SQLSetConnectAttr** para especificar o uso da biblioteca do cursor depois de chamar **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC para alocar a conexão e antes que ela se conecte à fonte de dados. Se um aplicativo chamar **SQLSetConnectAttr** com o atributo SQL_ATTR_ODBC_CURSORS enquanto a conexão ainda estiver ativa, a biblioteca do cursor retorna um erro.  
  
 Para definir um atributo de declaração suportado pela biblioteca do cursor para todas as instruções associadas a uma conexão, um aplicativo deve chamar **SQLSetConnectAttr** para esse atributo de declaração depois de se conectar à fonte de dados e antes de abrir o cursor. Se um aplicativo chamar **SQLSetConnectAttr** com um atributo de declaração e um cursor estiver aberto em uma declaração associada à conexão, o atributo de declaração não será aplicado a essa declaração até que o cursor seja fechado e reaberto.
