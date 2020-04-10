---
title: Método isBeforeFirst (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isBeforeFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0e2bd28-6949-47dc-b9dd-145ffb337069
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ab4b8639502f24f3bbe8946f19e5f5f2f197828
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909742"
---
# <a name="isbeforefirst-method-sqlserverresultset"></a>Método isBeforeFirst (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se o cursor está antes da primeira linha no objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isBeforeFirst()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se o cursor for anterior à primeira linha. **false** se o cursor estiver em qualquer outra posição ou se o conjunto de resultados não contiver nenhuma linha.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método isBeforeFirst é especificado pelo método isBeforeFirst na interface java.sql.ResultSet.  
  
 Se esse método for usado com cursores dinâmicos, incluindo cursores somente encaminhamento e somente leitura, e se a propriedade de conexão selectMethod estiver definida como "cursor", ocorrerá uma exceção.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
