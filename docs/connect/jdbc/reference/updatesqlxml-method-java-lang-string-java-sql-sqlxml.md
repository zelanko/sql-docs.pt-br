---
title: Método updateSQLXML (java.lang.String, java.sql.SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 60021881-ef83-499b-9977-e20ff23c1312
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e2772b43c084e1780b8e65cd6425b67d01092f1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67998286"
---
# <a name="updatesqlxml-method-javalangstring-javasqlsqlxml"></a>Método updateSQLXML (java.lang.String, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor java.sql.SQLXML.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateSQLXML(java.lang.String columnLabel,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnLabel*  
  
 Uma **Cadeia de Caracteres** que indica o rótulo de coluna.  
  
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
  
  
