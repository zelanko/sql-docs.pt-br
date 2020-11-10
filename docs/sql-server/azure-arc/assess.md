---
title: Configurar uma Avaliação do SQL sob demanda para uma instância do SQL Server habilitada para o Azure Arc
description: Configurar uma Avaliação do SQL sob demanda para uma instância do SQL Server habilitada para o Azure Arc
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: c6f2a0989cb13253ef4a6a26e013a6b8c7a84ded
ms.sourcegitcommit: f888ac94c7b5f6b6f138ab75719dadca04e8284a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93294385"
---
# <a name="configure-sql-assessment-on-an-azure-arc-enabled-sql-server-instance"></a>Configurar uma Avaliação do SQL em uma instância do SQL Server habilitada para o Azure Arc

A Avaliação do SQL fornece um mecanismo para avaliar a configuração do SQL Server. Este artigo fornece instruções para usar a Avaliação do SQL em uma instância do SQL Server habilitada para o Azure Arc.

## <a name="prerequisites"></a>Pré-requisitos

* A instância do SQL Server precisa estar conectada ao Azure Arc. Para obter instruções, confira o artigo [Conectar o SQL Server ao Azure Arc](connect.md).

* A extensão MMA (Microsoft Monitoring Agent) precisa estar instalada e configurada no computador. Veja o artigo [Instalar o MMA](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma) para obter instruções. Você também pode obter mais informações no artigo [Agente do Log Analytics](/azure/azure-monitor/platform/log-analytics-agent).

* A instância do SQL Server precisa estar com o [protocolo TCP/IP habilitado](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).

* O [serviço de navegador do SQL Server](../../tools/configuration-manager/sql-server-browser-service.md) precisa estar em execução se você está operando uma instância nomeada do SQL Server.

* Verifique se você já examinou o documento do SQL Server em [Pré-requisitos de avaliações sob demanda do hub de serviços](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents).

## <a name="run-on-demand-sql-assessment"></a>Executar a Avaliação do SQL sob demanda

1. Abra o recurso SQL Server – Azure Arc e selecione **Integridade do Ambiente** no painel à esquerda.

   > [!div class="mx-imgBorder"]
   > [ ![Captura de tela mostrando a tela de Integridade do Ambiente de um recurso SQL Server – Azure Arc.](media/assess/sql-assessment-heading-sql-server-arc.png) ](media/assess/sql-assessment-heading-sql-server-arc.png#lightbox)

> [!IMPORTANT]
> Se a extensão do MMA não estiver instalada, você não poderá iniciar a Avaliação do SQL sob demanda.

2. Selecione o tipo de conta. Se você tiver uma Conta de serviço gerenciado, ela permitirá que você inicie a Avaliação do SQL diretamente no Portal. Especifique o nome da conta.

> [!NOTE]
> Especificar uma *Conta de serviço gerenciado* ativará o botão **Configurar Avaliação do SQL** para que você possa iniciar a avaliação no Portal implantando uma *CustomScriptExtension*. Como somente uma *CustomScriptExtension* pode ser implantada por vez, a extensão de script para a Avaliação do SQL será removida automaticamente após a execução. Se você já tiver outra *CustomScriptExtension* implantada no computador de hospedagem, o botão **Configurar Avaliação do SQL** não será ativado.

3. Especifique um diretório de trabalho no computador de coleta de dados se quiser alterar o padrão. Por padrão, `C:\sql_assessment\work_dir` é usado. Durante a coleta e a análise, os dados são armazenados temporariamente nessa pasta. Se a pasta não existir, ela será criada automaticamente.

4. Se você iniciar a Avaliação do SQL no Portal clicando em **Configurar Avaliação do SQL** , uma bolha de implantação padrão será exibida.

> [!div class="mx-imgBorder"]
   > [ ![Captura de tela mostrando a implantação de CustomScriptExtension.](media/assess/sql-assessment-custom-script-deployment.png) ](media/assess/sql-assessment-custom-script-deployment.png#lightbox)

5. Se preferir iniciar a Avaliação do SQL no computador de destino, clique em **Baixar script de configuração** , copie o script baixado para o computador de destino e execute um dos seguintes blocos de código em uma instância de administrador de **powershell.exe** :

   * _Conta de domínio_ :  Você será solicitado a fornecer a conta de usuário e a senha.

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

   * _MSA (conta de serviço gerenciado)_

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

> [!NOTE]
> O script agenda uma tarefa chamada *SQLAssessment* , que dispara a coleta de dados. Essa tarefa é executada em até uma hora depois de você executar o script. Em seguida, ela se repete a cada sete dias.

> [!TIP]
> Você pode modificar a tarefa para ser executada em uma data e hora diferentes ou até mesmo forçá-la a ser executada imediatamente. Na biblioteca do Agendador de Tarefas, encontre **Microsoft** > **Operations Management Suite** > **AOI\*\*\***  > **Avaliações** > **Avaliação do SQL**.

## <a name="view-sql-assessment-results"></a>Ver os resultados da Avaliação do SQL

* No painel _Integridade do Ambiente_ , selecione o botão **Ver resultados da Avaliação do SQL**.

   > [!NOTE]
   > O botão **Ver resultados da Avaliação do SQL** permanece desabilitado até que os resultados estejam prontos no Log Analytics. Esse processo pode levar até duas horas depois que os arquivos de dados são processados no computador de destino.

   > [!div class="mx-imgBorder"]
   > [ ![Captura de tela mostrando os resultados da Avaliação do SQL.](media/assess/sql-assessment-results.png) ](media/assess/sql-assessment-results.png#lightbox)

* Você pode ver o estado do processamento de dados no computador de coleta verificando os arquivos na pasta de trabalho. Depois que a tarefa agendada for concluída, você verá vários arquivos com o prefixo _new._ no diretório de trabalho.

   > [!div class="mx-imgBorder"]
   > [ ![Captura de tela mostrando uma janela do Gerenciador de Arquivos que exibe novos arquivos de dados na pasta de trabalho.](media/assess/sql-assessment-data-files-ready.png) ](media/assess/sql-assessment-data-files-ready.png#lightbox)

* O Microsoft Monitoring Agent examina a pasta de trabalho a cada 15 minutos. Ele procura arquivos _new.*_ e envia os dados para o workspace do Log Analytics. Depois que o MMA carrega o arquivo, ele altera o prefixo de _new._ para _processed._

   > [!div class="mx-imgBorder"]
   > ![Captura de tela mostrando uma janela do Gerenciador de Arquivos que exibe arquivos de dados processados.](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>Próximas etapas

* Obtenha mais informações conferindo os documentos de pré-requisitos em [Avaliações sob demanda do hub de serviços](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents).

* Para obter suporte abrangente ao recurso de Avaliação do SQL sob demanda, uma assinatura de suporte Premier ou Unificado é necessária. Para obter detalhes, confira [Suporte Premier do Azure](https://azure.microsoft.com/support/plans/premier).
