---
title: Implantar um projeto do SSIS com Transact-SQL (SSMS) | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: e97fb20f5b0ee10aa3e5de690676b7e0bb797b4c
ms.contentlocale: pt-br
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>Implantar um projeto do SSIS do SSMS com Transact-SQL

Este guia rápido demonstra como usar o SQL Server Management Studio (SSMS) para se conectar ao banco de dados de catálogo do SSIS e, em seguida, usar instruções Transact-SQL para implantar um projeto do SSIS no catálogo do SSIS. 

> [!NOTE]
> O método descrito neste artigo não está disponível quando você se conectar a um servidor de banco de dados SQL com o SSMS. O `catalog.deploy_project` procedimento armazenado espera o caminho para o `.ispac` arquivo no sistema de arquivos local (no local).

SQL Server Management Studio é um ambiente integrado para gerenciar qualquer infraestrutura SQL, do SQL Server para o banco de dados SQL. Para obter mais informações sobre o SSMS, consulte [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se que você tem a versão mais recente do SQL Server Management Studio. Para baixar o SSMS, consulte [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssis-catalog-database"></a>Conecte-se ao banco de dados de catálogo do SSIS

Use o SQL Server Management Studio para estabelecer uma conexão para o catálogo do SSIS. 

> [!NOTE]
> Um servidor de banco de dados de SQL do Azure escuta na porta 1433. Se você está tentando se conectar a um servidor de banco de dados de SQL Azure de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo para que você se conectar com êxito.

1. Abra o SQL Server Management Studio.

2. No **conectar ao servidor** caixa de diálogo, digite as seguintes informações:

   | Configuração       | Valor sugerido | Obter mais informações | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de banco de dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome totalmente qualificado do servidor |  |
   | **Autenticação** | Autenticação do SQL Server | Este guia de início rápido usa a autenticação do SQL. |
   | **Logon** | A conta de administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha para sua conta de administrador do servidor | Esta é a senha que você especificou quando criou o servidor. |

3. Clique em **Conectar**. Abre a janela Pesquisador de objetos no SSMS. 

4. No Pesquisador de objetos, expanda **catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados de catálogo do SSIS.

## <a name="run-the-t-sql-code"></a>Execute o código T-SQL
Execute o seguinte código de Transact-SQL para implantar um projeto do SSIS.

1.  No SSMS, abra uma nova janela de consulta e cole o código a seguir.

2.  Atualizar os valores de parâmetro no `catalog.deploy_project` procedimento armazenado para seu sistema.

3.  Certifique-se de que o SSISDB é o banco de dados atual.

4.  Execute o script.

5. No Pesquisador de objetos, atualizar o conteúdo de **SSISDB** se necessário e verificação para o projeto que você implantou.

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary =
    (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>Próximas etapas
- Considere a possibilidade de outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com o SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implantar um pacote do SSIS no prompt de comando](./ssis-quickstart-deploy-cmdline.md)
    - [Implantar um pacote do SSIS com o PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implantar um pacote do SSIS com c#](./ssis-quickstart-deploy-dotnet.md) 
- Execute um pacote implantado. Para executar um pacote, você pode escolher entre várias ferramentas e linguagens. Para obter mais informações, consulte os seguintes artigos:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com c#](./ssis-quickstart-run-dotnet.md) 

