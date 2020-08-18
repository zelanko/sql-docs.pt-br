---
description: SQLExtendedFetch (Driver ODBC do Visual FoxPro)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f938dda4e9e474854d62c50401ee0bf91317983
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449168"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 2  
  
 Semelhante a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) , mas retorna várias linhas usando uma matriz para cada coluna. O conjunto de resultados é de encaminhamento progressivo e pode ser rolado para trás se o cursor for definido como estático, não somente encaminhamento.  
  
 Por padrão, o driver ODBC do Visual FoxPro não retorna linhas marcadas como excluídas em uma tabela do FoxPro. As linhas marcadas para exclusão, mas ainda não foram removidas de uma tabela, não estão incluídas no cursor do conjunto de resultados. Você pode alterar esse comportamento usando o comando [set Deleted](../../odbc/microsoft/set-deleted-command.md) .  
  
 Para obter mais informações, consulte [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) na *referência do programador de ODBC*.
