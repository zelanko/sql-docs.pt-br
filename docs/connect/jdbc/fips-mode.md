---
title: O modo FIPS | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.openlocfilehash: 792d843a2c11c7bde016aec513df9c8724b366b4
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278847"
---
# <a name="fips-mode"></a>Modo FIPS
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O Microsoft JDBC Driver para SQL Server dá suporte a *modo de conformidade do FIPS 140*. Para Oracle / Sun JVM, consulte o [modo de compatível com FIPS 140 para SunJSSE](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html) seção fornecida pela Oracle para configurar o FIPS para JVM habilitada. 

**Pré-requisitos**:
* FIPS configurado da JVM
* Certificado SSL apropriado.
* Arquivos de política apropriada. 
* Parâmetros de configuração apropriado. 


## <a name="fips-configured-jvm"></a>FIPS configurado da JVM

Para ver os módulos aprovados para a configuração de FIPS, veja a [validado FIPS 140-1 e os módulos criptográficos FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm). 

Os fornecedores podem ter algumas etapas adicionais para configurar o JVM com o FIPS.

### <a name="ensure-your-jvm-is-in-fips-mode"></a>Verifique se que sua JVM está no modo FIPS
Para garantir que sua JVM FIPS habilitada, execute o seguinte trecho: 

```java
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
```

## <a name="appropriate-ssl-certificate"></a>Certificado SSL apropriado
Para conectar o SQL Server no modo FIPS, é necessário um certificado SSL válido. Instale ou importe-o Store de chave Java na máquina do cliente (JVM) em que o FIPS está habilitada.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importando o certificado SSL no repositório de chaves Java
Para FIPS, provavelmente você precisará importar o certificado (CERT) para qualquer um dos PKCS ou em um formato específico do provedor. Use o trecho a seguir para importar o certificado SSL e armazená-lo em um diretório de trabalho com o formato apropriado do repositório de chaves. _TRUST_STORE_PASSWORD_ é sua senha do repositório de chaves Java. 

```java
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

```


O exemplo a seguir está importando um certificado de SSL do Azure no formato PKCS12 com BouncyCastle provedor. O certificado é importado no diretório de trabalho chamado _MyTrustStore_PKCS12_ usando o trecho a seguir:

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>Arquivos de política apropriada
Para alguns provedores de FIPS, irrestritos jars de política são necessários. Nesses casos, Sun / Oracle, baixar o Java Cryptography Extension (JCE) ilimitado força jurisdição arquivos da política para [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) ou [JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parâmetros de configuração apropriado
Para executar o JDBC Driver no modo compatível com FIPS, configure propriedades de conexão, conforme mostrado na tabela a seguir. 

**Propriedades**: 

|Propriedade|Tipo|Padrão|Descrição|Observações|
|---|---|---|---|---|
|encrypt|booliano ["true / false"]|"false"|Para FIPS habilitado JVM criptografar a propriedade deve ser **true**||
|TrustServerCertificate|booliano ["true / false"]|"false"|Para FIPS, o usuário precisa validar a cadeia de certificados, portanto, o usuário deve usar **"false"** valor para essa propriedade. ||
|trustStore|Cadeia de caracteres|nulo|Caminho do arquivo de repositório de chaves Java em que você importou o certificado. Se você instalar o certificado em seu sistema, não há necessidade de passar qualquer coisa. Driver usa cacerts ou jssecacerts arquivos.||
|trustStorePassword|String|nulo|A senha usada para verificar a integridade dos dados de trustStore.||
|fips|booliano ["true / false"]|"false"|Para FIPS habilitada da JVM para essa propriedade deve ser **true**|Adicionado no 6.1.4 (estável 6.2.2 de versão)||
|fipsProvider|Cadeia de caracteres|nulo|Provedor FIPS configurado na JVM. Por exemplo, BCFIPS ou SunPKCS11 NSS |Adicionado no 6.1.2 (estável 6.2.2 de versão), substituído no 6.4.0 - consulte os detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|Cadeia de caracteres|JKS|Para o tipo de repositório de confiança do conjunto de modo FIPS PKCS12 ou tipo definido pelo provedor FIPS |Adicionado no 6.1.2 (estável 6.2.2 de versão)||



  
