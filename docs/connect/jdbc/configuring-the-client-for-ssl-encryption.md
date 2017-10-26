---
title: "Configuração do cliente para criptografia SSL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5c395fcd8ae12a91db5dcd7bf26f8d81589d2f6
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-the-client-for-ssl-encryption"></a>Configurando o cliente para criptografia SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ou o cliente precisa validar que o servidor é o servidor correto e seu certificado é emitido por uma autoridade de certificação que o cliente confia. Para validar o certificado do servidor, o material de confiança deve ser fornecido na hora da conexão. Além disso, o emissor do certificado do servidor deve ser uma autoridade de certificação em que o cliente confia.  
  
 Este tópico primeiro descreve como fornecer o material de confiança no computador cliente. Em seguida, o tópico descreve como importar um certificado do servidor para o repositório de confiança do computador cliente quando a instância do certificado de Protocolo SSL (SSL) do SQL Server é emitida por uma autoridade de certificação privada.  
  
 Para obter mais informações sobre como validar o certificado do servidor, consulte a seção de validação de certificado do servidor SSL em [Noções básicas sobre o suporte a SSL](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="configuring-the-client-trust-store"></a>Configurando o repositório de confiança do cliente  
 Validar o certificado do servidor requer que o material confiável deve ser fornecido no tempo de conexão usando **trustStore** e **trustStorePassword** propriedades de conexão explicitamente, ou usando o repositório de confiança padrão Java Máquina Virtual (da JVM subjacente) implicitamente. Para obter mais informações sobre como definir o **trustStore** e **trustStorePassword** propriedades em uma cadeia de caracteres de conexão, consulte [conectando com criptografia SSL](../../connect/jdbc/connecting-with-ssl-encryption.md).  
  
 Se o **trustStore** propriedade é não especificado ou definido como null, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] confiará no provedor de segurança da JVM subjacente, o Java Secure Socket Extension (SunJSSE). O provedor de SunJSSE fornece um padrão TrustManager, que é usado para validar certificados x. 509 retornados pelo SQL Server contra o material de confiança fornecido em um repositório de confiança.  
  
 TrustManager tenta localizar o trustStore padrão na seguinte ordem de pesquisa:  
  
-   Se a propriedade do sistema "javax.NET.SSL. truststore" for definida, o TrustManager tenta localizar o arquivo trustStore padrão usando o nome do arquivo especificado por essa propriedade do sistema.  
  
-   Se a propriedade do sistema "javax.NET.SSL. truststore" não foi especificada e se o arquivo "\<java-home >/lib/security/jssecacerts" existe, esse arquivo é usado.  
  
-   Se o arquivo "\<java-home >/lib/security/cacerts" existe, esse arquivo é usado.  
  
 Para obter mais informações, consulte a documentação da interface do SUNX509 TrustManager no site da Sun Microsystems.  
  
 O Java Runtime Environment permite definir as propriedades do sistema trustStore e trustStorePassword da seguinte maneira:  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 Neste caso, qualquer aplicativo que estiver executando nesta JVM usará estas configurações como padrão. Para substituir as configurações padrão do seu aplicativo, você deve definir o **trustStore** e **trustStorePassword** propriedades de conexão na cadeia de conexão ou no respectivo método setter a [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) classe.  
  
 Além disso, você pode configurar e gerenciar os arquivos de repositório de confiança padrão como "\<java-home >/lib/security/jssecacerts" e "\<java-home >/lib/security/cacerts". Para fazer isso, use o utilitário "keytool" de JAVA que é instalado com o JRE (Java Runtime Environment). Para obter mais informações sobre o utilitário "keytool", consulte documentação de keytool no site da Sun Microsystems.  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>Importando o certificado do servidor para repositório de confiança  
 Durante o handshake SSL, o servidor envia seu certificado de chave pública ao cliente. O emissor de um certificado de chave pública é conhecido como uma Autoridade de Certificação (CA). O cliente precisa garantir que a autoridade de certificação é de sua confiança. Isto é obtido sabendo a chave pública de CAs de confiança com antecedência. Normalmente, o JVM é enviado com um conjunto predefinido de autoridades de certificação de confiança.  
  
 Se a instância do certificado de Protocolo SSL (SSL) do SQL Server é emitida por uma autoridade de certificação privada, você deve adicionar o certificado da autoridade de certificação à lista de certificados confiáveis no repositório de confiança do computador cliente.  
  
 Para fazer isso, use o utilitário "keytool" de JAVA que é instalado com o JRE (Java Runtime Environment). O prompt de comando a seguir demonstra como usar o utilitário "keytool" para importar um certificado de um arquivo:  
  
```  
keytool -import -v -trustcacerts -alias myServer -file caCert.cer -keystore truststore.ks  
```  
  
 O exemplo usa um arquivo denominado "caCert.cer" como arquivo de certificado. Você deve obter este arquivo de certificado do servidor. As etapas seguintes explicam como exportar o certificado do servidor para um arquivo:  
  
1.  Clique em Iniciar e em Executar, e digite MMC. (MMC é um acrônimo para o Console de Gerenciamento Microsoft.)  
  
2.  Em MMC, abra os Certificados.  
  
3.  Expanda Pessoal e, em seguida, Certificados.  
  
4.  Clique com o botão direito no certificado do servidor e selecione Todas as Tarefas\Exportar.  
  
5.  Clique em Avançar para mover além da caixa de diálogo de boas-vindas do Assistente de Exportação de Certificado.  
  
6.  Confirme se "Não, não exportar a chave privada" está selecionada e clique em Avançar.  
  
7.  Verifique se X.509 binário codificado por DER (*.cer) ou X.509 codificado na base 64 (*.cer) está selecionado e clique em Avançar.  
  
8.  Insira um nome do arquivo de exportação.  
  
9. Clique em Avançar e em Concluir para exportar o certificado.  
  
## <a name="see-also"></a>Consulte também  
 [Usando a criptografia SSL](../../connect/jdbc/using-ssl-encryption.md)   
 [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  

