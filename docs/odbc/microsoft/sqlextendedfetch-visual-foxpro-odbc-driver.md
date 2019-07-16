---
title: SQLExtendedFetch (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d58d7885eed1a8ed0611470f29cb24e8072afcb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053806"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível 2  
  
 Semelhante ao [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) , mas retorna várias linhas usando uma matriz para cada coluna. O conjunto de resultados é rolável de encaminhamento e pode ser feito com versões anteriores-rolável se o cursor é definido como estático, não apenas de encaminhamento.  
  
 Por padrão, o Driver de ODBC do Visual FoxPro não retorna linhas marcadas como excluídas em uma tabela FoxPro. Marcado para exclusão, mas ainda não foram removidas de uma tabela de linhas não são incluídas no cursor de conjunto de resultados. Você pode alterar esse comportamento usando o [definir excluído](../../odbc/microsoft/set-deleted-command.md) comando.  
  
 Para obter mais informações, consulte [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) na *referência do programador de ODBC*.
