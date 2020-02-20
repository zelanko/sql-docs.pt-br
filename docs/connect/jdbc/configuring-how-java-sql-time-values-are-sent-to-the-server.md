---
title: Configurando como os valores java.sql.Time são enviados ao servidor | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fe6969d51834d0798a530b9cc9926af1b27fec2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028236"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configuração de como os valores de java.sql.Time são enviados ao servidor
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Se você usar um objeto java.sql.Time ou o tipo java.sql.Types.TIME do JDBC para definir um parâmetro, poderá configurar como o valor java.sql.Time é enviado ao servidor; como um tipo **time** ou um tipo **datetime** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esse cenário se aplica ao usar um dos seguintes métodos:  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 Configure como o valor java.sql.Time é enviado usando a propriedade de conexão **sendTimeAsDatetime**. Para obter mais informações, veja [Configuração das propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Você pode modificar de forma programática o valor da propriedade de conexão **sendTimeAsDatetime** com [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 As versões de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores à [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] não dão suporte o tipo de dados **time**. Dessa forma, os aplicativos que utilizam o java.sql.Time geralmente armazenam os valores de java.sql.Time como tipos de dados **datetime** ou **smalldatetime** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se quiser usar os tipos de dados **datetime** e **smalldatetime**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao trabalhar com valores java.sql.Time values, você deverá definir a propriedade de conexão **sendTimeAsDatetime** como **true**. Se quiser usar o tipo de dados **time** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao trabalhar com valores java.sql.Time, você deverá definir a propriedade de conexão **sendTimeAsDatetime** para **false**.  
  
 Esteja ciente de que, ao enviar valores java.sql.Time para um parâmetro cujo tipo de dados também pode armazenar a data, as datas padrão serão diferentes dependendo de se o valor java.sql.Time é enviado como um valor **datetime** (1/1/1970) ou **time** (1/1/1900). Para obter mais informações sobre conversões de dados ao enviar dados para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [Usando dados de data e hora](https://go.microsoft.com/fwlink/?LinkID=145211).  
  
 No JDBC Driver 3.0 do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **sendTimeAsDatetime** é true por padrão. Em uma futura versão, a propriedade de conexão **sendTimeAsDatetime** poderá ser definida como falso por padrão.  
  
 Para garantir que o aplicativo continue funcionando conforme esperado, independentemente do valor padrão da propriedade de conexão **sendTimeAsDatetime**, você pode:  
  
-   Usar java.sql.Time ao trabalhar com o tipo de dados **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Use java.sql.Timestamp ao trabalhar com os tipos de dados **datetime**, **smalldatetime** e **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
SendTimeAsDatetime precisa ser false para colunas criptografadas, pois as colunas criptografadas não dão suporte à conversão de time em datetime. No Microsoft JDBC Driver 6.0 para SQL Server e versões posteriores, a classe SQLServerConnection tem os dois métodos a seguir para definir/obter o valor da propriedade sendTimeAsDatetime.

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Confira também
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
