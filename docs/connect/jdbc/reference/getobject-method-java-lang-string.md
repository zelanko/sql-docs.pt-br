---
title: Método getObject (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a1e955ce-13db-4828-ad59-d9b6a8b2c6cc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e06642390b060164d0e7fba3a8584200e5bc4dd8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981136"
---
# <a name="getobject-method-javalangstring"></a>Método getObject (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto na linguagem de programação Java, considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **Object**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getObject é especificado pelo método getObject na interface java.sql.CallableStatement.  
  
 Esse método retornará o valor da coluna fornecida como um objeto Java. O tipo desse objeto será o tipo de objeto Java padrão correspondente ao tipo SQL da coluna, seguindo o mapeamento para tipos internos constante na especificação do JDBC. Se o valor for um SQL NULL, o driver retornará um Java nulo.  
  
 Esse método também pode ser usado para ler tipos de dados abstratos específicos do banco de dados. Na API do JDBC 2.0, o comportamento do método getObject é estendido para materializar dados de tipos definidos pelo usuário do SQL. Quando uma coluna contiver um valor estruturado ou distinto, o comportamento desse método será como se fosse uma chamada para `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`.  
  
 A partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0:  
  
-   Um valor de tipo **date** será retornado como um objeto java.sql.Date.  
  
-   Um valor de tipo **time** será retornado como um objeto java.sql.Time.  
  
-   Um valor de tipo **datetime2** será retornado como um objeto java.sql.Timestamp.  
  
-   Um valor de tipo **datetimeoffset** será retornado como um objeto microsoft.sql.DateTimeOffset.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getObject &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
