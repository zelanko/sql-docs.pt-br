---
title: Conectar-se com criptografia SSL | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78cdeb64cbd0bc76109c7bd3db784c2262ae80ff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812184"
---
# <a name="connecting-with-ssl-encryption"></a>Conectando-se com criptografia SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Os exemplos deste artigo descrevem como usar propriedades de cadeia de conexão que permitem aos aplicativos usar a criptografia de protocolo SSL em um aplicativo Java. Para obter mais informações sobre essas novas propriedades de cadeia de conexão, como **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword** e **hostNameInCertificate**, veja [Definindo as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Quando a propriedade **encrypt** estiver definida como **true** e a propriedade **trustServerCertificate** estiver definida como **true**, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não validará o certificado SSL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso costuma ser obrigatório para permitir conexões em ambientes de teste, como naqueles em que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem apenas um certificado autoassinado.  
  
 O seguinte exemplo de código demonstra como definir a propriedade **trustServerCertificate** em uma cadeia de conexão:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 Quando a propriedade **encrypt** estiver definida como **true** e a propriedade **trustServerCertificate** estiver definida como **false**, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] validará o certificado SSL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para validar o certificado do servidor, o material de confiança precisa ser fornecido no tempo de conexão usando as propriedades de conexão **trustStore** e **trustStorePassword** explicitamente ou usando o repositório de confiança padrão da JVM (Máquina Virtual Java) subjacente.  
  
 A propriedade **trustStore** especifica o caminho (incluindo o nome de arquivo) para o arquivo trustStore do certificado, que contém a lista de certificados na qual o cliente confia. A propriedade **trustStorePassword** especifica a senha usada para verificar a integridade dos dados de trustStore. Para obter mais informações sobre como usar o repositório de confiança padrão da JVM, consulte o [Configurando o cliente para criptografia SSL](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md).  
  
 O seguinte exemplo de código demonstra como definir as propriedades **trustStore** e **trustStorePassword** em uma cadeia de conexão:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 O JDBC Driver fornece uma propriedade adicional, **hostNameInCertificate**, que especifica o nome do host do servidor. O valor dessa propriedade deve corresponder à propriedade subject do certificado.  
  
 O seguinte exemplo de código demonstra como usar a propriedade **hostNameInCertificate** em uma cadeia de conexão:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  Como alternativa, você pode definir o valor das propriedades de conexão usando os métodos **setter** apropriados fornecidos pela classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
 Se a propriedade **encrypt** estiver definida como **true** e a propriedade **trustServerCertificate** estiver definida como **false**, e o nome do servidor na cadeia de conexão não corresponder ao nome do servidor no certificado SSL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o seguinte erro será emitido: o driver não conseguiu estabelecer uma conexão segura com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a criptografia do protocolo SSL. Erro: "java.security.cert.CertificateException: falha ao validar o nome do servidor em um certificado durante a inicialização do protocolo SSL."  
  
## <a name="see-also"></a>Consulte Também  
 [Usando criptografia SSL](../../connect/jdbc/using-ssl-encryption.md)   
 [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
