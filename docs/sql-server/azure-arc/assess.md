---
title: Configurar a Avaliação do SQL para o SQL Server habilitado para o Azure Arc
titleSuffix: ''
description: Configurar uma avaliação sob demanda para uma instância do SQL Server habilitada para o Azure Arc
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 41a7f1f4edc247f211ee5b3cdcaddfd139c5027c
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988012"
---
# <a name="configure-on-demand-sql-assessment-for-azure-arc-enabled-sql-server-instance"></a>Configurar uma avaliação do SQL sob demanda para uma instância do SQL Server habilitada para o Azure Arc

Você pode habilitar a Avaliação do SQL para suas instâncias do SQL Server seguindo estas etapas.

## <a name="prerequisites"></a>Pré-requisitos

* Sua instância do SQL Server está conectada ao Azure Arc. Siga estas instruções para [integrar sua instância do SQL Server ao SQL Server habilitado para o Arc](connect.md).

* A extensão do MMA está instalada e configurada no computador. Siga estas instruções para [Instalar o MMA (Microsoft Monitoring Agent)](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma). Para obter mais informações, confira [Agente do Log Analytics](/azure/azure-monitor/platform/log-analytics-agent).

* O SQL Server tem o [protocolo TCP/IP habilitado](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).

* O [navegador do SQL Server](../../tools/configuration-manager/sql-server-browser-service.md) está em execução se você está operando uma instância nomeada do SQL Server.

* Você examinou o documento do SQL Server em [Pré-requisitos de avaliações sob demanda do hub de serviços](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents).

## <a name="enable-on-demand-sql-assessment"></a>Habilitar a Avaliação do SQL sob demanda

1. Abra o recurso SQL Server – Azure Arc e selecione __Integridade do Ambiente__ no menu à esquerda.

   ![Seleção da Avaliação do SQL](media/assess/sql-assessment-heading-sql-server-arc.png)

1. Especifique um diretório de trabalho no computador de coleta de dados. Por padrão, `C:\sql_assessment\work_dir` será usado. Durante a coleta e a análise, os dados são armazenados temporariamente nessa pasta. Se a pasta não existir, ela será criada automaticamente.

1. Clique em __Baixar script de configuração__ e copie o script baixado para o computador de destino.

1. Inicie uma instância de administrador do __powershell.exe__ e siga um destes procedimentos: 
   * Se você estiver usando uma conta de domínio, execute os comandos a seguir. Você será solicitado a fornecer a conta de usuário e a senha. 

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

    * Se você estiver usando uma conta MSA, execute os comandos a seguir.

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

   > [!NOTE]
   > O script agendará uma tarefa chamada *SQLAssessment* para ser executada dentro de uma hora após a execução do script anterior e, depois disso, a cada sete dias. A tarefa pode ser modificada para ser executada em uma data e hora diferentes ou até mesmo forçada a ser executada imediatamente da biblioteca do agendador de tarefas > Microsoft > Operations Management Suite > AOI*** > Avaliações > SQLAssessment. Essa tarefa dispara a coleta de dados.

## <a name="view-the-assessment-results"></a>Exibir os resultados da avaliação

O botão __Exibir o resultado da avaliação do SQL__ na folha _Integridade do Ambiente_ fica desabilitada até que os resultados estejam prontos no Log Analytics. Depois que o botão for ativado, você poderá clicar nele para exibir os resultados. Pode levar até duas horas para ver os resultados no Log Analytics depois que os arquivos de dados são processados no computador de destino.

![Resultados da avaliação do SQL](media/assess/sql-assessment-results.png)

Você pode ver o estado do processamento de dados no computador de coleta verificando os arquivos na pasta de trabalho. Depois que a tarefa agendada for concluída, você verá vários arquivos com o prefixo _new._ no diretório de trabalho:

![Arquivos de dados prontos](media/assess/sql-assessment-data-files-ready.png)

O Microsoft Monitoring Agent examina a pasta de trabalho a cada 15 minutos procurando arquivos _new._ e envia os dados para o workspace do Log Analytics. Depois que o arquivo for carregado, o prefixo será alterado de _new._ para _processed._ :

![Arquivos de dados processados](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>Próximas etapas

Confira o documento do SQL Server em [Pré-requisitos de avaliações sob demanda do hub de serviços](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents) para obter mais informações.

Para obter suporte abrangente da Avaliação do SQL sob demanda, uma assinatura de suporte Premier ou Unificado é necessária. Confira [Suporte Premier do Azure](https://azure.microsoft.com/support/plans/premier) para obter detalhes.