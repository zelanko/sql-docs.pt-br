---
title: SQLSetConnectAttr (biblioteca de cursores) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d4023c513ffda04a3cf499110185d3746ca40d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299184"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetConnectAttr** função na biblioteca de cursor. Para obter informações gerais sobre **SQLSetConnectAttr**, consulte [função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Um aplicativo chama **SQLSetConnectAttr** com o atributo SQL_ATTR_ODBC_CURSORS para especificar se a biblioteca de cursores é sempre usada, usada se o driver não oferece suporte a cursores roláveis ou nunca foi usada. A biblioteca de cursores pressupõe que um driver dá suporte a cursores roláveis se ele retornar SQL_CA1_RELATIVE para o tipo de informações SQL_STATIC_CURSOR_ATTRIBUTES1 na **SQLGetInfo**.  
  
 O aplicativo deve chamar **SQLSetConnectAttr** para especificar o uso da biblioteca de cursor, depois que ele chama **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC para alocar a conexão e antes de se conectar à fonte de dados. Se um aplicativo chamar **SQLSetConnectAttr** com o atributo SQL_ATTR_ODBC_CURSORS enquanto a conexão ainda está ativa, a biblioteca de cursores retornará um erro.  
  
 Para definir um atributo de instrução com suporte pela biblioteca de cursores para todas as instruções associadas com uma conexão, um aplicativo deve chamar **SQLSetConnectAttr** para esse atributo de instrução depois que ele se conecta à fonte de dados e antes que ele Abre o cursor. Se um aplicativo chamar **SQLSetConnectAttr** com uma instrução de atributo e um cursor é aberto em uma instrução associada com a conexão, o atributo de instrução não será aplicado à instrução até que o cursor seja fechado e reaberta.
