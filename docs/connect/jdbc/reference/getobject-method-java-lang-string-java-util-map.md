---
title: Método getObject (Java, java.util.Map) | Microsoft Docs
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
- SQLServerCallableStatement.getObject (java.lang.String, Java.util.Map)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e174eb81-d569-479e-a171-365cd6d44b6a
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ef8e694e3d03f314f6985276218ee15dcf88e9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32837361"
---
# <a name="getobject-method-javalangstring-javautilmap"></a>Método getObject (java.lang.String, java.util.Map)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto na linguagem de programação Java fornecido o nome do parâmetro, usando o objeto de mapa fornecido.  
  
> [!NOTE]  
>  Esse método não é suportado atualmente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. O uso deste método sempre retornará o mapeamento padrão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol,  
                                  java.util.Map m)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *M*  
  
 Um objeto de mapa.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **objeto** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getObject é especificado pelo método na interface do CallableStatement getObject.  
  
 Esse método retornará o valor da coluna fornecida como um objeto Java. O tipo desse objeto será o tipo de objeto Java padrão correspondente ao tipo SQL da coluna, seguindo o mapeamento para tipos internos constante na especificação do JDBC. Se o valor for um SQL NULL, o driver retornará um Java nulo.  
  
 Esse método também pode ser usado para ler tipos de dados abstratos específicos do banco de dados. Na API do JDBC 2.0, o comportamento do método getObject é estendido para materializar dados de tipos definidos pelo usuário do SQL. Quando uma coluna contém um valor estruturado ou distinto, o comportamento desse método é como se fosse uma chamada para `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`.  
  
 A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0:  
  
-   Um valor do tipo **data** serão retornados como um objeto Java.SQL.  
  
-   Um valor do tipo **tempo** serão retornados como um objeto Java.SQL. time.  
  
-   Um valor do tipo **datetime2** serão retornados como um objeto Java.SQL. timestamp.  
  
-   Um valor do tipo **datetimeoffset** serão retornados como um objeto Microsoft.SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Método getObject &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
