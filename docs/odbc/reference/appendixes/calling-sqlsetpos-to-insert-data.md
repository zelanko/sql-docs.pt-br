---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e07bf71f0d622ad9095974cd7020001625edf1f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037711"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Chamar SQLSetPos para inserir dados
Quando um ODBC *2.x* aplicativo trabalhar com ODBC *3.x* driver chama **SQLSetPos** com um *operação* argumento de SQL_ADD, o Gerenciador de driver não é mapeado para essa chamada para **SQLBulkOperations**. Se um ODBC *3.x* driver deve funcionar com um aplicativo que chama **SQLSetPos** com SQL_ADD, o driver deve dar suporte a essa operação.  
  
 Uma grande diferença no comportamento quando **SQLSetPos** é chamado com SQL_ADD ocorre quando ele é chamado no estado S6. Em ODBC *2.x*, o driver retornou S1010 quando **SQLSetPos** foi chamado com SQL_ADD no estado S6 (depois que o cursor foi posicionado com **SQLFetch**). Em ODBC *3.x*, **SQLBulkOperations** com um *operação* de SQL_ADD pode ser chamado no estado S6. Uma grande diferença no comportamento a segunda é que **SQLBulkOperations** com um *operação* de SQL_ADD pode ser chamado no estado S5, enquanto **SQLSetPos** com um  **Operação** de SQL_ADD não é possível. Para as transições de instrução que podem ocorrer para a mesma chamada em ODBC *3.x*, consulte [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
