---
title: "SQLSetPos (Drivers do banco de dados de área de trabalho) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b630be96f099e1f2553c8d03b9896f32ea3e670
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (Drivers do banco de dados de área de trabalho)
A semântica do modelo em massa para **SQLSetPos** chamadas com o *irow* argumento igual a 0 são suportados.  
  
 Há suporte para SQL_LOCK_NO_CHANGE para *fLock*. Não há suporte para SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK.  
  
 **SQLSetPos** oferece suporte a junções atualizáveis. (Para obter mais informações, consulte o *guia do programador do Microsoft Jet Database Engine*.)
