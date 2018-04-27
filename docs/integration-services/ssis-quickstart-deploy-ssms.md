---
title: Implantar um projeto do SSIS com o SSMS | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c13783a7bbd5a23c2329151932f4438255babb9b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>Implantar um projeto do SSIS com o SSMS (SQL Server Management Studio)
Este guia de início rápido demonstra como usar o SSMS (SQL Server Management Studio) para se conectar ao banco de dados do Catálogo do SSIS e, em seguida, executar o Assistente de Implantação do Integration Services para implantar um projeto do SSIS no Catálogo do SSIS. 

O SQL Server Management Studio é um ambiente integrado para gerenciar qualquer infraestrutura do SQL, do SQL Server ao Banco de Dados SQL. Para obter mais informações sobre o SSMS, consulte [SSMS (SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Prerequisites

Antes de começar, verifique se você tem a última versão do SQL Server Management Studio. Para baixar o SSMS, consulte [Baixar o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Conectar-se ao banco de dados SSISDB

Use o SQL Server Management Studio para estabelecer uma conexão com o Catálogo do SSIS. 

> [!NOTE]
> Um servidor de Banco de Dados SQL do Azure escuta na porta 1433. Se estiver tentando se conectar a um servidor de Banco de Dados SQL do Azure em um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você se conecte com êxito.

1. Abra o SQL Server Management Studio.

2. Na caixa de diálogo **Conectar-se ao Servidor**, insira as seguintes informações:

   | Configuração       | Valor sugerido | Obter mais informações | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de banco de dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome do servidor totalmente qualificado | Se estiver se conectando a um servidor de Banco de Dados SQL do Azure, o nome estará neste formato: `<server_name>.database.windows.net`. |
   | **Autenticação** | Autenticação do SQL Server | Este guia de início rápido usa a autenticação do SQL. |
   | **Logon** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |

3. Clique em **Conectar**. A janela Pesquisador de Objetos será aberta no SSMS. 

4. No Pesquisador de Objetos, expanda **Catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados do Catálogo do SSIS.

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar o Assistente de Implantação do Integration Services
1. No Pesquisador de Objetos, com o nó **Catálogos do Integration Services** e o **SSISDB** expandidos, expanda a pasta do projeto.

2.  Selecione o nó **Projetos**.

3.  Clique com o botão direito do mouse no nó **Projetos** e selecione **Implantar projeto**. O Assistente de Implantação do Integration Services será aberto. Implante um projeto do catálogo atual ou do sistema de arquivos.

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
    - [Implantar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
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
