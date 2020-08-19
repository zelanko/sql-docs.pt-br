---
description: SQLSetConnectAttr (Biblioteca de cursores)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b809ad81e9edaca7fbe7d40952673a1698f113e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424888"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetConnectAttr** na biblioteca de cursores. Para obter informações gerais sobre **SQLSetConnectAttr**, consulte [SQLSetConnectAttr function](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Um aplicativo chama **SQLSetConnectAttr** com o atributo SQL_ATTR_ODBC_CURSORS para especificar se a biblioteca de cursores sempre será usada, usada se o driver não oferecer suporte a cursores roláveis ou nunca usado. A biblioteca de cursores pressupõe que um driver dá suporte a cursores roláveis se retornar SQL_CA1_RELATIVE para o tipo de informação SQL_STATIC_CURSOR_ATTRIBUTES1 em **SQLGetInfo**.  
  
 O aplicativo deve chamar **SQLSetConnectAttr** para especificar o uso da biblioteca de cursores depois de chamar **SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC para alocar a conexão e antes de se conectar à fonte de dados. Se um aplicativo chamar **SQLSetConnectAttr** com o atributo SQL_ATTR_ODBC_CURSORS enquanto a conexão ainda estiver ativa, a biblioteca de cursores retornará um erro.  
  
 Para definir um atributo de instrução com suporte na biblioteca de cursores para todas as instruções associadas a uma conexão, um aplicativo deve chamar **SQLSetConnectAttr** para esse atributo de instrução depois de se conectar à fonte de dados e antes de abrir o cursor. Se um aplicativo chamar **SQLSetConnectAttr** com um atributo de instrução e um cursor estiver aberto em uma instrução associada à conexão, o atributo de instrução não será aplicado a essa instrução até que o cursor seja fechado e reaberto.
