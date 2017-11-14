---
title: Implantar, executar e monitorar um pacote do SSIS no Azure | Microsoft Docs
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
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 2e16666c412870cc55024e7156752f43ddbc1800
ms.contentlocale: pt-br
ms.lasthandoff: 10/13/2017

---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>Implantar, executar e monitorar um pacote do SSIS no Azure
Este tutorial mostra como implantar um projeto do SQL Server Integration Services para o banco de dados de catálogo do SSISDB no banco de dados do SQL Azure, executar um pacote no tempo de execução de integração do Azure SSIS e monitorar a execução de um pacote.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se que você tem a versão mais recente do SQL Server Management Studio ou 17.2. Para baixar a versão mais recente do SSMS, consulte [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Verifique também se você configurar o banco de dados do SSISDB e provisionado o tempo de execução de integração do Azure SSIS. Para obter informações sobre como provisionar SSIS no Azure, consulte [comparar e deslocar pacotes do SQL Server Integration Services (SSIS) para o Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="connect-to-the-ssisdb-database"></a>Conecte-se ao banco de dados SSISDB

Use o SQL Server Management Studio para se conectar ao catálogo do SSIS no seu servidor de banco de dados SQL. Para obter mais informações, consulte [conectar-se ao banco de dados de catálogo do SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

> [!IMPORTANT]
> Um servidor de banco de dados de SQL do Azure escuta na porta 1433. Se você está tentando se conectar a um servidor de banco de dados de SQL Azure de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo para que você se conectar com êxito.

1. Abra o SQL Server Management Studio.

2. **Conectar ao servidor**. No **conectar ao servidor** caixa de diálogo, digite as seguintes informações:

   | Configuração       | Valor sugerido | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de Banco de Dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome totalmente qualificado do servidor | O nome deve estar neste formato: **mysqldbserver.database.windows.net**. Se você precisar o nome do servidor, consulte [conectar-se ao banco de dados de catálogo do SSISDB no Azure](ssis-azure-connect-to-catalog-database.md). |
   | **Autenticação** | Autenticação do SQL Server | Este guia de início rápido usa a autenticação do SQL. |
   | **Logon** | A conta de administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha para sua conta de administrador do servidor | Esta é a senha que você especificou quando criou o servidor. |

3. **Conecte-se ao banco de dados SSISDB**. Selecione **opções** para expandir o **conectar ao servidor** caixa de diálogo. Em expandidos **conectar ao servidor** caixa de diálogo, selecione o **propriedades de Conexão** guia. No **conectar-se ao banco de dados** campo, selecione ou digite `SSISDB`.

4. Em seguida, selecione **conectar**. Abre a janela Pesquisador de objetos no SSMS. 

5. No Pesquisador de objetos, expanda **catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados de catálogo do SSIS.

## <a name="deploy-a-project"></a>Implantar um projeto

### <a name="start-the-integration-services-deployment-wizard"></a>Iniciar o Assistente de implantação do Integration Services
1. No Pesquisador de objetos no SSMS, com o **catálogos do Integration Services** nó e o **SSISDB** nó expandido, expanda a pasta do projeto.

2.  Selecione o **projetos** nó.

3.  Clique com botão direito no **projetos** nó e selecione **implantar projeto**. Abre o Assistente de implantação do Integration Services. Você pode implantar um projeto de um banco de dados de catálogo do SSIS ou do sistema de arquivos.

### <a name="deploy-a-project-with-the-deployment-wizard"></a>Implantar um projeto com o Assistente de implantação
1. Sobre o **Introdução** página do Assistente de implantação, examine a introdução. Selecione **próximo** para abrir o **Selecionar origem** página.

2. Sobre o **Selecionar origem** , selecione o projeto existente do SSIS para implantar.
    -   Para implantar um arquivo de implantação do projeto que você criou, selecione **Arquivo de implantação do projeto** e insira o caminho para o arquivo .ispac.
    -   Para implantar um projeto que reside em um catálogo do SSIS, selecione **catálogo do Integration Services**e, em seguida, insira o nome do servidor e o caminho para o projeto no catálogo.
    -   Selecione **próximo** para ver o **Selecionar destino** página.
  
3.  Sobre o **Selecionar destino** , selecione o destino para o projeto.
    -   Digite o nome do servidor totalmente qualificado no formato `<server_name>.database.windows.net`.
    -   Em seguida, selecione **procurar** para selecionar a pasta de destino em SSISDB.
    -   Selecione **próximo** para abrir o **revisão** página.  
  
4.  Sobre o **examine** , examine as configurações selecionadas.
    -   Você pode alterar suas seleções, selecionando **anterior**, ou selecionando qualquer uma das etapas no painel esquerdo.
    -   Selecione **implantar** para iniciar o processo de implantação.
  
5.  Depois que o processo de implantação estiver concluído, o **resultados** página será aberta. Essa página exibe o êxito ou a falha de cada ação.
    -   Se a ação falhou, selecione **falha** no **resultados** coluna para exibir uma explicação do erro.
    -   Opcionalmente, selecione **Salvar relatório...**  para salvar os resultados em um arquivo XML.
    -   Selecione **fechar** para sair do assistente.

## <a name="run-a-package"></a>Executar um pacote

1. No Pesquisador de objetos no SSMS, selecione o pacote que você deseja executar.

2. Clique com botão direito e selecione **Execute** para abrir o **executar pacote** caixa de diálogo.

3.  No **executar pacote** caixa de diálogo caixa, configure a execução do pacote, usando as configurações no **parâmetros**, **gerenciadores de Conexão**, e **avançado**  guias.

4.  Selecione **Okey** para executar o pacote.

## <a name="monitor-the-running-package-in-ssms"></a>Monitorar o pacote em execução no SSMS

Para exibir o status da execução no momento de operações do Integration Services no servidor do Integration Services, como implantação, validação e execução do pacote, use o **operações ativas** caixa de diálogo no SSMS. Para abrir o **operações ativas** caixa de diálogo, clique com botão direito **SSISDB**e, em seguida, selecione **operações ativas**.

Você também pode selecionar um pacote no Pesquisador de objetos, clique com botão direito e selecione **relatórios**, em seguida, **relatórios padrão**, em seguida, **todas as execuções**.

Para obter mais informações sobre como monitorar pacotes em execução no SSMS, consulte [Monitor executando pacotes e outras operações](https://docs.microsoft.com/en-us/sql/integration-services/performance/monitor-running-packages-and-other-operations).

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Monitorar o tempo de execução de integração do Azure SSIS

Para obter informações de status sobre o tempo de execução de integração do Azure SSIS nos quais pacotes estão em execução, use os seguintes comandos do PowerShell: para cada um dos comandos, forneça os nomes de fábrica de dados, o IV SSIS do Azure e o grupo de recursos.

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Obter metadados sobre o tempo de execução de integração do Azure SSIS

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Obter o status de tempo de execução de integração do Azure SSIS

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>Próximas etapas
- Saiba como agendar a execução do pacote. Para obter mais informações, consulte [SSIS de agendamento de execução de pacote no Azure](ssis-azure-schedule-packages.md)

