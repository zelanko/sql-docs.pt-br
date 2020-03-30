---
title: Método updateDouble (java.lang.String, double) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateDouble (java.lang.String, double)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f70971d5-34cc-4f70-8a91-5d46356b24ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15617e1d5dda6315547228e07853c373f9eb1a37
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67999035"
---
# <a name="updatedouble-method-javalangstring-double"></a>Método updateDouble (java.lang.String, double)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **double**, considerando o nome da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateDouble(java.lang.String columnName,  
                         double x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *x*  
  
 Um valor **double**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateDouble é especificado pelo método updateDouble na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateDouble &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
