---
title: Dependências de recurso do Microsoft JDBC Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bf49c4264b89b6a47f083eec3654a757c1dce6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956590"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Dependências de recurso do Microsoft JDBC Driver para SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo lista as bibliotecas das quais o Microsoft JDBC Driver para SQL Server depende. O projeto tem as seguintes dependências.

## <a name="compile-time"></a>Tempo de compilação

 - `com.microsoft.azure:azure-keyvault` : Azure Key Vault Provider para o recurso Always Encrypted no Azure Key Vault (opcional)
 - `com.microsoft.azure:azure-keyvault-webkey` : Azure Key Vault Provider para o recurso Always Encrypted no Azure Key Vault (opcional)
 - `com.microsoft.azure:adal4j` : Biblioteca do Microsoft Azure Active Directory para Java para o recurso de Autenticação do Azure Active Directory e o recurso Azure Key Vault (opcional)
 - `com.microsoft.rest:client-runtime` : Biblioteca do Microsoft Azure Active Directory para Java para o recurso de Autenticação do Azure Active Directory e o recurso Azure Key Vault (opcional)
- `org.osgi:org.osgi.core`: Biblioteca principal de OSGi para suporte a OSGi Framework.
- `org.osgi:org.osgi.compendium`: Biblioteca com compêndio de OSGi para suporte a OSGi Framework.

## <a name="test-time"></a>Tempo de teste

Os projetos específicos que exigem qualquer um dos recursos anteriores precisam declarar explicitamente as respectivas dependências em seu arquivo POM.

**Por exemplo:** quando estiver usando o recurso de Autenticação do Azure Active Directory, será necessário declarar novamente a dependência `adal4j` no arquivo POM do projeto. Veja o trecho de código a seguir:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
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

**Por exemplo:** quando estiver usando o recurso Azure Key Vault, será necessário declarar novamente a dependência `azure-keyvault` e a dependência `adal4j` no arquivo POM do projeto. Veja o trecho de código a seguir:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
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

### <a name="working-with-the-azure-key-vault-provider"></a>Trabalhando com o Azure Key Vault Provider:

- JDBC Driver versões 7.2.2 – versões de dependência: Azure-Keyvault (versão 1.2.0), Azure-Keyvault-Webkey (versão 1.2.0), o Adal4j (versão 1.6.3), Client-Runtime-for-AutoRest (1.6.5) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC Driver versão 7.0.0 – versões de dependência: Azure-Keyvault (versão 1.0.0), Adal4j (versão 1.6.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC Driver versão 6.4.0 – versões de dependência: Azure-Keyvault (versão 1.0.0), Adal4j (versão 1.4.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC Driver versão 6.2.2 – versões de dependência: Azure-Keyvault (versão 1.0.0), Adal4j (versão 1.4.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC Driver versão 6.0.0 – versões de dependência: Azure-Keyvault (versão 0.9.7), Adal4j (versão 1.3.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> Nas versões 6.2.2 e 6.4.0 do driver, a dependência azure-keyvault-java foi atualizada para a versão 1.0.0. No entanto, a nova versão não era compatível com a versão anterior (0.9.7) e interrompe a implementação existente no driver. A nova implementação no driver exigiu alterações na API, que, por sua vez, interrompe programas do cliente que usam o Azure Key Vault Provider.
>
> Esse problema foi resolvido na versão mais recente do driver (7.0.0). O construtor removido que usava o mecanismo de retorno de chamada de autenticação foi novamente adicionado ao Azure Key Vault Provider para oferecer uma compatibilidade com as versões anteriores.

### <a name="working-with-azure-active-directory-authentication"></a>Trabalhando com a Autenticação do Azure Active Directory:

- JDBC Driver versão 7.2.2 – versões de dependência: Adal4j (versão 1.6.3), Client-Runtime-for-AutoRest (1.6.5) e suas dependências
- JDBC Driver versão 7.0.0 – versões de dependência: Adal4j (versão 1.6.0) e suas dependências
- JDBC Driver versão 6.4.0 – versões de dependência: Adal4j (versão 1.4.0) e suas dependências
- JDBC Driver versão 6.2.2 – versões de dependência: Adal4j (versão 1.4.0) e suas dependências
- JDBC Driver versão 6.0.0 – versões de dependência: Adal4j (versão 1.3.0) e suas dependências. Nesta versão do driver, é possível se conectar usando somente o modo de autenticação _ActiveDirectoryIntegrated_, em um sistema operacional Windows, e usando sqljdbc_auth.dll e a Biblioteca de Autenticação do Active Directory para SQL Server (ADALSQL. DLL).

Da verão 6.4.0 do driver em diante, os aplicativos não exigem necessariamente o uso da ADALSQL.DLL em sistemas operacionais Windows. Nos *sistemas operacionais que não são Windows*, o driver exige um tíquete Kerberos para funcionar com a autenticação ActiveDirectoryIntegrated. Para saber mais sobre como se conectar ao Active Directory usando o Kerberos, confira o artigo [Definir tíquete Kerberos no Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac).

Nos *sistemas operacionais Windows*, o driver busca o sqljdbc_auth.dll por padrão e não exige a instalação do tíquete Kerberos ou das dependências de biblioteca do Azure. Se o sqljdbc_auth.dll não estiver disponível, o driver buscará o tíquete Kerberos para autenticação no Active Directory como ocorre em outros sistemas operacionais.

Você pode obter um [aplicativo de exemplo](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) que usa esse recurso.

## <a name="see-also"></a>Confira também

[Repositório GitHub do JDBC Driver](https://github.com/microsoft/mssql-jdbc)  
[Referência de API do JDBC Driver](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
