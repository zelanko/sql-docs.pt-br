---
title: Executar um pacote do SSIS com Transact-SQL (SSMS) | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 1c656661f645ac9f5d1659800893290819525f39
ms.contentlocale: pt-br
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>Executar um pacote do SSIS no SSMS com Transact-SQL
Este guia rápido demonstra como usar o SQL Server Management Studio (SSMS) para se conectar ao banco de dados de catálogo do SSIS e, em seguida, use instruções Transact-SQL para executar um pacote do SSIS armazenado no catálogo do SSIS.

SQL Server Management Studio é um ambiente integrado para gerenciar qualquer infraestrutura SQL, do SQL Server para o banco de dados SQL. Para obter mais informações sobre o SSMS, consulte [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se que você tem a versão mais recente do SQL Server Management Studio (SSMS). Para baixar o SSMS, consulte [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Conecte-se ao banco de dados SSISDB

Use o SQL Server Management Studio para estabelecer uma conexão para o catálogo do SSIS no seu servidor de banco de dados SQL. 

> [!NOTE]
> Um servidor de banco de dados de SQL do Azure escuta na porta 1433. Se você está tentando se conectar a um servidor de banco de dados de SQL Azure de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo para que você se conectar com êxito.

1. Abra o SQL Server Management Studio.

2. No **conectar ao servidor** caixa de diálogo, digite as seguintes informações:

   | Configuração       | Valor sugerido | Obter mais informações | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de banco de dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome totalmente qualificado do servidor | Se você estiver se conectando a um servidor de banco de dados SQL, o nome é neste formato: `<server_name>.database.windows.net`. |
   | **Autenticação** | Autenticação do SQL Server | Este guia de início rápido usa a autenticação do SQL. |
   | **Logon** | A conta de administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha para sua conta de administrador do servidor | Esta é a senha que você especificou quando criou o servidor. |

3.  Clique em **Conectar**. Abre a janela Pesquisador de objetos no SSMS.

4. No Pesquisador de objetos, expanda **catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados de catálogo do SSIS.

## <a name="run-a-package"></a>Executar um pacote
Execute o seguinte código de Transact-SQL para executar um pacote do SSIS.

1.  No SSMS, abra uma nova janela de consulta e cole o código a seguir. (Esse código é o código gerado pelo **Script** opção o **executar pacote** caixa de diálogo no SSMS.)

2.  Atualizar os valores de parâmetro no `catalog.create_execution` procedimento armazenado para seu sistema.

3.  Certifique-se de que o SSISDB é o banco de dados atual.

4.  Execute o script.

5. No Pesquisador de objetos, atualizar o conteúdo de **SSISDB** se necessário e verificação para o projeto que você implantou.

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx',
    @execution_id=@execution_id OUTPUT,
    @folder_name=N'Deployed Projects',
      @project_name=N'Integration Services Project1',
    @use32bitruntime=False,
      @reference_id=Null
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,
    @object_type=50,
      @parameter_name=N'LOGGING_LEVEL',
      @parameter_value=@var0
EXEC [SSISDB].[catalog].[start_execution] @execution_id
GO
```

## <a name="next-steps"></a>Próximas etapas
- Considere a possibilidade de outras maneiras de executar um pacote.
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com c#](./ssis-quickstart-run-dotnet.md) 

