---
title: Método setObject (int, java.lang.Object, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d190ee20-d669-4c6f-a081-d5cfec2f72ca
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61e81b3eebdae47b2fd60d279a8ca1614d8e5267
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setobject-method-int-javalangobject-int-int"></a>Método setObject (int, java.lang.Object, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor do parâmetro designado usando o objeto fornecido, o tipo de destino e a escala.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setObject(int n,  
                            java.lang.Object obj,  
                            int targetSqlType,  
                            int scale)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *n*  
  
 Um **int** que indica o número do parâmetro.  
  
 *obj*  
  
 Um objeto.  
  
 *targetSqlType*  
  
 Um **int** que indica o tipo de destino, conforme definido no Types.  
  
 *scale*  
  
 Um **int** que indica o número de dígitos à direita da vírgula decimal. Esse parâmetro é ignorado para todos os tipos diferentes de NUMERIC e DECIMAL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setObject é especificado pelo método setObject na interface PreparedStatement.  
  
 Começando com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0, o comportamento desse método é modificado pelo **sendTimeAsDatetime** propriedade de conexão ([definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [ Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte [Java.SQL. time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Método setObject &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
