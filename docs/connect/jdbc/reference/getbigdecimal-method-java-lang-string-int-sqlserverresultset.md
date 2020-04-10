---
title: Método getBigDecimal (java.lang.String, int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBigDecimal (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 572a1799-c232-400f-b8d8-37a5719a8d5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db42729446b2007a730c5fda795cf628eea0fc5f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920603"
---
# <a name="getbigdecimal-method-javalangstring-int-sqlserverresultset"></a>Método getBigDecimal (java.lang.String, int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) usando a escala fornecida.  
  
> [!NOTE]  
>  Esse método foi substituído na especificação do JDBC. Em vez disso, você deve usar o método [getBigDecimal (java.lang.String)](../../../connect/jdbc/reference/getbigdecimal-method-java-lang-string-sqlserverresultset.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.math.BigDecimal getBigDecimal(java.lang.String columnName,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *scale*  
  
 Um **int** que indica o número de dígitos à direita da vírgula decimal.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto BigDecimal.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método getBigDecimal é especificado pelo método getBigDecimal na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBigDecimal &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
