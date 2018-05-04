---
title: Método (SQLServerResultSet) rowUpdated | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 244272de76744a5506f4d129c49fe1f277a3f89d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rowupdated-method-sqlserverresultset"></a>rowUpdated método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se a linha atual foi atualizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se a linha foi atualizada visivelmente pelo proprietário ou outro usuário, e as atualizações são detectadas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método rowUpdated é especificado pelo método rowUpdated na interface Java.SQL. resultset.  
  
 O valor que é retornado dependerá da capacidade do conjunto de resultados de detectar atualizações.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] não detecta linhas atualizadas para qualquer tipo de cursor.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
