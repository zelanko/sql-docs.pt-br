---
title: Implantar um projeto do SSIS por meio do prompt de comando | Microsoft Docs
ms.date: 09/25/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: non-specific
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b7497837e9785a1e256921e354477bd345bcf49d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>Implantar um projeto do SSIS por meio do prompt de comando com ISDeploymentWizard.exe
Este tutorial de início rápido demonstra como implantar um projeto do SSIS por meio do prompt de comando executando o Assistente de Implantação do Integration Services, `ISDeploymentWizard.exe`.

Para obter mais informações sobre o Assistente de implantação do Integration Services, consulte [Assistente de Implantação do Integration Services](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar o Assistente de Implantação do Integration Services
1. Abra uma janela do prompt de comando.

2. Execute `ISDeploymentWizard.exe`. O Assistente de Implantação do Integration Services será aberto.

    Se a pasta que contém `ISDeploymentWizard.exe` não está na variável de ambiente `path`, talvez você precise usar o comando `cd` para mudar para o diretório dela. Para SQL Server 2017, essa pasta normalmente é `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

## <a name="deploy-a-project-with-the-wizard"></a>Implantar um projeto com o assistente
1. Na página **Introdução** do assistente, examine a introdução. Clique em **Avançar** para abrir a página **Selecionar Origem**.

2. Na página **Selecionar Origem**, selecione o projeto existente do SSIS a ser implantado.
    -   Para implantar um arquivo de implantação do projeto que você criou, selecione **Arquivo de implantação do projeto** e insira o caminho para o arquivo .ispac.
    -   Para implantar um projeto que reside em um catálogo do SSIS, selecione **Catálogo do Integration Services** e, em seguida, insira o nome do servidor e o caminho para o projeto no catálogo.
    Clique em **Avançar** para ver a página **Selecionar Destino** .
  
3.  Na página **Selecionar Destino**, selecione o destino para o projeto.
    -   Insira o nome do servidor totalmente qualificado. Se o servidor de destino for um servidor de Banco de Dados SQL do Azure, o nome estará neste formato: `<server_name>.database.windows.net`.
    -   Em seguida, clique em **Procurar** para selecionar a pasta de destino no SSISDB.
    Clique em **Avançar** para abrir a página **Examinar**.  
  
4.  Na página **Examinar**, examine as configurações selecionadas.
    -   Você pode alterar suas seleções clicando em **Anterior**ou clicando em qualquer uma das etapas no painel esquerdo.
    -   Clique em **Implantar** para começar o processo de implantação.
  
5.  Após a conclusão do processo de implantação, a página **Resultados** será aberta. Essa página exibe o êxito ou a falha de cada ação.
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
