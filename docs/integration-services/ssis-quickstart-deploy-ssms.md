---
title: Implantar um projeto do SSIS com o SSMS | Microsoft Docs
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
ms.openlocfilehash: b9729343ab14563ee6264795d6f098f3c22e91bf
ms.contentlocale: pt-br
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>Implantar um projeto do SSIS com o SQL Server Management Studio (SSMS)
Este guia rápido demonstra como usar o SQL Server Management Studio (SSMS) para se conectar ao banco de dados de catálogo do SSIS e, em seguida, execute o Assistente de implantação do Integration Services para implantar um projeto do SSIS no catálogo do SSIS. 

SQL Server Management Studio é um ambiente integrado para gerenciar qualquer infraestrutura SQL, do SQL Server para o banco de dados SQL. Para obter mais informações sobre o SSMS, consulte [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se que você tem a versão mais recente do SQL Server Management Studio. Para baixar o SSMS, consulte [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Conecte-se ao banco de dados SSISDB

Use o SQL Server Management Studio para estabelecer uma conexão para o catálogo do SSIS. 

> [!NOTE]
> Um servidor de banco de dados de SQL do Azure escuta na porta 1433. Se você está tentando se conectar a um servidor de banco de dados de SQL Azure de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo para que você se conectar com êxito.

1. Abra o SQL Server Management Studio.

2. No **conectar ao servidor** caixa de diálogo, digite as seguintes informações:

   | Configuração       | Valor sugerido | Obter mais informações | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de banco de dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome totalmente qualificado do servidor | Se você estiver se conectando a um servidor de banco de dados SQL, o nome é neste formato: `<server_name>.database.windows.net`. |
   | **Autenticação** | Autenticação do SQL Server | Este guia de início rápido usa a autenticação do SQL. |
   | **Logon** | A conta de administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha para sua conta de administrador do servidor | Esta é a senha que você especificou quando criou o servidor. |

3. Clique em **Conectar**. Abre a janela Pesquisador de objetos no SSMS. 

4. No Pesquisador de objetos, expanda **catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados de catálogo do SSIS.

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar o Assistente de implantação do Integration Services
1. No Pesquisador de objetos, com o **catálogos do Integration Services** nó e o **SSISDB** expandida, expanda a pasta do projeto.

2.  Selecione o **projetos** nó.

3.  Clique com botão direito no **projetos** nó e selecione **implantar projeto**. Abre o Assistente de implantação do Integration Services. Você pode implantar um projeto do catálogo atual ou do sistema de arquivos.

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
    -   Opcionalmente, clique em **Salvar relatório...**  para salvar os resultados em um arquivo XML.
    -   Clique em **fechar** para sair do assistente.

## <a name="next-steps"></a>Próximas etapas
- Considere a possibilidade de outras maneiras de implantar um pacote.
    - [Implantar um pacote do SSIS com Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
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

