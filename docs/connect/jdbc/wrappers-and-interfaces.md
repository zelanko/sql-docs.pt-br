---
title: Wrappers e interfaces | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7be51a27364107afe6b79ebcce5de109909b1836
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916062"
---
# <a name="wrappers-and-interfaces"></a>Wrappers e interfaces

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é compatível com interfaces que permitem criar um proxy de uma classe, além de wrappers que permitem acessar extensões para a API do JDBC específicas do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] por meio de uma interface de proxy.

## <a name="wrappers"></a>Wrappers

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte à interface java.sql.Wrapper. Essa interface fornece um mecanismo para acessar extensões para a API do JDBC que são específicas do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] por meio de uma interface de proxy.

A interface java. Sql. Wrapper define dois métodos: **isWrapperFor** e **Unwrap**. O método **isWrapperFor** verifica se o objeto de entrada especificado implementa essa interface. O método **unwrap** retorna um objeto que implementa essa interface para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

os métodos **isWrapperFor** e **Unwrap** são expostos da seguinte maneira:

- [Método isWrapperFor &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)

- [Método unwrap &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)

- [Método isWrapperFor &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)

- [Método unwrap &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)

- [Método isWrapperFor &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)

- [desencapsular &#40;o método SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)

- [Método isWrapperFor &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)

- [Método unwrap &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)

- [Método isWrapperFor &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)

- [desencapsular &#40;o método SQLServerStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)

- [Método isWrapperFor &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)

- [desencapsular &#40;o método SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)

## <a name="interfaces"></a>Interfaces

Começando com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0, as interfaces são disponibilizadas para um servidor de aplicativos para acessar um método específico de driver usando a classe associada. O servidor de aplicativos pode encapsular a classe criando um proxy, expondo a funcionalidade específica do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] de uma interface. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é compatível com interfaces que têm os métodos específicos e constantes do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para que um servidor de aplicativos possa criar um proxy da classe.

Como as interfaces derivam das interfaces Java padrão, você pode usar o mesmo objeto após o desencapsulamento para acessar a funcionalidade específica do driver ou a funcionalidade genérica do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

As seguintes interfaces são adicionadas:

- [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)

- [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)

- [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)

- [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)

- [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)

- [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)

## <a name="example"></a>Exemplo

### <a name="description"></a>Descrição

Esse exemplo demonstra como acessar uma função específica do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usando um objeto DataSource. Essa classe DataSource pode ter sido encapsulada por um servidor de aplicativos. Para acessar a função específica ou a constante do JDBC Driver, é possível desencapsular a fonte de dados em uma interface ISQLServerDataSource e usar as funções declaradas na interface.

### <a name="code"></a>Código

```java
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  

public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  

   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  

         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  

      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```

## <a name="see-also"></a>Consulte Também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
