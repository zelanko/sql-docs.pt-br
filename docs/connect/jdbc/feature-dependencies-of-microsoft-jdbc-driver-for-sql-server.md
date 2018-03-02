---
title: "Recurso de dependências do Microsoft JDBC Driver para SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 703a27220a80744c46ca0bc7667756cec1ab6596
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
---
# <a name="feature-dependencies-of-microsoft-jdbc-driver-for-sql-server"></a>Dependências de recurso do Microsoft JDBC Driver para SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

 Esta página contém a lista de bibliotecas que depende do Microsoft JDBC Driver para SQL Server. O projeto tem as seguintes dependências.
 
 ## <a name="compile-time"></a>Tempo de compilação
 - `azure-keyvault` : O provedor do Cofre de chave do azure para o recurso de sempre criptografado Azure Key Vault (opcional)
 - `adal4j` : Biblioteca do Active Directory do azure para Java para o recurso de autenticação do Active Directory do Azure e o recurso de Cofre de chaves do Azure (opcional)

 ##  <a name="test-time"></a>Tempo de teste
Projetos específicos que exigem um destes dois recursos acima precisam declarar explicitamente as respectivas dependências em seu arquivo pom:

***Por exemplo:*** se você estiver usando *recurso de autenticação do Active Directory do Azure*, em seguida, você precisa declarar novamente *adal4j* dependência no arquivo de pom do seu projeto. Consulte o trecho a seguir: 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>
```

***Por exemplo:*** se você estiver usando *recurso de Cofre de chaves do Azure* , em seguida, você precisa declarar novamente *azure keyvault* dependência e *adal4j* dependência no seu arquivo pom do projeto. Consulte o trecho a seguir: 
```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre8</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.4.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```
 
 ## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisitos de dependência para o Driver JDBC

 ### <a name="azure-keyvault-feature"></a>Recurso Keyvault do Azure:
- JDBC Driver versão 6.0.0 
    - Versões de dependência: Azure-Keyvault (versão 0.9.7), Adal4j (versão 1.3.0) e suas dependências ( [aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))
- JDBC Driver versão 6.2.2 e posterior (incluindo o 6.4.0 mais recente)
    - Versões de dependência: Azure-Keyvault (versão 1.0.0), Adal4j (versão 1.4.0) e suas dependências ([aplicativo de exemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))

> [!NOTE]
>   A partir de v6.2.2, a dependência de java do azure-keyvault é atualizada para a versão 1.0.0. No entanto, a nova versão não é compatível com a versão anterior (versão 0.9.7) e, portanto, divide a implementação existente no driver. A nova implementação do driver requer alterações de API, que por sua vez interromper programas de cliente que usam o recurso de Cofre de chaves do Azure.

  
 ### <a name="azure-active-directory-authentication"></a>Autenticação do Active Directory do Azure:
- JDBC Driver versão 6.0.0 
    - Versões de dependência: Adal4j (versão 1.3.0) e suas dependências
        - Nesta versão do driver, você pode se conectar usando *ActiveDirectoryIntegrated* modo de autenticação somente em um sistema operacional e usando sqljdbc_auth.dll e a biblioteca de autenticação do Active Directory para SQL Server (o Windows ADALSQL. DLL). 
- JDBC Driver versão 6.4.0
    - Versões de dependência: Adal4j (versão 1.4.0) e suas dependências
        - Nesta versão do driver, seu aplicativo não requer o uso de ADALSQL. DLL. Dependendo do sistema operacional. Para **sistemas operacionais não Windows**, o driver requer o tíquete do Kerberos para trabalhar com a autenticação ActiveDirectoryIntegrated. Consulte [tíquete Kerberos definida no Windows, Mac e do Linux](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) para obter mais detalhes. Para **sistemas operacionais Windows**, driver por padrão verifica se sqljdbc_auth.dll está carregado e não exige a dependência de configuração ou adal4j de tíquete do Kerberos. No entanto, se sqljdbc_auth.dll não estiver carregado, o driver se comporta da mesma forma que sistemas operacionais não Windows e requer a instalação, que é descrita no exemplo a seguir: um aplicativo de exemplo usando esse recurso pode ser encontrado [aqui](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) .

 ## <a name="see-also"></a>Consulte também  
 [Repositório do GitHub do JDBC Driver](https://github.com/microsoft/mssql-jdbc)  
 [Referência da API do Driver JDBC](../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  