---
title: Dependências de recurso do Microsoft JDBC Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/06/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26402f5b15fa7dd8e24b13f3adc41836ff275228
ms.sourcegitcommit: c61c7b598aa61faa34cd802697adf3a224aa7dc4
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56154681"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Dependências de recurso do Microsoft JDBC Driver para SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo lista as bibliotecas que depende do Microsoft JDBC Driver para SQL Server. O projeto tem as seguintes dependências.

## <a name="compile-time"></a>Tempo de compilação

 - `com.microsoft.azure:azure-keyvault` : O azure Key Vault Provider para o recurso sempre criptografado do Azure Key Vault (opcional)
 - `com.microsoft.azure:azure-keyvault-webkey` : O azure Key Vault Provider para o recurso sempre criptografado do Azure Key Vault (opcional)
 - `com.microsoft.azure:adal4j` : O azure Active Directory Library para Java para o recurso de autenticação do Azure Active Directory e o recurso de Cofre de chaves do Azure (opcional)
 - `com.microsoft.rest:client-runtime` : O azure Active Directory Library para Java para o recurso de autenticação do Azure Active Directory e o recurso de Cofre de chaves do Azure (opcional)
- `org.osgi:org.osgi.core`: Biblioteca de núcleo OSGi para suporte OSGi Framework.
- `org.osgi:org.osgi.compendium`: Biblioteca Compêndio OSGi suporte OSGi Framework.

## <a name="test-time"></a>Tempo de teste

Projetos específicos que exigem qualquer um dos recursos anteriores precisam declarar explicitamente as respectivas dependências em seu arquivo POM.

**Por exemplo:** quando você estiver usando o recurso de autenticação do Active Directory do Azure, você precisa declarar novamente o `adal4j` dependência no arquivo POM do seu projeto. Consulte o trecho a seguir:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>
```

**Por exemplo:** quando você estiver usando o recurso do Azure Key Vault, você precisa declarar novamente o `azure-keyvault` dependência e o `adal4j` dependência no arquivo POM do seu projeto. Consulte o trecho a seguir:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault-webkey</artifactId>
    <version>1.2.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisitos de dependência do JDBC Driver

### <a name="working-with-the-azure-key-vault-provider"></a>Trabalhando com o provedor do Azure Key Vault:

- Driver JDBC versão 7.2.1 - versões de dependência: Azure-Keyvault (versão 1.2.0), o Azure-Keyvault-Webkey (versão 1.2.0), o Adal4j (versão 1.6.3), cliente-tempo de execução-para-AutoRest (1.6.5) e suas dependências ([doaplicativodeexemplo](../../connect/jdbc/azure-key-vault-sample.md))
- Driver JDBC versão 7.0.0 - versões de dependência: Azure-Keyvault (versão 1.0.0), o Adal4j (versão 1.6.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample.md))
- JDBC Driver versão 6.4.0 - versões de dependência: Azure-Keyvault (versão 1.0.0), o Adal4j (versão 1.4.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Driver JDBC versão 6.2.2 - versões de dependência: Azure-Keyvault (versão 1.0.0), o Adal4j (versão 1.4.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Driver JDBC versão 6.0.0 - versões de dependência: Azure-Keyvault (versão 0.9.7), o Adal4j (versão 1.3.0) e suas dependências ( [aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> Nas versões de driver 6.2.2 e 6.4.0, a dependência do azure-keyvault-java foi atualizada para a versão 1.0.0. No entanto, a nova versão não era compatível com a versão anterior (0.9.7) e interrompe a implementação existente no driver. A nova implementação no driver necessárias alterações na API, que por sua vez quebra programas cliente que usam o provedor do Cofre de chaves do Azure.
>
> Esse problema é resolvido com a versão mais recente do driver (7.0.0). O construtor removido que usado o mecanismo de retorno de chamada de autenticação é adicionado para o Azure Key Vault Provider para compatibilidade com versões anteriores.

### <a name="working-with-azure-active-directory-authentication"></a>Trabalhando com a Autenticação do Azure Active Directory:

- Driver JDBC versão 7.2.1 - versões de dependência: Adal4j (versão 1.6.3), cliente-tempo de execução-para-AutoRest (1.6.5) e suas dependências
- Driver JDBC versão 7.0.0 - versões de dependência: Adal4j (versão 1.6.0) e suas dependências
- JDBC Driver versão 6.4.0 - versões de dependência: Adal4j (versão 1.4.0) e suas dependências
- Driver JDBC versão 6.2.2 - versões de dependência: Adal4j (versão 1.4.0) e suas dependências
- Driver JDBC versão 6.0.0 - versões de dependência: Adal4j (versão 1.3.0) e suas dependências. Nesta versão do driver, você pode se conectar usando _ActiveDirectoryIntegrated_ somente em um sistema de operacional Windows e por meio de sqljdbc_auth e Active Directory Authentication Library para SQL Server (de modo de autenticação ADALSQL. DLL).

Da versão do driver 6.4.0 em diante, aplicativos não exigem necessariamente usando ADALSQL. DLL em sistemas de operacionais do Windows. Para *sistemas operacionais de não-Windows*, o driver requer um tíquete Kerberos para trabalhar com autenticação ActiveDirectoryIntegrated. Para obter mais informações sobre como se conectar ao Active Directory usando o Kerberos, consulte [tíquete Kerberos definido no Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac).

Para *os sistemas operacionais Windows*, o driver procurará sqljdbc_auth por padrão e não exige a instalação do tíquete Kerberos ou dependências de biblioteca do Azure. Se sqljdbc_auth não estiver disponível, o driver procurará o tíquete Kerberos para autenticação no Active Directory como em outros sistemas operacionais.

Você pode obter um [aplicativo de exemplo](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) que usa esse recurso.

## <a name="see-also"></a>Confira também

[Repositório GitHub do Driver JDBC](https://github.com/microsoft/mssql-jdbc)  
 [Referência de API do JDBC Driver](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
