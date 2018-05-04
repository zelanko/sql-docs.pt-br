---
title: Conectar-se com a criptografia SSL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49c6aaf771bb5335b8ba649869a4a8cf13894e82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-with-ssl-encryption"></a>Conectando-se com criptografia SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Os exemplos neste tópico descrevem como usar propriedades de cadeia de conexão que permitem aos aplicativos usar criptografia de Protocolo SSL (Secure Sockets Layer) em um aplicativo Java. Para obter mais informações sobre esses conexão nova cadeia de caracteres propriedades como **criptografar**, **trustServerCertificate**, **trustStore**,  **trustStorePassword**, e **hostNameInCertificate**, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Quando o **criptografar** está definida como **true** e **trustServerCertificate** está definida como **true**, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não validará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] certificado SSL. Isso é geralmente necessário para permitir conexões em ambientes de teste, como onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância tem apenas um certificado autoassinado.  
  
 O exemplo de código a seguir demonstra como definir a **trustServerCertificate** propriedade em uma cadeia de caracteres de conexão:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 Quando o **criptografar** está definida como **true** e **trustServerCertificate** está definida como **false**, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] validará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] certificado SSL. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para validar o certificado do servidor, o material confiável deve ser fornecido em tempo de conexão usando **trustStore** e **trustStorePassword** propriedades de conexão, ou explicitamente, usando a máquina Virtual (JVM Java) subjacente do padrão de confiança armazenar implicitamente.  
  
 O **trustStore** propriedade especifica o caminho (incluindo o nome do arquivo) para o arquivo trustStore do certificado, que contém a lista de certificados que o cliente confia. O **trustStorePassword** propriedade especifica a senha usada para verificar a integridade dos dados de trustStore. Para obter mais informações sobre como usar o repositório de confiança padrão da JVM, consulte o [configuração do cliente para criptografia SSL](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md).  
  
 O exemplo de código a seguir demonstra como definir a **trustStore** e **trustStorePassword** propriedades em uma cadeia de caracteres de conexão:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 O Driver JDBC fornece uma propriedade adicional, **hostNameInCertificate**, que especifica o nome do host do servidor. O valor dessa propriedade deve corresponder à propriedade subject do certificado.  
  
 O exemplo de código a seguir demonstra como usar o **hostNameInCertificate** propriedade em uma cadeia de caracteres de conexão:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  Como alternativa, você pode definir o valor das propriedades de conexão usando a **setter** métodos fornecidos pelo [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) classe.  
  
 Se o **criptografar** está definida como **true** e **trustServerCertificate** está definida como **false** e se o nome do servidor no cadeia de caracteres de conexão não coincide com o nome do servidor no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] certificado SSL, o seguinte erro será emitido: O driver não foi possível estabelecer uma conexão segura para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando criptografia segura Sockets Layer (SSL). Erro: "java.security.cert.CertificateException: falha ao validar o nome do servidor em um certificado durante a inicialização do protocolo SSL."  
  
## <a name="see-also"></a>Consulte também  
 [Usando a criptografia SSL](../../connect/jdbc/using-ssl-encryption.md)   
 [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
