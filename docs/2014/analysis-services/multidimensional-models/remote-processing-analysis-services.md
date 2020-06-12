---
title: Processamento remoto (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d58bcb3c-0b3f-4ab0-81eb-4fdcc86153af
author: minewiskan
ms.author: owend
ms.openlocfilehash: 699cc312b2f4b0a716d08259daf189276551e5d4
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545764"
---
# <a name="remote-processing-analysis-services"></a>Processamento remoto (Analysis Services)
  Você pode executar processamento em um controle remoto agendado ou autônomo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância, em que a solicitação de processamento origina-se de um computador, mas é executada em outro computador na mesma rede.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Se você estiver executando versões diferentes do SQL Server em cada computador, as bibliotecas de cliente devem corresponder à versão da instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está processando o modelo. Por exemplo, se o processamento estiver em uma instância [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] e, em seguida, o computador do qual se origina a solicitação precisar ter a biblioteca de cliente correspondente a [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]. Consulte [Provedores de dados usados em conexões do Analysis Services](../instances/data-providers-used-for-analysis-services-connections.md).  
  
-   No servidor remoto, a opção **Permitir conexões remotas a este computador** deve estar habilitada e a conta de emitir a solicitação de processamento deve estar listada como um usuário permitido.  
  
-   Regras de Firewall do Windows devem ser configuradas para permitir conexões de entrada para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Verifique se você pode se conectar à instância remota [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Consulte [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
-   Resolva quaisquer erros de processamento local existentes antes de tentar o processamento remoto. Verifique que quando a solicitação de processamento for local, os dados possam ser recuperados com êxito da fonte de dados relacional externa. Consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](set-impersonation-options-ssas-multidimensional.md) para obter instruções sobre como especificar as credenciais usadas para recuperar os dados.  
  
## <a name="on-demand-remote-processing"></a>O processamento remoto sob demanda  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aceita solicitações de processamento de contas de usuário ou aplicativo que têm permissões de administrador [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se você é um administrador, verifique se você pode se conectar à instância remota e processar o banco de dados manualmente pela conexão remota.  
  
1.  No computador que será usado para agendar o processamento, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conecte-se à instância remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  Clique com o botão direito do mouse no banco de dados, selecione **Processo**, aponte para **Script** e escolha **Ação do Script para nova janela de consulta**. Os comandos usados para chamar o processamento serão exibidos na janela de consulta.  
  
3.  Clique em **OK** para iniciar o processamento.  
  
     A conclusão bem-sucedida dessa tarefa fornece uma consulta XMLA que você pode inserir em um trabalho agendado. Ela também confirma que não há problemas de conexão.  
  
## <a name="schedule-remote-processing-using-sql-server-agent-service"></a>Agendar processamento remoto usando o serviço SQL Server Agent  
 Por padrão, o serviço SQL Server Agent é executado sob uma conta virtual, com conexões de rede feitas usando a conta do computador. Para evitar a necessidade de conceder direitos administrativos a uma conta de computador na instância remota [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você deve alterar a conta de serviço do SQL Server Agent para ser executada como uma conta de usuário de domínio com privilégios mínimos.  
  
 Certifique-se de conceder todas as permissões necessárias, incluindo dar à conta **sysadmin** direitos na instância do mecanismo de banco de dados que fornece o serviço.  
  
 Use os links a seguir para definir permissões:  
  
-   [Configurar o SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)  
  
-   [SQL Server Agent Components](../../ssms/agent/sql-server-agent.md#Components) sugere as funções de servidor fixas alternativas se a concessão de permissões **sysadmin** não for possível.  
  
 Depois que as permissões de conta são configuradas, continue com estas etapas.  
  
#### <a name="grant-the-sql-server-agent-account-administrator-permission-on-ssas"></a>Conceda a permissão de administrador de conta do SQL Server Agent no SSAS  
  
1.  Usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], conecte-se à instância remota [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  Clique com o botão direito do mouse no nome do servidor, clique em P**ropriedades**e em **Segurança**.  
  
3.  Clique em **Adicionar** para adicionar a conta do SQL Server Agent.  
  
#### <a name="create-the-job"></a>Criar o trabalho  
  
1.  No Management Studio, conecte-se à instância do mecanismo do banco de dados local. O SQL Server Agent é o último item no Pesquisador de objetos. Se necessário, inicie o serviço.  
  
2.  Clique com o botão direito do mouse em **Trabalho**s, clique em **Novo trabalho** e digite um nome.  
  
3.  Em etapas, clique em **Novo** e, em seguida, digite um nome.  
  
4.  Em Tipo, selecione **Comando do SQL Server Analysis Services**.  
  
5.  No servidor, digite o nome da instância remota [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
6.  Nesse comando, cole o comando XMLA para processamento no banco de dados. Este é o script XMLA gerado na etapa de verificação para processamento remoto sob demanda. Clique em **OK** para salvar o trabalho.  
  
#### <a name="start-sql-server-profiler"></a>Iniciar o SQL Server Profiler  
  
1.  No computador remoto, inicie o SQL Server Profiler. Conecte-se à instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, clique em **Executar** para iniciar o rastreamento usando os eventos padrão.  
  
     Você usará o SQL Server Profiler para monitorar os eventos de processamento, conforme elas ocorrem.  
  
2.  Opcionalmente, você pode definir propriedades de rastreamento para enviar o rastreamento para um arquivo ou tabela em um banco de dados.  
  
#### <a name="run-the-job"></a>Executar o trabalho  
  
1.  No computador usado para executar o trabalho, verifique se o trabalho pode executar a operação básica. No Pesquisador de objetos, no SQL Server Agent, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que você acabou de criado e clique em **Iniciar trabalho na etapa**. O trabalho será iniciado imediatamente. Você pode monitorar o progresso no SQL Server Profiler.  
  
2.  Como etapa final, modifique o trabalho para ser executado em uma agenda que você definir, adicionando quaisquer alertas ou notificações necessários para administrar o trabalho. Você também poderá refinar o script de processamento ou criar várias etapas do trabalho para processar objetos independentemente.  
  
## <a name="see-also"></a>Consulte Também  
 [Componentes do SQL Server Agent](../../ssms/agent/sql-server-agent.md#Components)   
 [Agendar tarefas administrativas do SSAS com SQL Server Agent](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)   
 [Analysis Services de &#40;de processamento em lotes&#41;](batch-processing-analysis-services.md)   
 [Processamento de objeto de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md)   
 [Processando objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)  
  
  
