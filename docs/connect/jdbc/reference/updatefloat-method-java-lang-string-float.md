---
title: Método updateFloat (java.lang.String, float) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateFloat (java.lang.String, float)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19a6164f-f560-4304-8466-e55f0667a3d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4563da01d0d00ddaa0aca3fff551691083bd1353
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927855"
---
# <a name="updatefloat-method-javalangstring-float"></a>Método updateFloat (java.lang.String, float)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **float**, considerando o nome da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateFloat(java.lang.String columnName,  
                        float x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *x*  
  
 Um valor **float**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateFloat é especificado pelo método updateFloat na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateFloat &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
