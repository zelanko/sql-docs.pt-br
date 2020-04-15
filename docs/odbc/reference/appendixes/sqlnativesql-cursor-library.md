---
title: SQLNativeSql (Biblioteca Cursor) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300566"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLNativeSql** na biblioteca do cursor. Para obter informações gerais sobre **sqlnativesql**, consulte [SQLNativeSql Function](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Se o driver suportar essa função, a biblioteca do cursor liga para **SQLNativeSql** no driver e passa-a para a declaração SQL. Para atualização posicionada, exclusão posicionada e **instruções SELECT FOR UPDATE,** a biblioteca do cursor modifica a instrução antes de passá-la ao driver.  
  
> [!NOTE]  
>  A biblioteca do cursor retorna incorretamente SQLSTATE 34000 (nome do cursor inválido) se o nome do cursor for inválido em uma declaração de atualização ou exclusão posicionada que é passada no argumento *InStatementText* de **SQLNativeSql**. **O SQLNativeSql** não se destina a retornar erros de sintaxe, que são devolvidos apenas após a preparação ou execução da declaração.
