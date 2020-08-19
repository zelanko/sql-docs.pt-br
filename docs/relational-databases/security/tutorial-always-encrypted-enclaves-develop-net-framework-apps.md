---
description: 'Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros'
title: 'Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros | Microsoft Docs'
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: cd75e0a63ebbfbf6a5749939442b8b8a2e964d92
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88403792"
---
# <a name="tutorial-develop-a-net-framework-application-using-always-encrypted-with-secure-enclaves"></a>Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Este tutorial ensina como desenvolver um aplicativo simples que emite consultas de banco de dados que usam um enclave seguro no lado do servidor para o [Always Encrypted com enclaves seguros](encryption/always-encrypted-enclaves.md). 

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial é a continuação do [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](./tutorial-getting-started-with-always-encrypted-enclaves.md). Você precisa concluí-lo antes de prosseguir para as próximas etapas.

Além disso, você precisa do Visual Studio (a versão 2019 é recomendada) – você pode baixá-lo em [https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com). O computador de desenvolvimento de aplicativos deve executar o .NET Framework 4.7.2 ou posterior.

## <a name="step-1-set-up-your-visual-studio-project"></a>Etapa 1: Configure seu projeto do Visual Studio

Para usar o Always Encrypted com enclaves seguros em um aplicativo .NET Framework, você precisa verificar se seu aplicativo foi compilado no .NET Framework 4.7.2 e está integrado ao [NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders). Além disso, se armazenar a chave mestra da coluna no Azure Key Vault, você também precisará integrar seu aplicativo ao [NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider), versão 2.2.0 ou posterior. 

1. Abra o Visual Studio.

2. Crie um novo projeto de Aplicativo de Console de C\# (.NET Framework).

3. Certifique-se de que seu projeto tenha como destino pelo menos o .NET Framework 4.7.2. Clique com o botão direito do mouse no projeto no Gerenciador de Soluções, selecione Propriedades e defina a estrutura de destino como o .NET Framework 4.7.2.

4. Instale o seguinte pacote NuGet acessando **Ferramentas** (menu principal) > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**. Execute o seguinte código no Console do Gerenciador de Pacotes.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. Se você usa o Azure Key Vault para armazenar chaves mestras de coluna, instale os seguintes pacotes NuGet acessando **Ferramentas** (menu principal) > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**. Execute o seguinte código no Console do Gerenciador de Pacotes.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

7. Abra o arquivo de configuração do aplicativo do projeto.

8. Localize a seção \<configuration\> e adicione ou atualize as seções \<configSections\>.

   a. Se a seção de \<configuration\> **não** contiver a seção \<configSections\>, adicione o conteúdo a seguir imediatamente abaixo de \<configuration\>.
   
      ```xml
      <configSections>
         <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```
   b. Se a seção \<configruation\> já contiver a seção \<configSections\>, adicione a seguinte linha dentro de \<configSections\>:

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. Dentro da seção de configuração, abaixo de \<configSections\>, adicione a seguinte seção, que especifica um provedor de enclave a ser usado para atestar e interagir com os enclaves VBS:

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

Veja um exemplo completo de um arquivo app.config de um aplicativo de console simples.
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
  </configSections>
  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
    </providers>
  </SqlColumnEncryptionEnclaveProviders>
  <startup> 
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
  </startup>
</configuration>
```
## <a name="step-2-implement-your-application-logic"></a>Etapa 2: Implementar a lógica do aplicativo
Seu aplicativo se conectará ao banco de dados **ContosoHR** do [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](tutorial-getting-started-with-always-encrypted-enclaves.md) e executará uma consulta que contém o predicado `LIKE` na coluna **SSN** e uma comparação de intervalo na coluna **Salário**.

1. Substitua o conteúdo do arquivo Program.cs (gerado pelo Visual Studio) pelo código abaixo. Atualize a cadeia de conexão de banco de dados com o nome do servidor e a URL de atestado do enclave para seu ambiente. Você também pode atualizar as configurações de autenticação do banco de dados.

    ```cs
    using System;
    using System.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {
    
                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    SqlCommand cmd = connection.CreateCommand();
                    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";

                    SqlParameter paramSSNPattern = cmd.CreateParameter();

                    paramSSNPattern.ParameterName = @"@SSNPattern";
                    paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
                    paramSSNPattern.Direction = ParameterDirection.Input;
                    paramSSNPattern.Value = "%1111";
                    paramSSNPattern.Size = 11;

                    cmd.Parameters.Add(paramSSNPattern);

                    SqlParameter MinSalary = cmd.CreateParameter();

                    MinSalary.ParameterName = @"@MinSalary";
                    MinSalary.DbType = DbType.Currency;
                    MinSalary.Direction = ParameterDirection.Input;
                    MinSalary.Value = 900;

                    cmd.Parameters.Add(MinSalary);
                    cmd.ExecuteNonQuery();
    
                    SqlDataReader reader = cmd.ExecuteReader();
                    while (reader.Read())

                    {
                        Console.WriteLine(reader);
                        Console.WriteLine(reader[0] + ", " + reader[1] + ", " + reader[2] + ", " + reader[3]);
                    }   
                    Console.ReadKey();
                }
            }
        }
    }
    ```
2. Criar e executar o aplicativo.  

## <a name="see-also"></a>Consulte Também
- [Usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
