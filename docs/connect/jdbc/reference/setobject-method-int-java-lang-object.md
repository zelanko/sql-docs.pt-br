---
title: Método setObject (int, java.lang.Object) | Microsoft Docs
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
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cac0013c8867bce46dc9fd8ebbae9d0b0c487259
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783976"
---
# <a name="setobject-method-int-javalangobject"></a>Método setObject (int, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor do parâmetro designado usando o objeto fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setObject(int index,  
                            java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica o número do parâmetro.  
  
 *obj*  
  
 Um objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setObject é especificado pelo método setObject na interface do PreparedStatement.  
  
 Antes de chamar o método setObject, o aplicativo pode definir o parâmetro especificado usando um dos métodos a seguir:  
  
-   Os métodos set\<Type> da classe SQLServerPreparedStatement e da classe SQLServerCallableStatement  
  
-   Os métodos setNull da classe SQLServerPreparedStatement e da classe SQLServerCallableStatement  
  
-   O [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) método da classe SQLServerCallableStatement  
  
 Em todos os casos, o tipo do parâmetro é definido automaticamente. Se o aplicativo chamar o método setObject com um valor obj NULL, o driver suporá que o tipo do parâmetro é definido pelo método chamado anteriormente.  
  
 Se o valor obj for NULL e nenhuma informação de tipo para esse parâmetro puder ser determinada, o método setObject converterá o parâmetro especificado em um CHAR antes de enviá-lo ao banco de dados.  
  
 Começando com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0, o comportamento desse método é modificado pela **sendTimeAsDatetime** propriedade de conexão ([definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md)) e [ Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obter mais informações, consulte [time configurando como os valores são enviados para o servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método setObject &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
