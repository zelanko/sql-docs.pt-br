---
title: Modo FIPS em JDBC | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: craigg
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: kenvh
ms.openlocfilehash: d710bb6e83d6f9761f7926afac3280a2c33d2bec
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822237"
---
# <a name="fips-mode"></a>Modo FIPS

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O Microsoft JDBC Driver para SQL Server dá suporte à execução em JVMs configurados para serem *compatível com FIPS 140*.

#### <a name="prerequisites"></a>Prerequisites

- FIPS configurado da JVM
- Certificado SSL apropriado
- Arquivos de política apropriada
- Parâmetros de configuração apropriado

## <a name="fips-configured-jvm"></a>FIPS configurado da JVM

Em geral, os aplicativos podem definir o `java.security` arquivo usar provedores de criptografia compatíveis com FIPS. Consulte a documentação específica para sua JVM para saber como configurar a conformidade do FIPS 140.

Para ver os módulos aprovados para a configuração de FIPS, veja [módulos validados no programa de validação do módulo criptográfico](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules).

Os fornecedores podem ter algumas etapas adicionais para configurar uma JVM com o FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificado SSL apropriado
Para se conectar ao SQL Server no modo FIPS, é necessário um certificado SSL válido. Instale ou importá-lo para a chave de Store Java no computador cliente (JVM) em que o FIPS está habilitada.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importando o certificado SSL no repositório de chaves Java
Para FIPS, provavelmente você precisará importar o certificado (CERT) em um formato específico do provedor ou PKCS.
Use o trecho a seguir para importar o certificado SSL e armazená-lo em um diretório de trabalho com o formato apropriado do repositório de chaves. _CONFIAR\_STORE\_senha_ é sua senha do repositório de chaves Java.

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

O exemplo a seguir está importando um certificado de SSL do Azure no formato PKCS12 com o provedor de BouncyCastle. O certificado é importado no diretório de trabalho chamado _MyTrustStore\_PKCS12_ usando o trecho a seguir:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>Arquivos de política apropriada
Para alguns provedores de FIPS, irrestritos jars de política são necessários. Nesses casos, Sun / Oracle, baixar o Java Cryptography Extension (JCE) ilimitado força jurisdição arquivos da política para [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) ou [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parâmetros de configuração apropriado
Para executar o JDBC Driver no modo compatível com FIPS, configure propriedades de conexão, conforme mostrado na tabela a seguir. 

#### <a name="properties"></a>Propriedades 

|Propriedade|Tipo|Padrão|Descrição|Observações|
|---|---|---|---|---|
|encrypt|boolean ["true / false"]|"false"|Para FIPS habilitado JVM criptografar a propriedade deve ser **true**||
|TrustServerCertificate|boolean ["true / false"]|"false"|Para FIPS, o usuário precisa validar a cadeia de certificados, portanto, o usuário deve usar **"false"** valor para essa propriedade. ||
|trustStore|Cadeia de caracteres|nulo|Caminho do arquivo de repositório de chaves Java em que você importou o certificado. Se você instalar o certificado em seu sistema, não há necessidade de passar qualquer coisa. Driver usa cacerts ou jssecacerts arquivos.||
|trustStorePassword|Cadeia de caracteres|nulo|A senha usada para verificar a integridade dos dados de trustStore.||
|fips|boolean ["true / false"]|"false"|Para FIPS habilitada da JVM para essa propriedade deve ser **true**|Adicionado no 6.1.4 (estável 6.2.2 de versão)||
|fipsProvider|Cadeia de caracteres|nulo|Provedor FIPS configurado na JVM. Por exemplo, BCFIPS ou SunPKCS11 NSS |Adicionado no 6.1.2 (estável 6.2.2 de versão), substituído no 6.4.0 - consulte os detalhes [aqui](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|Cadeia de caracteres|JKS|Para o tipo de repositório de confiança do conjunto de modo FIPS PKCS12 ou tipo definido pelo provedor FIPS |Adicionado no 6.1.2 (estável 6.2.2 de versão)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
