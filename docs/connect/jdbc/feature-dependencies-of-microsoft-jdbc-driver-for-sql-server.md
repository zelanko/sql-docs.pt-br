---
title: Dependências de recurso do Microsoft JDBC Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61c66d192a158fb754563e2d103eba946dee47c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830354"
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Dependências de recurso do Microsoft JDBC Driver para SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esta página lista as bibliotecas que depende do Microsoft JDBC Driver para SQL Server. O projeto tem as seguintes dependências.

## <a name="compile-time"></a>Tempo de compilação

- `azure-keyvault`: O azure Key Vault Provider para o recurso sempre criptografado do Azure Key Vault (opcional)
- `adal4j`: Biblioteca do ActiveDirectory azure para Java para o recurso de autenticação do Azure Active Directory e o recurso de Cofre de chaves do Azure (opcional)

## <a name="test-time"></a>Tempo de teste

Projetos específicos que exigem qualquer um dos dois recursos acima precisam declarar explicitamente as respectivas dependências em seu arquivo pom:

**_Por exemplo:_**  ao usar _o recurso de autenticação do Azure Active Directory_, em seguida, você precisa declarar novamente _adal4j_ dependência no arquivo de pom do seu projeto. Consulte o trecho a seguir:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>
```

**_Por exemplo:_**  ao usar _o recurso do Azure Key Vault_, em seguida, você precisa declarar novamente _azure-keyvault_ dependência e _adal4j_ dependência no arquivo de pom do seu projeto. Consulte o trecho a seguir:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisitos de dependência para o JDBC Driver

### <a name="working-with-azure-key-vault-provider"></a>Trabalhando com o provedor do Azure Key Vault:

- Driver JDBC versão 7.0.0 - versões de dependência: Azure-Keyvault (versão 1.0.0), o Adal4j (versão 1.6.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-7-0-0.md))
- JDBC Driver versão 6.4.0 - versões de dependência: Azure-Keyvault (versão 1.0.0), o Adal4j (versão 1.4.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Driver JDBC versão 6.2.2 - versões de dependência: Azure-Keyvault (versão 1.0.0), o Adal4j (versão 1.4.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Driver JDBC versão 6.0.0 - versões de dependência: Azure-Keyvault (versão 0.9.7), o Adal4j (versão 1.3.0) e suas dependências ( [aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> Nas versões de driver v6.2.2 e v6.4.0, a dependência do azure-keyvault-java foi atualizada para a versão 1.0.0. No entanto, a nova versão não era compatível com a versão anterior (versão 0.9.7) e, portanto, divide a implementação existente no driver. A nova implementação no driver necessárias alterações na API, que por sua vez quebra programas cliente que usam o provedor do Cofre de chaves do Azure.

> Esse problema foi resolvido com v7.0.0 de versão de driver mais recente o construtor removido usando o mecanismo de retorno de chamada de autenticação é adicionado de volta ao provedor de Azure Key Vault para com versões anteriores compatibilidade.

### <a name="working-with-azure-active-directory-authentication"></a>Trabalhando com a Autenticação do Azure Active Directory:

- Driver JDBC versão 7.0.0 - versões de dependência: Ada4j (versão 1.6.0) e suas dependências
- JDBC Driver versão 6.4.0 - versões de dependência: Adal4j (versão 1.4.0) e suas dependências
- Driver JDBC versão 6.2.2 - versões de dependência: Adal4j (versão 1.4.0) e suas dependências
- Driver JDBC versão 6.0.0 - versões de dependência: Adal4j (versão 1.3.0), e suas dependências - nesta versão do driver, você pode se conectar usando _ActiveDirectoryIntegrated_ modo de autenticação apenas em um sistema de operacional do Windows e o uso de sqljdbc_auth e Active Directory Authentication Library para SQL Server (ADALSQL. DLL).

Da versão do driver 6.4.0 em diante, aplicativos não exigem necessariamente usando ADALSQL. DLL em sistemas de operacionais do Windows. Para **sistemas operacionais de não-Windows**, o driver requer o tíquete Kerberos para trabalhar com autenticação ActiveDirectoryIntegrated. Para obter mais informações sobre como se conectar ao Active Directory usando o Kerberos, consulte [tíquete Kerberos definido no Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac).

Para **os sistemas operacionais Windows**, driver procurará sqljdbc_auth por padrão e não requer a instalação do tíquete Kerberos ou dependências de biblioteca do Azure. No entanto, se sqljdbc_auth não estiver disponível, o driver procurará o tíquete Kerberos para autenticação no Active Directory, como em outros sistemas operacionais.

Um aplicativo de exemplo usando esse recurso pode ser encontrado [aqui](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md).

## <a name="see-also"></a>Consulte Também

[Repositório do GitHub do JDBC Driver](https://github.com/microsoft/mssql-jdbc)  
 [Referência de API do JDBC Driver](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
