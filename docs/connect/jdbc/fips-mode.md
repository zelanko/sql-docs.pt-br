---
title: Modo FIPS no JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83ce3690d194b8b06fc79d58c2d7bc7efa996619
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293376"
---
# <a name="fips-mode"></a>Modo FIPS

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O Microsoft JDBC Driver para SQL Server é compatível com a execução nas JVMs configuradas para estar *em conformidade com o FIPS 140*.

#### <a name="prerequisites"></a>Pré-requisitos

- JVM configurada para FIPS
- Certificado TLS/SSL apropriado
- Arquivos de política apropriados
- Parâmetros de configuração apropriados

## <a name="fips-configured-jvm"></a>JVM configurada para FIPS

Em geral, os aplicativos podem configurar o arquivo `java.security` para usar provedores de criptografia em conformidade com FIPS. Confira a documentação específica para sua JVM para saber como configurar a conformidade com o FIPS 140.

Para ver os módulos aprovados para configuração de FIPS, veja [Módulos validados no programa de validação do módulo de criptografia](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules).

Os fornecedores podem ter algumas etapas adicionais para configurar uma JVM com FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificado SSL apropriado
Para se conectar ao SQL Server no modo FIPS, é necessário um certificado TLS/SSL válido. Instale ou importe-o no repositório de chaves do Java no computador cliente (JVM) em que o FIPS está habilitado.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Como importar o certificado SSL no Java keyStore
Para o FIPS, é mais provável que você precise importar o certificado (.cert) no formato PKCS ou específico do provedor.
Use o snippet a seguir para importar o certificado TLS/SSL e armazená-lo em um diretório de trabalho com o formato KeyStore apropriado. _TRUST\_STORE\_PASSWORD_ é sua senha para o Java KeyStore.

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

O exemplo a seguir está importando um certificado TLS/SSL do Azure no formato PKCS12 com o provedor BouncyCastle. O certificado é importado no diretório de trabalho chamado _MyTrustStore\_PKCS12_ usando o seguinte snippet:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>Arquivos de política apropriados
Para alguns provedores FIPS, são necessários jars de política irrestrita. Nesses casos, para Sun/Oracle, baixe os arquivos de política de jurisdição de força ilimitada do JCA (Java Cryptography Extension) para [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) ou [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parâmetros de configuração apropriados
Para executar o driver JDBC no modo em conformidade com FIPS, configure as propriedades de conexão, conforme mostrado na tabela a seguir. 

#### <a name="properties"></a>Propriedades 

|Propriedade|Type|Padrão|Descrição|Observações|
|---|---|---|---|---|
|encrypt|boolean ["true / false"]|"false"|Para a JVM habilitada para FIPS, essa propriedade de criptografia deve ser **true**||
|TrustServerCertificate|boolean ["true / false"]|"false"|Para o FIPS, o usuário precisa validar a cadeia de certificados, de modo que ele deve usar o valor **"false"** para essa propriedade. ||
|trustStore|String|nulo|O caminho do arquivo do repositório de chaves do Java em que você importou o certificado. Se você instalar o certificado em seu sistema, não será necessário aprovar nada. O driver usa arquivos cacerts ou jssecacerts.||
|trustStorePassword|String|nulo|A senha usada para verificar a integridade dos dados de trustStore.||
|fips|boolean ["true / false"]|"false"|Para a JVM habilitada para FIPS, essa propriedade deve ser **true**|Adicionada na versão 6.1.4 (versão estável 6.2.2)||
|fipsProvider|String|nulo|Provedor FIPS configurado na JVM. Por exemplo, BCFIPS ou SunPKCS11-NSS |Adicionada na versão 6.1.2 (versão estável 6.2.2), preterida na 6.4.0 – confira os detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|String|JKS|Para o modo FIPS, defina o tipo de repositório confiável, PKCS12 ou o tipo definido pelo provedor FIPS |Adicionada na versão 6.1.2 (versão estável 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
