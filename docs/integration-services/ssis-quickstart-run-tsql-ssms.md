---
title: Executar um pacote do SSIS com o Transact-SQL (SSMS) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4943bbddb027632a39e7a3ef13748dec286c68c
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328450"
---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>Executar um pacote do SSIS do SSMS com o Transact-SQL
Este guia de início rápido demonstra como usar o SSMS (SQL Server Management Studio) para se conectar ao banco de dados do Catálogo do SSIS e, em seguida, usar instruções do Transact-SQL para executar um pacote do SSIS armazenado no Catálogo do SSIS.

O SQL Server Management Studio é um ambiente integrado para gerenciar qualquer infraestrutura do SQL, do SQL Server ao Banco de Dados SQL. Para obter mais informações sobre o SSMS, consulte [SSMS (SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Prerequisites

Antes de começar, verifique se você tem a última versão do SSMS (SQL Server Management Studio). Para baixar o SSMS, consulte [Baixar o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Um servidor de Banco de Dados SQL do Azure escuta na porta 1433. Se estiver tentando se conectar a um servidor de Banco de Dados SQL do Azure em um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você se conecte com êxito.

## <a name="supported-platforms"></a>Plataformas compatíveis

Você pode usar as informações neste guia de início rápido para executar um pacote do SSIS nas seguintes plataformas:

-   SQL Server no Windows.

-   Banco de Dados SQL do Azure. Para obter mais informações sobre como implantar e executar pacotes no Azure, veja [Remover e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Você não pode usar as informações neste guia de início rápido para executar um pacote do SSIS no Linux. Para obter mais informações sobre como executar pacotes no Linux, veja [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="for-azure-sql-database-get-the-connection-info"></a>Para o Banco de Dados SQL do Azure, obtenha as informações de conexão

Para executar o pacote no Banco de Dados SQL do Azure, obtenha as informações de conexão necessárias para se conectar ao SSISDB (banco de dados de catálogo do SSIS). Você precisa das informações de logon e de nome do servidor totalmente qualificado nos procedimentos a seguir.

1. Faça logon no [portal do Azure](https://portal.azure.com/).
2. Selecione **Bancos de Dados SQL** no menu à esquerda e selecione o banco de dados do SSISDB na página **Bancos de dados SQL**. 
3. Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor. Para ver a opção **Clique para copiar**, passe o mouse sobre o nome do servidor. 
4. Se você esquecer suas informações de logon do servidor de Banco de Dados SQL do Azure, navegue até a página do servidor de Banco de Dados SQL para exibir o nome do administrador de servidor. Você pode redefinir a senha, se necessário.

## <a name="connect-to-the-ssisdb-database"></a>Conectar-se ao banco de dados SSISDB

Use o SQL Server Management Studio para estabelecer uma conexão ao catálogo do SSIS no seu servidor de Banco de Dados SQL do Azure. 

1. Abra o SQL Server Management Studio.

2. Na caixa de diálogo **Conectar-se ao Servidor**, insira as seguintes informações:

   | Configuração       | Valor sugerido | Obter mais informações | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de banco de dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome do servidor totalmente qualificado | Se estiver se conectando a um servidor de Banco de Dados SQL do Azure, o nome estará neste formato: `<server_name>.database.windows.net`. |
   | **Autenticação** | Autenticação do SQL Server | Com a autenticação do SQL Server, você pode se conectar ao SQL Server ou ao Banco de Dados SQL do Azure. Se você estiver se conectando a um servidor de Banco de Dados SQL do Azure, não poderá usar a autenticação do Windows. |
   | **Logon** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |

3.  Clique em **Conectar**. A janela Pesquisador de Objetos será aberta no SSMS.

4. No Pesquisador de Objetos, expanda **Catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados do Catálogo do SSIS.

## <a name="run-a-package"></a>Executar um pacote
Execute o seguinte código Transact-SQL para executar um pacote do SSIS.

1.  No SSMS, abra uma nova janela de consulta e cole o código a seguir. (Esse código é o código gerado pela opção **Script** na caixa de diálogo **Executar Pacote** no SSMS.)

2.  Atualizar os valores de parâmetro no procedimento armazenado `catalog.create_execution` para seu sistema.

3.  Verifique se o SSISDB é o banco de dados atual.

4.  Execute o script.

5. No Pesquisador de Objetos, atualize o conteúdo de **SSISDB** se necessário e procure o projeto que você implantou.

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
- Considere outras maneiras de executar um pacote.
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
