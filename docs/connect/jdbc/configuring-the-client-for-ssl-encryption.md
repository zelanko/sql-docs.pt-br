---
title: Como configurar o cliente para criptografia | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0327a4321b141f0433cd9c6c9554c5a48f7381fb
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922485"
---
# <a name="configuring-the-client-for-encryption"></a>Configurando o cliente para criptografia
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ou o cliente precisa validar se o servidor é o correto e se seu certificado é emitido por uma autoridade de certificação de confiança do cliente. Para validar o certificado do servidor, o material de confiança deve ser fornecido na hora da conexão. Além disso, o emissor do certificado do servidor deve ser uma autoridade de certificação em que o cliente confia.  
  
 Este tópico primeiro descreve como fornecer o material de confiança no computador cliente. Em seguida, o tópico descreve como importar um certificado do servidor para o repositório de confiança do computador cliente quando a instância do certificado de protocolo TLS do SQL Server é emitida por uma autoridade de certificação privada.  
  
 Para obter mais informações sobre como validar o certificado do servidor, confira a seção Validando o certificado TLS do servidor em [Noções básicas sobre suporte à criptografia](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="configuring-the-client-trust-store"></a>Configurando o repositório de confiança do cliente 
 Validar o certificado do servidor exige que o material confiável seja fornecido no momento da conexão usando-se as propriedades de conexão **trustStore** e **trustStorePassword** explicitamente ou o armazenamento de confiança padrão da JVM (Máquina Virtual Java) subjacente implicitamente. Para obter mais informações sobre como definir as propriedades **trustStore** e **trustStorePassword** na cadeia de conexão, confira [Conectando-se com criptografia](../../connect/jdbc/connecting-with-ssl-encryption.md).  
  
 Se a propriedade **trustStore** não for especificada ou estiver definida como nula, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] confiará no provedor de segurança da JVM subjacente, o Java Secure Socket Extension (SunJSSE). O provedor de SunJSSE fornece um TrustManager padrão que é usado para validar certificados de X.509 retornados pelo SQL Server em relação ao material de confiança fornecido em um repositório de confiança.  
  
 O TrustManager tenta localizar o trustStore padrão na seguinte ordem de pesquisa:  
  
-   Se a propriedade do sistema "javax.net.ssl.trustStore" for definida, o TrustManager tentará localizar o arquivo trustStore padrão usando o nome de arquivo especificado por aquela propriedade de sistema.  
  
-   Se a propriedade do sistema "javax.net.ssl.trustStore" não foi especificada, e se o arquivo "\<java-home>/lib/security/jssecacerts" existe, esse arquivo é usado.  
  
-   Se o arquivo "\<java-home>/lib/security/cacerts" existe, esse arquivo é usado.  
  
 Para obter mais informações, consulte a documentação da interface do SUNX509 TrustManager no site da Sun Microsystems.  
  
 O Java Runtime Environment permite definir as propriedades do sistema trustStore e trustStorePassword da seguinte maneira:  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 Neste caso, qualquer aplicativo que estiver executando nesta JVM usará estas configurações como padrão. Para anular as configurações padrão em seu aplicativo, você deverá definir as propriedades de conexão **trustStore** e **trustStorePassword** na cadeia de conexão ou no método setter apropriado da classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
 Além disso, você pode configurar e gerenciar os arquivos de repositório de confiança padrão como "\<java-home>/lib/security/jssecacerts" e "\<java-home>/lib/security/cacerts". Para fazer isso, use o utilitário "keytool" de JAVA que é instalado com o JRE (Java Runtime Environment). Para obter mais informações sobre o utilitário "keytool", consulte documentação de keytool no site da Sun Microsystems.  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>Importando o certificado do servidor para o repositório de confiança  
 Durante o handshake TLS, o servidor envia seu certificado de chave pública ao cliente. O emissor de um certificado de chave pública é conhecido como uma Autoridade de Certificação (CA). O cliente precisa garantir que a autoridade de certificação é de sua confiança. Isto é obtido sabendo a chave pública de CAs de confiança com antecedência. Normalmente, o JVM é enviado com um conjunto predefinido de autoridades de certificação de confiança.  
  
 Se a instância do certificado de protocolo TLS do SQL Server for emitida por uma autoridade de certificação privada, você deverá adicionar o certificado da autoridade de certificação à lista de certificados confiáveis no repositório de confiança do computador cliente.  
  
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
  
## <a name="see-also"></a>Confira também  
 [Usando criptografia](../../connect/jdbc/using-ssl-encryption.md)   
 [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)