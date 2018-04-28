---
title: Configurar como os valores são enviados ao servidor | Microsoft Docs
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
ms.topic: article
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4550251e0b768c3be17b6efbbac43f8b6618dcf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurando como os valores de java.sql.Time são enviados ao servidor
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Se você usar um objeto Java.SQL. time ou o tipo JDBC Types. time para definir um parâmetro, você pode configurar como o valor de Java.SQL. time será enviado ao servidor. como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tempo** tipo ou como um **datetime** tipo.  
  
 Esse cenário se aplica ao usar um dos seguintes métodos:  
  
-   [SQLServerCallableStatement.registerOutParameter (int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter (int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 Você pode configurar como o valor de Java.SQL. time será enviado usando o **sendTimeAsDatetime** propriedade de conexão. Para obter mais informações, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Você pode modificar programaticamente o valor de **sendTimeAsDatetime** propriedade de conexão com [Setsendtimeasdatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] anteriores [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] não dão suporte a **tempo** valores de tipo de dados, para aplicativos que utilizam o Java.SQL. time geralmente armazenam Java.SQL. time como **datetime** ou **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados.  
  
 Se você quiser usar o **datetime** e **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados ao trabalhar com os valores, você deve definir o **sendTimeAsDatetime** propriedade de conexão para **true**. Se você quiser usar o **tempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de tipo de dados quando trabalhar com os valores, você deve definir o **sendTimeAsDatetime** propriedade de conexão para **false**.  
  
 Lembre-se de que ao enviar valores Java.SQL. time para um parâmetro cujo tipo de dados também pode armazenar a data, as datas padrão serão diferentes dependendo se o valor de Java.SQL. Time for enviado como um **datetime** (1/1/1970) ou **tempo** valor (1/1/1900). Para obter mais informações sobre conversões de dados ao enviar dados para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [usando dados de data e hora](http://go.microsoft.com/fwlink/?LinkID=145211).  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0, **sendTimeAsDatetime** é verdadeiro por padrão. Em uma versão futura, a **sendTimeAsDatetime** propriedade de conexão pode ser definida como false por padrão.  
  
 Para garantir que seu aplicativo continue a funcionar como esperado, independentemente do valor padrão de **sendTimeAsDatetime** propriedade de conexão, você pode:  
  
-   Use o Java.SQL. time ao trabalhar com o **tempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados.  
  
-   Use o Java.SQL. timestamp ao trabalhar com o **datetime**, **smalldatetime**, e **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados.  
  
Observe que sendTimeAsDatetime deve ser false para colunas criptografadas, como colunas criptografadas não dão suporte a conversão de tempo para datetime. Começando com o Microsoft JDBC Driver 6.0 para SQL Server, a classe SQLServerConnection tem dois métodos a seguir para definir/obter o valor da propriedade sendTimeAsDatetime.

```
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
