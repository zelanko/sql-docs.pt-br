---
title: SQLSetPos (Drivers de banco de dados da área de trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95117c82c213851d2e0600e65d8061ce532d9933
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200455"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (Drivers de banco de dados de área de trabalho)
A semântica do modelo em massa para **SQLSetPos** chamadas com o *irow* argumento igual a 0 são suportados.  
  
 SQL_LOCK_NO_CHANGE há suporte para *usam*. Não há suporte para SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK.  
  
 **SQLSetPos** dá suporte a junções atualizáveis. (Para obter mais informações, consulte o *guia do programador do Microsoft Jet banco de dados Engine*.)
