---
title: Relatórios para o servidor de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.SUMMARY.RENDER.CUSTOM.REPORT.F1
ms.assetid: e976e7c0-a805-4370-bf73-356c8e3becfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aa53c012649f983953b61a21901763b9bdd02c8b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056439"
---
# <a name="reports-for-the-integration-services-server"></a>Relatórios do servidor do Integration Services
  Na versão atual do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], os relatórios padrão estão disponíveis no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para ajudar a monitorar projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , que foram implantados no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Esses relatórios ajudam a exibir o status e o histórico do pacote e, se necessário, a identificar a causa de falhas na execução do pacote.  
  
 Na parte superior de cada página de relatório, o ícone de voltar leva você à página anteriormente exibida, o ícone de atualização atualiza as informações exibidas na página e o ícone de impressão permite imprimir a página atual.  
  
 Para obter mais informações sobre como implantar pacotes no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , consulte [Implantar projetos no servidor do Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
## <a name="integration-services-dashboard"></a>Painel do Integration Services  
 O relatório **Painel do Integration Services** oferece uma visão geral de todas as execuções de pacote na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para cada pacote executado no servidor, o painel permite "ampliar" para localizar detalhes específicos sobre erros de execução de pacote que possam ter ocorrido.  
  
 O relatório exibe as seções de informações a seguir.  
  
|Seção|DESCRIÇÃO|  
|-------------|-----------------|  
|**Informações de Execução**|Mostra o número de execuções que estão em estados diferentes (com falha, executando, teve sucesso, outros) nas últimas 24 horas.|  
|**Informações do Pacote**|Mostra o número total de pacotes que foram executados nas últimas 24 horas.|  
|**Informações de Conexão**|Mostra as conexões que foram usadas em execuções com falha nas últimas 24 horas.|  
|**Informações Detalhadas do Pacote**|Mostra os detalhes das execuções completas ocorridas nas últimas 24 horas. Por exemplo, esta seção mostra o número de execuções com falha em relação ao número total de execuções, a duração de execuções (em segundos) e a duração média de execuções nos últimos três meses.<br /><br /> Você pode exibir informações adicionais para um pacote clicando em **Visão Geral**, **Todas as Mensagens**e **Desempenho de Execução**.<br /><br /> O relatório de **Desempenho de Execução** mostra a duração da última instância de execução, bem como as horas de início e de término, e o ambiente que foi aplicado.<br /><br /> O gráfico e a tabela associada incluídos no relatório de **Desempenho de Execução** mostram a duração das últimas 10 execuções com êxito do pacote. A tabela também mostra a duração média de uma execução em um período de três meses. Os ambientes diferentes e os valores literais diferentes podem ter sido aplicados em runtime dessas 10 execuções com êxito do pacote.<br /><br /> Finalmente, o relatório de **Desempenho de Execução** mostra a hora ativa e o tempo total para os componentes de fluxo de dados do pacote. O Tempo Ativo se refere ao tempo total que o componente gastou na execução em todas as fases, e o Tempo Total representa o tempo total decorrido para um componente. O relatório só exibe essas informações para componentes do pacote quando o nível de log da última execução do pacote foi definido como o desempenho ou detalhado.<br /><br /> O relatório de **Visão Geral** mostra o estado de tarefas do pacote. O relatório de **Mensagens** mostra as mensagens de evento e as mensagens de erro para o pacote e as tarefas, como relatar as horas de início e de término, e o número de linhas gravadas.<br /><br /> Você também pode clicar em **Exibir Mensagens** no relatório de **Visão Geral** para navegar até o relatório **Mensagens** . Você também pode clicar em **Exibir Visão Geral** no relatório **Mensagens** para navegar até o relatório **Visão Geral** .|  
  
 Você pode filtrar a tabela exibida em qualquer página clicando em **Filtrar** e, em seguida, selecionando os critérios na caixa de diálogo **Configurações de Filtro** . Os critérios de filtro disponíveis dependem dos dados que estão sendo exibidos. É possível alterar a ordem de classificação do relatório clicando no ícone de classificação na caixa de diálogo **Configurações de Filtro** .  
  
## <a name="all-executions-report"></a>Relatório Todas as Execuções  
 O **Relatório Todas as Execuções** exibe um resumo de todas as execuções do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que foram efetuadas no servidor. Pode haver várias execuções do pacote de exemplo. Ao contrário do relatório **Painel do Integration Services** , você pode configurar o relatório **Todas as Execuções** para mostrar as execuções iniciadas durante um intervalo de datas. As datas podem abranger vários dias, meses ou anos.  
  
 O relatório exibe as seções de informações a seguir.  
  
|Seção|DESCRIÇÃO|  
|-------------|-----------------|  
|Filtrar|Mostra o filtro atual aplicado ao relatório, como o intervalo de horas de início.|  
|Informações de Execução|Mostra a hora de início, a hora de término e a duração para cada execução do pacote. Você pode exibir uma lista de valores de parâmetros que foram usados com uma execução de pacote, como valores que foram transmitidos a um pacote filho usando a tarefa Executar Pacote. Para exibir a lista de parâmetros, clique em Visão Geral.|  
  
 Para obter mais informações sobre como usar a tarefa Executar Pacote para disponibilizar valores para um pacote filho, consulte [Tarefa Executar Pacote](control-flow/execute-package-task.md).  
  
 Para obter mais informações sobre parâmetros, consulte [Parâmetros do Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="all-connections"></a>Todas as Conexões  
 O relatório **Todas as Conexões** fornece as informações a seguir para conexões que falharam, para execuções que ocorreram na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 O relatório exibe as seções de informações a seguir.  
  
|Seção|DESCRIÇÃO|  
|-------------|-----------------|  
|Filtrar|Mostra o filtro atual aplicado ao relatório, como conexões com uma cadeia de caracteres especificada e o intervalo de **Hora da Última Falha** .<br /><br /> Você define o intervalo de **Hora da Última Falha** para exibir apenas as falhas de conexão que ocorreram durante um intervalo de datas. O intervalo pode abranger vários dias, meses ou anos.|  
|Detalhes|Mostra a cadeia de conexão, o número de execuções em que uma conexão falhou, e a data da última falha na conexão.|  
  
## <a name="all-operations-report"></a>Relatório Todas as Operações  
 O **Relatório Todas as Operações** exibe um resumo de todas as operações do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que foram executadas no servidor, inclusive implantação, validação e execução de pacotes e outras operações administrativas. Como no Painel do Integration Services, você pode aplicar um filtro à tabela para reduzir as informações exibidas.  
  
## <a name="all-validations-report"></a>Relatório Todas as Validações  
 O **Relatório Todas as Validações** exibe um resumo de todas as execuções do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que foram efetuadas no servidor. O resumo exibe informações para cada validação, como status, hora de início e hora de término. Cada entrada resumida inclui um link a mensagens geradas durante validação. Como no Painel do Integration Services, você pode aplicar um filtro à tabela para reduzir as informações exibidas.  
  
## <a name="custom-reports"></a>Relatórios personalizados  
 Você pode adicionar um relatório personalizado (arquivo .rdl) ao nó do catálogo do **SSISDB** no nó **Catálogos do Integration Services** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Antes de adicionar o relatório, confirme que você está usando uma convenção de nomenclatura de três partes para qualificar completamente os objetos que você referencia, por exemplo, uma tabela de origem. Caso contrário, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] exibirá um erro. A convenção de nomenclatura é \<database>.\<owner>.\<object>. Um exemplo seria SSISDB.internal.executions.  
  
> [!NOTE]  
>  Quando você adicionar relatórios personalizados ao nó do **SSISDB** , no nó **Bancos de Dados** , o prefixo do SSISDB não será necessário.  
  
 Para obter instruções sobre como criar e adicionar um relatório personalizado, consulte [Adicionar um relatório personalizado ao Management Studio](../ssms/object/add-a-custom-report-to-management-studio.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Exibir relatórios do servidor do Integration Services](../../2014/integration-services/view-reports-for-the-integration-services-server.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Monitorando execuções de pacotes e outras operações](performance/monitor-running-packages-and-other-operations.md)  
  
  
