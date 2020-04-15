---
title: SQLBindParameter (Biblioteca cursor) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55708cc5192fb40149d6db7710f6ee638c4880d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305424"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLBindParameter** na biblioteca do cursor. Para obter informações gerais sobre **o SQLBindParameter,** consulte [SQLBindParameter Function .](../../../odbc/reference/syntax/sqlbindparameter-function.md)  
  
 Um aplicativo pode chamar **SQLBindParameter** para revincular parâmetros, desde que o tipo de dados C, o tamanho da coluna e os dígitos decimais da coluna vinculada permaneçam os mesmos.  
  
 A biblioteca do cursor suporta a definição do atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR para usar deslocamentos de vinculação. **(SQLBindParameter** não precisa ser chamado para que essa revinculação ocorra.)  
  
 A biblioteca do cursor suporta parâmetros vinculativos de data-at-execution.
