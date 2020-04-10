---
title: Método setObject (int, java.lang.Object, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d190ee20-d669-4c6f-a081-d5cfec2f72ca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01a7461c6f49f66304ff767038945da03a997298
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920874"
---
# <a name="setobject-method-int-javalangobject-int-int"></a>Método setObject (int, java.lang.Object, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor do parâmetro designado usando o objeto, o tipo de destino e a escala fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setObject(int n,  
                            java.lang.Object obj,  
                            int targetSqlType,  
                            int scale)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *n*  
  
 Um **int** que indica o número do parâmetro.  
  
 *obj*  
  
 Um objeto.  
  
 *targetSqlType*  
  
 Um **int** que indica o tipo de destino conforme definido em java.sql.Types.  
  
 *scale*  
  
 Um **int** que indica o número de dígitos à direita da vírgula decimal. Esse parâmetro é ignorado para todos os tipos diferentes de NUMERIC e DECIMAL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setObject é especificado pelo método setObject na interface java.sql.PreparedStatement.  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 e versões posteriores, o comportamento desse método foi modificado pela propriedade de conexão **sendTimeAsDatetime** ([Configuração das propriedades de conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para mais informações, confira [Como configurar a maneira como os valores de java.sql.Time são enviados ao servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método setObject &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
