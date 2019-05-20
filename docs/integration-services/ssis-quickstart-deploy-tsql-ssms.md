---
title: Implantar um projeto do SSIS com o Transact-SQL (SSMS) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 00d4557d7a525866bf74cd4883d0b403d6382232
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65717679"
---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>Implantar um projeto do SSIS por meio do SSMS com o Transact-SQL

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Este guia de início rápido demonstra como usar o SSMS (SQL Server Management Studio) para se conectar ao banco de dados do Catálogo do SSIS e, em seguida, usar instruções do Transact-SQL para implantar um projeto do SSIS no Catálogo do SSIS. 

O SQL Server Management Studio é um ambiente integrado para gerenciar qualquer infraestrutura do SQL, do SQL Server ao Banco de Dados SQL. Para obter mais informações sobre o SSMS, consulte [SSMS (SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Prerequisites

Antes de começar, verifique se você tem a última versão do SQL Server Management Studio. Para baixar o SSMS, consulte [Baixar o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="supported-platforms"></a>Plataformas compatíveis

Você pode usar as informações neste guia de início rápido para implantar um projeto do SSIS nas seguintes plataformas:

-   SQL Server no Windows.

Você não pode usar as informações neste guia de início rápido para implantar um pacote do SSIS para o Banco de Dados SQL do Azure. O procedimento armazenado `catalog.deploy_project` espera o caminho para o arquivo `.ispac` no sistema de arquivos local. Para obter mais informações sobre como implantar e executar pacotes no Azure, veja [Remover e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Você não pode usar as informações neste guia de início rápido para implantar um pacote do SSIS no SQL Server em Linux. Para obter mais informações sobre como executar pacotes no Linux, veja [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="connect-to-the-ssis-catalog-database"></a>Conectar-se ao banco de dados de Catálogo do SSIS

Use o SQL Server Management Studio para estabelecer uma conexão com o Catálogo do SSIS. 

1. Abra o SQL Server Management Studio.

2. Na caixa de diálogo **Conectar-se ao Servidor**, insira as seguintes informações:

   | Configuração       | Valor sugerido | Obter mais informações | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de banco de dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome do servidor totalmente qualificado |  |
   | **Autenticação** | Autenticação do SQL Server | |
   | **Logon** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |

3. Clique em **Conectar**. A janela Pesquisador de Objetos será aberta no SSMS. 

4. No Pesquisador de Objetos, expanda **Catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados do Catálogo do SSIS.

## <a name="run-the-t-sql-code"></a>Executar o código T-SQL
Execute o seguinte código Transact-SQL para implantar um projeto do SSIS.

1.  No SSMS, abra uma nova janela de consulta e cole o código a seguir.

2.  Atualizar os valores de parâmetro no procedimento armazenado `catalog.deploy_project` para seu sistema.

3.  Verifique se **SSISDB** é o banco de dados atual.

4.  Execute o script.

5. No Pesquisador de Objetos, atualize o conteúdo de **SSISDB** se necessário e procure o projeto que você implantou.

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
- Considere outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implantar um pacote do SSIS por meio do prompt de comando](./ssis-quickstart-deploy-cmdline.md)
    - [Implantar um pacote do SSIS com o PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implantar um pacote do SSIS com o C#](./ssis-quickstart-deploy-dotnet.md) 
- Execute um pacote implantado. Para executar um pacote, você pode escolher uma entre várias ferramentas e linguagens. Para saber mais, veja os tópicos a seguir:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
