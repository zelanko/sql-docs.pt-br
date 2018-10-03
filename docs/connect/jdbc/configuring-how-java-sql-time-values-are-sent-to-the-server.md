---
title: Configurando como os valores java.sql.Time são enviados ao servidor | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3afc4fc8a74dfe4c2ed625fc7a82df02dc21af3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850465"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurando como os valores de java.sql.Time são enviados ao servidor
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
  
 Versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] não há suporte para o **tempo** tipo de dados, portanto, os aplicativos usando o time geralmente armazenam time valores como **datetime** ou **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.  
  
 Se você quiser usar o **datetime** e **smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados ao trabalhar com os valores time, você deve definir o **sendTimeAsDatetime** propriedade de conexão para **verdadeira**. Se você quiser usar o **tempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados quando trabalhar com os valores time, você deve definir a **sendTimeAsDatetime** propriedade de conexão para **false**.  
  
 Esteja ciente de que, ao enviar valores java.sql.Time para um parâmetro cujo tipo de dados também pode armazenar a data, as datas padrão serão diferentes dependendo de se o valor java.sql.Time é enviado como um valor **datetime** (1/1/1970) ou **time** (1/1/1900). Para obter mais informações sobre conversões de dados ao enviar dados para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [Usando dados de data e hora](http://go.microsoft.com/fwlink/?LinkID=145211).  
  
 Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0, **sendTimeAsDatetime** é true por padrão. Em uma futura versão, a propriedade de conexão **sendTimeAsDatetime** poderá ser definida como falso por padrão.  
  
 Para garantir que o aplicativo continue funcionando conforme esperado, independentemente do valor padrão da propriedade de conexão **sendTimeAsDatetime**, você pode:  
  
-   Usar java.sql.Time ao trabalhar com o tipo de dados **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar timestamp ao trabalhar com o **datetime**, **smalldatetime**, e **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados.  
  
SendTimeAsDatetime deve ser false para colunas criptografadas como colunas criptografadas não dão suporte a conversão de tempo para a data e hora. Começando com o Microsoft JDBC Driver 6.0 para SQL Server, a classe SQLServerConnection tem dois métodos a seguir para definir/obter o valor da propriedade sendTimeAsDatetime.

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
