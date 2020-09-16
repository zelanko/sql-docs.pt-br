---
description: Método jdbcCompliant (SQLServerDriver)
title: Método jdbcCompliant (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25495005dafdc95982b2f7005c96eb186c864caf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433278"
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>Método jdbcCompliant (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Verifica se o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] é compatível com a especificação do JDBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se o driver JDBC atender aos requisitos mínimos. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Esse método jdbcCompliant é especificado pelo método jdbcCompliant na interface java.sql.Driver.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Membros do SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Classe SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
