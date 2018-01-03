---
title: Implementando SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c32f6f927dfc62a3a9adb782619c469e0edc995b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementando SQLGetDiagRec e SQLGetDiagField
**SQLGetDiagRec** e **SQLGetDiagField** são implementados pelo Gerenciador de Driver e cada driver. O Gerenciador de Driver e cada driver mantenham registros de diagnóstico para cada ambiente, a conexão, a instrução e o identificador do descritor e liberará esses registros somente quando outra função seja chamada com que o identificador ou o identificador é liberado.  
  
 Embora o Gerenciador de Driver e cada driver devem determinar primeiro registro status de acordo com as classificações no [sequência de registros de Status](../../../odbc/reference/develop-app/sequence-of-status-records.md), o Gerenciador de Driver determina a sequência de final de registros.  
  
 **SQLGetDiagRec** e **SQLGetDiagField** não publique os registros de diagnóstico sobre eles.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Regras de tratamento de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Função do Gerenciador do Driver](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Função do driver](../../../odbc/reference/develop-app/role-of-the-driver.md)
