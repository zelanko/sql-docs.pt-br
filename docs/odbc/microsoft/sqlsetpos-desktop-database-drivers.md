---
title: "SQLSetPos (Drivers do banco de dados de área de trabalho) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9355b4d4d21eb6cfdc3b90a306625892737e993d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (Drivers do banco de dados de área de trabalho)
A semântica do modelo em massa para **SQLSetPos** chamadas com o *irow* argumento igual a 0 são suportados.  
  
 Há suporte para SQL_LOCK_NO_CHANGE para *fLock*. Não há suporte para SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK.  
  
 **SQLSetPos** oferece suporte a junções atualizáveis. (Para obter mais informações, consulte o *guia do programador do Microsoft Jet Database Engine*.)
