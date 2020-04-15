---
title: SQLSetPos (Drivers de banco de dados de desktop) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e151e3abc4032ea3180e46360c501d9fbea9ae30
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301457"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (Drivers de banco de dados de área de trabalho)
A semântica de modelo em massa para chamadas **SQLSetPos** com o argumento *irow* igual a 0 é suportada.  
  
 SQL_LOCK_NO_CHANGE é suportado para *fLock*. SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK não são suportados.  
  
 **O SQLSetPos** suporta adesão updatable. (Para obter mais informações, consulte o *Guia do Programador do Mecanismo de Banco de Dados do Microsoft Jet*.)
