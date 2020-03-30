---
title: Método updateObject (java.lang.String, java.lang.Object, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateObject (java.lang.String, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 27283ce1-637e-4e2c-91ee-8ad379114ac5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12645120f543094015f2da03eca224c40e16ab6f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67998463"
---
# <a name="updateobject-method-javalangstring-javalangobject-int"></a>Método updateObject (java.lang.String, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **Object**, considerando o nome da coluna e a escala.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateObject(java.lang.String columnName,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *obj*  
  
 Um valor **Object**.  
  
 *scale*  
  
 Para tipos java.sql.Types.DECIMAL ou java.sql.Types.NUMERIC, esse é o número de dígitos depois da vírgula decimal. Esse valor é ignorado para todos os outros tipos.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateObject é especificado pelo método updateObject na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateObject &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
