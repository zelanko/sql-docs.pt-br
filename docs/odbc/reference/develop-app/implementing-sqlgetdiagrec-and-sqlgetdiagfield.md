---
title: Implementando SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a6be0d20a2e1171275c3a1ef05d83383a10b763
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementando SQLGetDiagRec e SQLGetDiagField
**SQLGetDiagRec** e **SQLGetDiagField** são implementados pelo Gerenciador de Driver e cada driver. O Gerenciador de Driver e cada driver mantenham registros de diagnóstico para cada ambiente, a conexão, a instrução e o identificador do descritor e liberará esses registros somente quando outra função seja chamada com que o identificador ou o identificador é liberado.  
  
 Embora o Gerenciador de Driver e cada driver devem determinar primeiro registro status de acordo com as classificações no [sequência de registros de Status](../../../odbc/reference/develop-app/sequence-of-status-records.md), o Gerenciador de Driver determina a sequência de final de registros.  
  
 **SQLGetDiagRec** e **SQLGetDiagField** não publique os registros de diagnóstico sobre eles.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Regras de tratamento de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Função do Gerenciador do Driver](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Função do driver](../../../odbc/reference/develop-app/role-of-the-driver.md)
