---
title: Método getReference (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b35f7ea76e51327bd6e4605fad28aa5f29e79b16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getreference-method-sqlserverdatasource"></a>Método getReference (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna uma referência a este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de referência.  
  
## <a name="remarks"></a>Remarks  
 Esse método getReference é especificado pelo método getReference na interface javax.  
  
 Antes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0, se Settruststorepassword fosse chamado em um objeto SQLServerDataSource, a senha estaria presente no objeto retornado pelo sqlserverdatasource. Getreference, permitindo que o objeto a ser usado para fazer conexões adicionais. No JDBC Driver 3.0, será necessário definir a senha no objeto retornado pelo SQLServerDataSource.getReference antes de fazer conexões com o objeto.  
  
 Além disso, se definir SQLServerDataSource.setTrustStorePassword antes de associar as propriedades de fonte de dados, você deverá chamar SQLServerDataSource.setTrustStorePassword antes de estabelecer a conexão. Por exemplo,  
  
```  
ctx = new InitialContext(System.getProperties());  
  
SQLServerDataSource ds1 = (SQLServerDataSource) ctx.lookup(jndiName);  
  
ds1.setTrustStorePassword("XXXXX");  
Connection con = ds1.getConnection("user", "XXXXXX");  
  
ctx.rebind(jndiName, ds1);  
SQLServerDataSource ds2 = (SQLServerDataSource) ctx.lookup(jndiName);  
ds2.setTrustStorePassword("XXXXX");   // reset the truststore password  
con = ds2.getConnection("user", "XXXXXX");   // provide userid and password again  
```  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
