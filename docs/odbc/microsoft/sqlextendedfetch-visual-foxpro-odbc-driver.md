---
title: SQLExtendedFetch (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053806"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 2  
  
 Semelhante a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) , mas retorna várias linhas usando uma matriz para cada coluna. O conjunto de resultados é de encaminhamento progressivo e pode ser rolado para trás se o cursor for definido como estático, não somente encaminhamento.  
  
 Por padrão, o driver ODBC do Visual FoxPro não retorna linhas marcadas como excluídas em uma tabela do FoxPro. As linhas marcadas para exclusão, mas ainda não foram removidas de uma tabela, não estão incluídas no cursor do conjunto de resultados. Você pode alterar esse comportamento usando o comando [set Deleted](../../odbc/microsoft/set-deleted-command.md) .  
  
 Para obter mais informações, consulte [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) na *referência do programador de ODBC*.
