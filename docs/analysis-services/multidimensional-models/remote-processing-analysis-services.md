---
title: Remoto processamento (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d58bcb3c-0b3f-4ab0-81eb-4fdcc86153af
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f32eb86f0d4b18ac576df77a28885c7f2053d962
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="remote-processing-analysis-services"></a>Processamento remoto (Analysis Services)
  Você pode executar processamento em um controle remoto agendado ou autônomo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância, em que a solicitação de processamento origina-se de um computador, mas é executada em outro computador na mesma rede.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Se você estiver executando versões diferentes do SQL Server em cada computador, as bibliotecas de cliente devem corresponder à versão da instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está processando o modelo.
  
-   No servidor remoto, a opção **Permitir conexões remotas a este computador** deve estar habilitada e a conta de emitir a solicitação de processamento deve estar listada como um usuário permitido.  
  
-   Regras de Firewall do Windows devem ser configuradas para permitir conexões de entrada para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Verifique se você pode se conectar à instância remota [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Consulte [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
-   Resolva quaisquer erros de processamento local existentes antes de tentar o processamento remoto. Verifique que quando a solicitação de processamento for local, os dados possam ser recuperados com êxito da fonte de dados relacional externa. Consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md) para obter instruções sobre como especificar as credenciais usadas para recuperar os dados.  
  
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
  
-   [Configurar o SQL Server Agent](http://msdn.microsoft.com/library/2e361a62-9e92-4fcd-80d7-d6960f127900)  
  
-   [SQL Server Agent Components](http://msdn.microsoft.com/library/8d1dc600-aabb-416f-b3af-fbc9fccfd0ec) sugere as funções de servidor fixas alternativas se a concessão de permissões **sysadmin** não for possível.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Agent Components](http://msdn.microsoft.com/library/8d1dc600-aabb-416f-b3af-fbc9fccfd0ec)   
 [Agendar tarefas administrativas do SSAS com o SQL Server Agent](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)   
 [Processamento em lotes &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)   
 [Processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Processamento de objetos &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)  
  
  

