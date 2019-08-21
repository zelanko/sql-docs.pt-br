---
title: Modo FIPS no JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
manager: kenvh
ms.openlocfilehash: 63681ee474d4993e248bf02dcabd9065317ffa39
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028061"
---
# <a name="fips-mode"></a>Modo FIPS

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O Microsoft JDBC Driver para SQL Server dá suporte à execução no JVMs configurado para ser *compatível com FIPS 140*.

#### <a name="prerequisites"></a>Prerequisites

- JVM configurada por FIPS
- Certificado SSL apropriado
- Arquivos de política apropriados
- Parâmetros de configuração apropriados

## <a name="fips-configured-jvm"></a>JVM configurada por FIPS

Em geral, os aplicativos podem `java.security` configurar o arquivo para usar provedores de criptografia compatíveis com FIPS. Consulte a documentação específica para sua JVM para saber como configurar a conformidade com o FIPS 140.

Para ver os módulos aprovados para configuração de FIPS, consulte [módulos validados no programa de validação do módulo criptográfico](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules).

Os fornecedores podem ter algumas etapas adicionais para configurar uma JVM com FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificado SSL apropriado
Para se conectar ao SQL Server no modo FIPS, é necessário um certificado SSL válido. Instale ou importe-o para o repositório de chaves Java no computador cliente (JVM) em que o FIPS está habilitado.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importando o certificado SSL no repositório de chaves Java
Para o FIPS, é mais provável que você precise importar o certificado (. CERT) no formato PKCS ou específico do provedor.
Use o trecho a seguir para importar o certificado SSL e armazená-lo em um diretório de trabalho com o formato de repositório de chaves apropriado. _A\_senha\_do repositório de confiança_ é sua senha para o repositório de chaves Java.

```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```

O exemplo a seguir está importando um certificado SSL do Azure no formato PKCS12 com o provedor BouncyCastle. O certificado é importado no diretório de trabalho chamado _MyTrustStore\_PKCS12_ usando o seguinte trecho:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>Arquivos de política apropriados
Para alguns provedores FIPS, são necessários jars de política irrestrita. Nesses casos, para Sun/Oracle, baixe os arquivos de política de jurisdição de nível ilimitado JCE (Java Cryptography Extension) para o [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) ou o [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parâmetros de configuração apropriados
Para executar o driver JDBC no modo compatível com FIPS, configure as propriedades de conexão, conforme mostrado na tabela a seguir. 

#### <a name="properties"></a>Propriedades 

|Propriedade|Tipo|Padrão|Descrição|Observações|
|---|---|---|---|---|
|encrypt|boolean ["true / false"]|"false"|Para a propriedade de criptografia JVM habilitada para FIPS deve ser **verdadeira**||
|TrustServerCertificate|boolean ["true / false"]|"false"|Para o FIPS, o usuário precisa validar a cadeia de certificados, de modo que o usuário deve usar o valor **"false"** para essa propriedade. ||
|trustStore|Cadeia de caracteres|nulo|O caminho do arquivo do repositório de chaves Java em que você importou o certificado. Se você instalar o certificado em seu sistema, não será necessário passar nada. O driver usa arquivos cacerts ou jssecacerts.||
|trustStorePassword|Cadeia de caracteres|nulo|A senha usada para verificar a integridade dos dados de trustStore.||
|fips|boolean ["true / false"]|"false"|Para JVM habilitada para FIPS, essa propriedade deve ser **verdadeira**|Adicionado no 6.1.4 (versão estável 6.2.2)||
|fipsProvider|Cadeia de caracteres|nulo|Provedor FIPS configurado na JVM. Por exemplo, BCFIPS ou SunPKCS11-NSS |Adicionado em 6.1.2 (versão estável 6.2.2), preterido em 6.4.0-Veja os detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|Cadeia de caracteres|JKS|Para o modo FIPS, defina o tipo de repositório de confiança PKCS12 ou type definido pelo provedor FIPS |Adicionado no 6.1.2 (versão estável 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
