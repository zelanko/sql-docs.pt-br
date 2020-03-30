---
title: 'Tutorial: Desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros | Microsoft Docs'
ms.custom: ''
ms.date: 10/18/2019
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 82ecd3fa04bbab0a1512ede08ebbc8bfaa3011f9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75244048"
---
# <a name="tutorial-develop-a-net-application-using-always-encrypted-with-secure-enclaves"></a>Tutorial: Desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

Este tutorial ensina como desenvolver um aplicativo simples que emite consultas de banco de dados que usam um enclave seguro no lado do servidor para o [Always Encrypted com enclaves seguros](../../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial é a continuação do [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md). Verifique se você o concluiu antes de seguir as etapas abaixo.

Além disso, você precisa do Visual Studio (a versão 2019 é recomendada) – você pode baixá-lo em [https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com). O ambiente de desenvolvimento de aplicativo deve usar o .NET Framework 4.6 ou posterior ou o .NET Core 2.1 ou posterior.

## <a name="step-1-set-up-your-visual-studio-project"></a>Etapa 1: Configure seu projeto do Visual Studio

Para usar o Always Encrypted com enclaves seguros em um aplicativo .NET Framework, você precisa verificar se seu aplicativo tem como destino o .NET Framework 4.6 ou posterior. Para usar o Always Encrypted com enclaves seguros em um aplicativo .NET Core, você precisa verificar se seu aplicativo tem como destino o .NET Core 2.1 ou posterior.

Além disso, se armazenar a chave mestra da coluna no Azure Key Vault, você também precisará integrar seu aplicativo ao [NuGet Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider).

1. Abra o Visual Studio.

2. Crie um projeto de Aplicativo do Console C\# (.NET Framework/Core).

3. Verifique se seu projeto tenha como destino pelo menos o .NET Framework 4.6 ou o .NET Core 2.1. Clique com o botão direito do mouse no projeto no Gerenciador de Soluções, selecione Propriedades e defina a Estrutura de destino.

4. Instale o seguinte pacote NuGet acessando **Ferramentas** (menu principal) > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**. Execute o seguinte código no Console do Gerenciador de Pacotes.

   ```powershell
   Install-Package Microsoft.Data.SqlClient -Version 1.1.0
   ```

5. Se você usa o Azure Key Vault para armazenar chaves mestras de coluna, instale os seguintes pacotes NuGet acessando **Ferramentas** (menu principal) > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**. Execute o seguinte código no Console do Gerenciador de Pacotes.

   ```powershell
   Install-Package Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider -Version 1.0.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

6. Especifique o `Attestation Protocol` e o `Enclave Attestation Url` na cadeia de conexão, que será usada em seu aplicativo para se comunicar com o SQL Server.

  ```cs
   Attestation Protocol = HGS; Enclave Attestation Url = http://hgs.bastion.local/Attestation; Column Encryption Setting = Enabled
   ```

## <a name="step-2-implement-your-application-logic"></a>Etapa 2: Implementar a lógica do aplicativo

Seu aplicativo se conectará ao banco de dados **ContosoHR** do [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md) e executará uma consulta que contém o predicado `LIKE` na coluna **SSN** e uma comparação de intervalo na coluna **Salário**.

1. Substitua o conteúdo do arquivo Program.cs (gerado pelo Visual Studio) pelo código a seguir. Atualize a cadeia de conexão de banco de dados com o nome do servidor e a URL de atestado do enclave do seu ambiente. Você também pode atualizar as configurações de autenticação do banco de dados.

    ```cs
    using System;
    using Microsoft.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {

                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Attestation Protocol = HGS; Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

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

- [Como usar o Always Encrypted com o Provedor de Dados do Microsoft .NET para SQL Server](sqlclient-support-always-encrypted.md)
- [Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted](azure-key-vault-example.md)
- [Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted habilitado com Enclaves Seguros](azure-key-vault-enclave-example.md)
