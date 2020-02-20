---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c36d7980355eed1e1a1e8f42fb53c75fdb70d0ed
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976954"
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
  
  
