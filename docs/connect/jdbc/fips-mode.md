---
title: Modo FIPS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
ms.assetid: ''
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.openlocfilehash: fb8e6d19ef4359ebc16ed1089561c23724d7a34b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="fips-mode"></a>Modo FIPS
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O Microsoft JDBC Driver para SQL Server dá suporte a *o modo compatível com FIPS 140*. Para Oracle / Sun JVM, consulte o [modo de compatível com FIPS 140 para SunJSSE](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html) seção fornecida pela Oracle para configurar FIPS habilitada JVM. 

**Pré-requisitos**:
* FIPS configurado da JVM
* Certificado SSL apropriado.
* Arquivos de política apropriada. 
* Parâmetros de configuração apropriado. 


## <a name="fips-configured-jvm"></a>FIPS configurado da JVM

Para ver os módulos aprovados para a configuração de FIPS, consulte o [validado FIPS 140-1 e os módulos de criptografia FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm). 

Os fornecedores podem ter algumas etapas adicionais para configurar o JVM com FIPS.

### <a name="ensure-your-jvm-is-in-fips-mode"></a>Certifique-se de que sua JVM está no modo FIPS
Para garantir que sua JVM é FIPS habilitada, execute o trecho a seguir: 

````
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
````

## <a name="appropriate-ssl-certificate"></a>Certificado SSL apropriado
Para conectar o SQL Server no modo FIPS, é necessário um certificado SSL válido. Instale ou importe-o repositório de chaves Java no computador cliente (JVM) onde FIPS está habilitado. Se você não importar / instalar o certificado apropriado, pode não ser capaz de se conectar ao SQL Server que não é possível estabelecer uma conexão segura.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importar o certificado SSL no armazenamento de chaves Java
Para FIPS, provavelmente você precisa importar o certificado (. cert na) para qualquer PKCS ou em um formato específico do provedor. Use o trecho a seguir para importar o certificado SSL e armazená-lo em um diretório de trabalho com o formato de armazenamento de chaves apropriado. _TRUST_STORE_PASSWORD_ é a senha para o armazenamento de chaves Java. 

````
    public void saveGenericKeyStore(String provider, String trustStoreType, String certName, String certPath) throws KeyStoreException, CertificateException, NoSuchAlgorithmException, NoSuchProviderException, IOException {
        KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
        FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
        ks.load(null, null);
        ks.setCertificateEntry(certName, getCertificate(certPath));
        ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
        os.flush();
        os.close();
    }

    private Certificate getCertificate(String pathName) throws FileNotFoundException, CertificateException {
        FileInputStream fis = new FileInputStream(pathName);
        CertificateFactory cf = CertificateFactory.getInstance("X.509");
        return cf.generateCertificate(fis);
    }

````


O exemplo a seguir é importar um certificado de SSL do Azure no formato PKCS12 com BouncyCastle provedor. O certificado foi importado no diretório de trabalho chamado _MyTrustStore_PKCS12_ usando o trecho a seguir:

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>Arquivos de política apropriada
Para alguns provedores de FIPS, irrestritos jars de política são necessários. Nesses casos, Sun / Oracle, baixar o Java Cryptography Extension (JCE) ilimitado força Policy Files para [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) ou [JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parâmetros de configuração apropriado
Para executar o Driver JDBC em modo compatível com FIPS, configure propriedades de conexão, conforme mostrado na tabela a seguir. 

**Propriedades**: 

|Propriedade|Tipo|Padrão|Description|Observações|
|---|---|---|---|---|
|encrypt|booliano ["true / false"]|"false"|Para FIPS habilitada JVM criptografar propriedade deve ser **true**||
|TrustServerCertificate|booliano ["true / false"]|"false"|Para FIPS, o usuário precisa validar a cadeia de certificados, então o usuário deve usar **"false"** valor para essa propriedade. ||
|trustStore|Cadeia de caracteres|nulo|O caminho de arquivo de armazenamento de chaves Java em que você importou o certificado. Se você instalar o certificado em seu sistema, em seguida, há necessidade de passar qualquer coisa. Driver usa cacerts ou jssecacerts arquivos.||
|trustStorePassword|String|nulo|A senha usada para verificar a integridade dos dados de trustStore.||
|FIPS|booliano ["true / false"]|"false"|Para fips habilitada JVM essa propriedade deve ser **true**|Adicionado no 6.1.4 (estável versão 6.2.2)||
|fipsProvider|Cadeia de caracteres|nulo|Provedor FIPS configurado na JVM. Por exemplo, BCFIPS ou SunPKCS11 NSS |Adicionado no 6.1.2 (estável versão 6.2.2), substituído no 6.4.0 - consulte os detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|Cadeia de caracteres|JKS|Para o tipo de repositório de confiança do conjunto de modo FIPS PKCS12 ou tipo definido pelo provedor FIPS |Adicionado no 6.1.2 (estável versão 6.2.2)||



  
