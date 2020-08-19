---
description: Chamar SQLSetPos para inserir dados
title: Chamando SQLSetPos para inserir dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 215d02e9b5bd92f6a22f7e45c8c29c7c5a0a6a4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449008"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Chamar SQLSetPos para inserir dados
Quando um aplicativo ODBC *2. x* que trabalha com um driver ODBC *3. x* chama **SQLSetPos** com um argumento de *operação* de SQL_ADD, o Gerenciador de driver não mapeia essa chamada para **SQLBulkOperations**. Se um driver ODBC *3. x* funcionar com um aplicativo que chama **SQLSetPos** com SQL_ADD, o driver deverá dar suporte a essa operação.  
  
 Uma grande diferença no comportamento quando **SQLSetPos** é chamado com SQL_ADD ocorre quando é chamado no estado s6. No ODBC *2. x*, o driver retornou S1010 quando **SQLSetPos** foi chamado com SQL_ADD no estado S6 (depois que o cursor tiver sido posicionado com **SQLFetch**). No ODBC *3. x*, **SQLBulkOperations** com uma *operação* de SQL_ADD pode ser chamado no estado s6. Uma segunda grande diferença no comportamento é que **SQLBulkOperations** com uma *operação* de SQL_ADD pode ser chamado no estado S5, enquanto **SQLSetPos** com uma **operação** de SQL_ADD não pode. Para as transições de instrução que podem ocorrer para a mesma chamada no ODBC *3. x*, consulte o [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
