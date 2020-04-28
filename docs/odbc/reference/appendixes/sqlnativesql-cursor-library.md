---
title: SQLNativeSql (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41f7617530f34d49852ca67db9f47cab94292385
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300566"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLNativeSql** na biblioteca de cursores. Para obter informações gerais sobre **SQLNativeSql**, consulte [SQLNativeSql function](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Se o driver oferecer suporte a essa função, a biblioteca de cursores chamará **SQLNativeSql** no driver e passará a instrução SQL. Para a atualização posicionada, a exclusão posicionada e as instruções **SELECT for Update** , a biblioteca de cursores modifica a instrução antes de passá-la para o driver.  
  
> [!NOTE]  
>  A biblioteca de cursor retorna incorretamente SQLSTATE 34000 (nome de cursor inválido) se o nome do cursor for inválido em uma instrução UPDATE ou DELETE posicionada que é passada no argumento *InStatementText* de **SQLNativeSql**. **SQLNativeSql** não se destina a retornar erros de sintaxe, que são retornados somente mediante preparação ou execução de instrução.
