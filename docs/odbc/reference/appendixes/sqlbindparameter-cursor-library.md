---
title: SQLBindParameter (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7943987d52554e0f5cd7723e8c9ae8a0e3afddd2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093036"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLBindParameter** na biblioteca de cursores. Para obter informações gerais sobre **SQLBindParameter**, consulte [SQLBindParameter function](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Um aplicativo pode chamar **SQLBindParameter** para reassociar parâmetros, desde que o tipo de dados C, o tamanho da coluna e os dígitos decimais da coluna associada permaneçam os mesmos.  
  
 A biblioteca de cursores dá suporte à definição do atributo instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para usar deslocamentos de ligação. (**SQLBindParameter** não precisa ser chamado para que essa reassociação ocorra.)  
  
 A biblioteca de cursores dá suporte à associação de parâmetros de dados em execução.
