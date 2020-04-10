---
title: Método updateSQLXML (int, java.sql.SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5170751-fbe1-433b-96f5-4f237ba55f60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a1fac23bf7ff998d971fdc05557839c6b230a89
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919631"
---
# <a name="updatesqlxml-method-int-javasqlsqlxml"></a>Método updateSQLXML (int, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor java.sql.SQLXML  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateSQLXML(int columnIndex,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice de coluna.  
  
 *xmlObject*  
  
 Um objeto SQLXML.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateSQLXML é especificado pelo método updateSQLXML na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateSQLXML &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
