---
title: Método rowUpdated (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b827ebb9740c9d88017c5d47626b9a1cef493143
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66765271"
---
# <a name="rowupdated-method-sqlserverresultset"></a>Método rowUpdated (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se a linha atual foi atualizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se a linha foi atualizada visivelmente pelo proprietário ou de outro usuário e as atualizações são detectadas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método rowUpdated é especificado pelo método rowUpdated na interface do resultset.  
  
 O valor que é retornado dependerá da capacidade do conjunto de resultados de detectar atualizações.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não detecta linhas atualizadas para qualquer tipo de cursor.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
