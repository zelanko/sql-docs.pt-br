---
title: Implantar um projeto do SSIS no prompt de comando | Microsoft Docs
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
ms.openlocfilehash: a1df574e0436a9fa81e714dfdc21bcbd43c0bda8
ms.contentlocale: pt-br
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>Implantar um projeto do SSIS no prompt de comando com ISDeploymentWizard.exe
Este tutorial de início rápido demonstra como implantar um projeto do SSIS no prompt de comando executando o Assistente de implantação do Integration Services, `ISDeploymentWizard.exe`.

Para obter mais informações sobre o Assistente de implantação do Integration Services, consulte [Assistente de implantação do Integration Services](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar o Assistente de implantação do Integration Services
1. Abra uma janela do prompt de comando.

2. Execute `ISDeploymentWizard.exe`. Abre o Assistente de implantação do Integration Services.

    Se a pasta que contém `ISDeploymentWizard.exe` não está no seu `path` variável de ambiente, talvez você precise usar o `cd` comando para alterar para seu diretório. Para SQL Server 2017, essa pasta é normalmente `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

## <a name="deploy-a-project-with-the-wizard"></a>Implantar um projeto com o Assistente
1. Sobre o **Introdução** página do assistente, examine a introdução. Clique em **próximo** para abrir o **Selecionar origem** página.

2. Sobre o **Selecionar origem** , selecione o projeto existente do SSIS para implantar.
    -   Para implantar um arquivo de implantação do projeto que você criou, selecione **Arquivo de implantação do projeto** e insira o caminho para o arquivo .ispac.
    -   Para implantar um projeto que reside em um catálogo do SSIS, selecione **catálogo do Integration Services**e, em seguida, insira o nome do servidor e o caminho para o projeto no catálogo.
    Clique em **Avançar** para ver a página **Selecionar Destino** .
  
3.  Sobre o **Selecionar destino** , selecione o destino para o projeto.
    -   Digite o nome totalmente qualificado do servidor. Se o servidor de destino for um servidor de banco de dados SQL, o nome é neste formato: `<server_name>.database.windows.net`.
    -   Em seguida, clique em **procurar** para selecionar a pasta de destino em SSISDB.
    Clique em **próximo** para abrir o **revisão** página.  
  
4.  Sobre o **examine** , examine as configurações selecionadas.
    -   Você pode alterar suas seleções clicando em **Anterior**ou clicando em qualquer uma das etapas no painel esquerdo.
    -   Clique em **Implantar** para começar o processo de implantação.
  
5.  Depois que o processo de implantação estiver concluído, o **resultados** página será aberta. Essa página exibe o êxito ou a falha de cada ação.
    -   Se a ação falhou, clique em **falha** no **resultados** coluna para exibir uma explicação do erro.
    -   Opcionalmente, clique em **Salvar relatório... ** para salvar os resultados em um arquivo XML.
    -   Clique em **fechar** para sair do assistente.

## <a name="next-steps"></a>Próximas etapas
- Considere a possibilidade de outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com o SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implantar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implantar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implantar um pacote do SSIS com o PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implantar um pacote do SSIS com c#](./ssis-quickstart-deploy-dotnet.md) 
- Execute um pacote implantado. Para executar um pacote, você pode escolher entre várias ferramentas e linguagens. Para obter mais informações, consulte os seguintes artigos:
    - [Executar um pacote do SSIS com o SSMS](./ssis-quickstart-run-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com Transact-SQL (VS código)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com c#](./ssis-quickstart-run-dotnet.md) 

