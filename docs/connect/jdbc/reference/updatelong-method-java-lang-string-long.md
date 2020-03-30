---
title: Método updateLong (java.lang.String, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateLong (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6003706-35de-42b1-8f23-899a388adb5b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 932035288f74c582620108db697cb898c59159bc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67999168"
---
# <a name="updatelong-method-javalangstring-long"></a>Método updateLong (java.lang.String, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **long**, considerando o nome da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateLong(java.lang.String columnName,  
                       long x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *x*  
  
 Um valor **long**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateLong é especificado pelo método updateLong na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateLong &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
