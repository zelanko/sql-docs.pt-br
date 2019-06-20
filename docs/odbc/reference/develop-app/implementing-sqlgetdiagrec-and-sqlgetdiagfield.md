---
title: Implementando SQLGetDiagRec e SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab1f808b005afaa91ed93bf8f8ec7a8385c9c945
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447279"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>Implementar SQLGetDiagRec e SQLGetDiagField
**SQLGetDiagRec** e **SQLGetDiagField** são implementadas por cada driver e o Gerenciador de Driver. O Gerenciador de Driver e cada driver mantenham registros de diagnóstico para cada ambiente, a conexão, a instrução e o identificador do descritor e liberem os registros somente quando a outra função seja chamada com que o identificador ou o identificador é liberado.  
  
 Embora o Gerenciador de Driver e cada driver devem determinar o primeiro registro de status acordo com as classificações nas [sequência de registros de Status](../../../odbc/reference/develop-app/sequence-of-status-records.md), o Gerenciador de Driver determina a sequência de final de registros.  
  
 **SQLGetDiagRec** e **SQLGetDiagField** não publique os registros de diagnóstico sobre si mesmos.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Regras de tratamento de diagnóstico](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [Função do Gerenciador do Driver](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [Função do driver](../../../odbc/reference/develop-app/role-of-the-driver.md)
