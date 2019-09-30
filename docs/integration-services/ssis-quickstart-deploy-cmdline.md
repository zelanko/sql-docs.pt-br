---
title: Implantar um projeto do SSIS por meio do prompt de comando | Microsoft Docs
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 182dcae5867cd05d508357160aecb5c46d1d5e82
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281773"
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>Implantar um projeto do SSIS por meio do prompt de comando com ISDeploymentWizard.exe

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este guia de início rápido demonstra como implantar um projeto do SSIS por meio do prompt de comando executando o Assistente de Implantação do Integration Services, `ISDeploymentWizard.exe`.

Para obter mais informações sobre o Assistente de implantação do Integration Services, consulte [Assistente de Implantação do Integration Services](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

## <a name="prerequisites"></a>Prerequisites

A validação descrita neste artigo para implantação no Banco de Dados SQL do Azure requer SQL Server Data Tools (SSDT) versão 17.4 ou posterior. Para obter a versão mais recente do SSDT, consulte [Baixar o SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md).

Um servidor de Banco de Dados SQL do Azure escuta na porta 1433. Se estiver tentando se conectar a um servidor de Banco de Dados SQL do Azure em um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você se conecte com êxito.

## <a name="supported-platforms"></a>Plataformas compatíveis

Você pode usar as informações neste guia de início rápido para implantar um projeto do SSIS nas seguintes plataformas:

-   SQL Server no Windows.

-   Banco de Dados SQL do Azure. Para obter mais informações sobre como implantar e executar pacotes no Azure, veja [Remover e deslocar cargas de trabalho do SQL Server Integration Services para a nuvem](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Você não pode usar as informações neste guia de início rápido para implantar um pacote do SSIS no SQL Server em Linux. Para obter mais informações sobre como executar pacotes no Linux, veja [Extrair, transformar e carregar dados no Linux com o SSIS](../linux/sql-server-linux-migrate-ssis.md).

## <a name="for-azure-sql-database-get-the-connection-info"></a>Para o Banco de Dados SQL do Azure, obtenha as informações de conexão

Para implantar o projeto no Banco de Dados SQL do Azure, obtenha as informações de conexão necessárias para se conectar ao SSISDB (banco de dados de catálogo do SSIS). Você precisa das informações de logon e de nome do servidor totalmente qualificado nos procedimentos a seguir.

1. Faça logon no [portal do Azure](https://portal.azure.com/).
2. Selecione **Bancos de Dados SQL** no menu à esquerda e selecione o banco de dados do SSISDB na página **Bancos de dados SQL**. 
3. Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor. Para ver a opção **Clique para copiar**, passe o mouse sobre o nome do servidor. 
4. Se você esquecer suas informações de logon do servidor de Banco de Dados SQL do Azure, navegue até a página do servidor de Banco de Dados SQL para exibir o nome do administrador de servidor. Você pode redefinir a senha, se necessário.

## <a name="wizard_auth"></a> Métodos de autenticação no Assistente de Implantação

Se você estiver implantando em um SQL Server com o Assistente de Implantação, precisará usar a autenticação do Windows; não poderá usar a autenticação do SQL Server.

Se você estiver implantando em um servidor de Banco de Dados SQL do Azure, precisará usar a autenticação do SQL Server ou a autenticação do Azure Active Directory; não poderá usar a autenticação do Windows.

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar o Assistente de Implantação do Integration Services
1. Abra uma janela do prompt de comando.

2. Execute `ISDeploymentWizard.exe`. O Assistente de Implantação do Integration Services será aberto.

    Se a pasta que contém `ISDeploymentWizard.exe` não está na variável de ambiente `path`, talvez você precise usar o comando `cd` para mudar para o diretório dela. Para SQL Server 2017, essa pasta normalmente é `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

## <a name="deploy-a-project-with-the-wizard"></a>Implantar um projeto com o assistente
1. Na página **Introdução** do assistente, examine a introdução. Clique em **Avançar** para abrir a página **Selecionar Origem**.

2. Na página **Selecionar Origem**, selecione o projeto existente do SSIS a ser implantado.
    -   Para implantar um arquivo de implantação de projeto que você criou compilando um projeto no ambiente de desenvolvimento, selecione **Arquivo de implantação de projeto** e insira o caminho do arquivo .ispac.
    -   Para implantar um projeto que já tenha sido implantado em um banco de dados de catálogo do SSIS, selecione **Catálogo do Integration Services** e, em seguida, insira o nome do servidor e o caminho para o projeto no catálogo.
    Clique em **Avançar** para ver a página **Selecionar Destino** .
  
3.  Na página **Selecionar Destino**, selecione o destino para o projeto.
    -   Insira o nome do servidor totalmente qualificado. Se o servidor de destino for um servidor de Banco de Dados SQL do Azure, o nome estará neste formato `<server_name>.database.windows.net`.
    -   Forneça informações de autenticação e selecione **Conectar**. Consulte [Métodos de autenticação no Assistente de implantação](#wizard_auth) neste artigo.
    -   Em seguida, selecione **Procurar** para selecionar a pasta de destino no SSISDB.
    -   Selecione **Avançar** para abrir a página **Examinar**. (O botão **Avançar** é habilitado somente depois de selecionar **Conectar**.)

4.  Na página **Examinar**, examine as configurações selecionadas.
    -   Você pode alterar suas seleções clicando em **Anterior**ou clicando em qualquer uma das etapas no painel esquerdo.
    -   Clique em **Implantar** para começar o processo de implantação.

5.  Se você estiver implantando em um servidor de Banco de Dados SQL do Azure, a página **Validar** será aberta e verificará os pacotes no projeto quanto a problemas conhecidos que podem impedir que os pacotes sejam executados conforme o esperado no Integration Runtime do Azure-SSIS. Para obter mais informações, consulte [Validar pacotes do SSIS implantados no Azure](lift-shift/ssis-azure-validate-packages.md).

6.  Após a conclusão do processo de implantação, a página **Resultados** será aberta. Essa página exibe o êxito ou a falha de cada ação.
    -   Se a ação falhou, clique em **Com falha** na coluna **Resultado** para exibir uma explicação do erro.
    -   Opcionalmente, clique em **Salvar Relatório...** para salvar os resultados em um arquivo XML.
    -   Clique em **Fechar** para sair do assistente.

## <a name="next-steps"></a>Próximas etapas
- Considere outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implantar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implantar um pacote do SSIS com o PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implantar um pacote do SSIS com o C#](./ssis-quickstart-deploy-dotnet.md) 
- Execute um pacote implantado. Para executar um pacote, você pode escolher uma entre várias ferramentas e linguagens. Para saber mais, veja os tópicos a seguir:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
