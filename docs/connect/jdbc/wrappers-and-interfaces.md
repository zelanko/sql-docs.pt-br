---
title: Wrappers e Interfaces | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7de6c4bb3e3bb28fefb5eba0fa52a5de8684fa6d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="wrappers-and-interfaces"></a>Wrappers e interfaces
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte a interfaces que permitem a você criar um proxy de uma classe, além de wrappers que permitem acessar extensões para a API do JDBC que são específicas para o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] por meio de uma interface de proxy.  
  
## <a name="wrappers"></a>Wrappers  
 O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte à interface Java.SQL. Essa interface fornece um mecanismo para acessar extensões para a API do JDBC que são específicos para o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] por meio de uma interface de proxy.  
  
 A interface Java.SQL define dois métodos: **isWrapperFor** e **unwrap**. O **isWrapperFor** método verifica se o objeto de entrada especificado implementa essa interface. O **unwrap** método retorna um objeto que implementa essa interface para permitir acesso a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos específicos.  
  
 **isWrapperFor** e **unwrap** métodos são expostos da seguinte maneira:  
  
-   [Método isWrapperFor &#40; SQLServerCallableStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)  
  
-   [decodificar método &#40; SQLServerCallableStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)  
  
-   [Método isWrapperFor &#40; SQLServerConnectionPoolDataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)  
  
-   [decodificar método &#40; SQLServerConnectionPoolDataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)  
  
-   [Método isWrapperFor &#40; SQLServerDataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)  
  
-   [decodificar método &#40; SQLServerDataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)  
  
-   [Método isWrapperFor &#40; SQLServerPreparedStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)  
  
-   [decodificar método &#40; SQLServerPreparedStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)  
  
-   [Método isWrapperFor &#40; SQLServerStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)  
  
-   [decodificar método &#40; SQLServerStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)  
  
-   [Método isWrapperFor &#40; SQLServerXADataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)  
  
-   [decodificar método &#40; SQLServerXADataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)  
  
## <a name="interfaces"></a>Interfaces  
 A partir do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0, as interfaces são disponibilizadas para um servidor de aplicativos acessar um método específico do driver da classe associada. O servidor de aplicativo pode encapsular a classe, criando um proxy, expondo a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-funcionalidade específica de uma interface. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte a interfaces que têm o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos específicos e constantes para um servidor de aplicativos pode criar um proxy da classe.  
  
 As interfaces derivam das interfaces Java padrão, você pode usar o mesmo objeto após o desencapsulamento para acessar a funcionalidade específica do driver ou genérico [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] funcionalidade.  
  
 As seguintes interfaces são adicionadas:  
  
-   [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)  
  
-   [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)  
  
-   [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)  
  
-   [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
-   [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
-   [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Description  
 Este exemplo demonstra como acessar um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-função específica de um objeto de fonte de dados. Essa classe de fonte de dados pode ter sido encapsulada por um servidor de aplicativos. Para acessar a função de específica do driver JDBC ou uma constante, você pode desencapsular a fonte de dados para uma interface ISQLServerDataSource e usar as funções declaradas na interface.  
  
### <a name="code"></a>Código  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

