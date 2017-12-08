---
title: Power Pivot Usage Data Collection | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9057cb89-fb17-466e-a1ce-192c8ca20692
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a5fab455ddd2ea659f2269512a81c93df2962df2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="power-pivot-usage-data-collection"></a>Coleta de dados de uso do PowerPivot
  A coleta de dados de uso é um recurso do SharePoint em nível de farm. [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint usa e estende esse sistema para fornecer relatórios no Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que mostram como os dados e serviços do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] são usados. Dependendo da forma como você instala o SharePoint, a coleta de dados de uso poderá ser desativada para o farm. Um administrador de farm deve habilitar o registro em log de uso para criar os dados de uso exibidos no Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .  
  
 Para obter informações sobre os dados de uso no Painel de Gerenciamento [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , consulte [Painel de Gerenciamento Power Pivot e dados de uso](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
  
##  <a name="usagearch"></a> Coleta de dados de uso e arquitetura de relatórios  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]dados de uso são coletados, armazenados e gerenciados usando uma combinação de recursos da infraestrutura do SharePoint e componentes de servidor do PowerPivot. A infraestrutura do SharePoint fornece um serviço de uso centralizado e trabalhos de timer internos. [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint adiciona o repositório de prazo mais longo para dados de uso do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] e relatórios exibidos na Administração Central do SharePoint.  
  
 No sistema de coleta de dados de uso, informações de evento inserem o sistema de coleção de uso no servidor de aplicativos ou front-end da Web. Dados de uso se movem pelo sistema em resposta a trabalhos de timer que levam dados a se moverem de arquivos de dados temporários no servidor físico para o repositório persistente em um servidor de banco de dados. O diagrama a seguir ilustra os componentes e processos que movem dados de uso pela coleta de dados e pelo sistema de relatórios.  
  
 **Observação:** Verifique se a coleta de dados de utilização está habilitada. Para verificar, vá para **Monitoramento** na Administração Central do SharePoint. Para obter mais informações, consulte [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 ![Componentes e processos de coleta de dados de uso. ] (../../analysis-services/power-pivot-sharepoint/media/gmni-usagedata.gif "Componentes e processos de coleta de dados de uso.")  
  
|Fase|Description|  
|-----------|-----------------|  
|1|A coleta de dados de uso é disparada por eventos gerados pelos componentes do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] e provedores de dados do [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] nas implantações do SharePoint. Eventos configuráveis que podem ser ativados ou desativados incluem solicitações de conexão, solicitações de carregamento e descarregamento e eventos de tempo de resposta de consulta que são monitorados pelo serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] no servidor de aplicativos. Outros eventos que são gerenciados somente pelo servidor e não podem ser desativados. Entre eles estão eventos de atualização de dados e de integridade do servidor.<br /><br /> Inicialmente, os dados de uso são coletados e armazenados em arquivos de log locais usando os recursos de coleta de dados do sistema do SharePoint. Os arquivos e sua localização fazem parte do sistema de coleta de dados de uso padrão no SharePoint. A localização dos arquivos é a mesma em todos os servidores do farm. Para exibir ou modificar o local do diretório de log, vá para **Monitoramento** na Administração Central do SharePoint e clique em **Configurar coleta de dados de integridade e uso**.|  
|2|Em intervalos agendados (a cada hora, por padrão), o trabalho do temporizador Importação de Dados de Uso do Microsoft SharePoint Foundation move os dados de uso dos arquivos locais para o banco de dados de aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Se você tiver vários aplicativos de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] em um farm, cada um deles terá seu próprio banco de dados. Os eventos incluem informações internas que identificam qual aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] produziu o evento. Os identificadores de aplicativo verificam se dados de uso estão associados ao aplicativo que os criou.|  
|3|Dados são copiados em um banco de dados de relatórios internos que está disponível no Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] na Administração Central.|  
|4|A fonte de dados é uma pasta de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que você pode acessar para criar relatórios personalizados no Excel. Há somente uma instância da pasta de trabalho de origem. Todos os relatórios localizados baseiam-se na mesma pasta de trabalho de origem.|  
|5|Os dados de uso são apresentados em relatórios de aplicativos de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para administradores que gerenciam o desempenho e a disponibilidade do servidor. As instâncias localizadas das pastas de trabalho são criadas para os idiomas do SharePoint com suporte. Para obter mais informações, consulte [Relatórios sobre dados de uso](#reporting) neste tópico.|  
  
##  <a name="sources"></a> Fontes de dados de uso  
 Quando a coleta de dados de uso está habilitada, dados são gerados para os eventos de servidor a seguir.  
  
|Evento|Description|Configurável|  
|-----------|-----------------|------------------|  
|Conexões|Conexões de servidor feitas em nome de um usuário que está consultando dados do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] em uma pasta de trabalho do Excel. Eventos de conexão identificam quem abriu uma conexão com uma pasta de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Em relatórios, estas informações são usadas para identificar os usuários mais frequentes, as fontes de dados do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que são acessadas pelos mesmos usuários e tendências em conexões com o passar do tempo.|Você pode habilitar e desabilitar [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Tempos de resposta de consulta|Estatísticas de resposta de consulta com base no tempo que levam para serem concluídas. As estatísticas de resposta de consulta mostram padrões em relação ao tempo que o servidor leva para responder a solicitações de consulta.|Você pode habilitar e desabilitar [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Carregamento de dados|Operações de carregamento de dados pelo [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Eventos de carregamento de dados identificam quais fontes de dados são usadas com mais frequência.|Você pode habilitar e desabilitar [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Descarregamento de dados|Operações de descarregamento de dados através de aplicativos de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Um [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] descarregará fontes de dados inativas do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] se elas não estiverem sendo usadas ou quando o servidor estiver sob pressão de memória ou precisar de mais memória para executar trabalhos de atualização de dados.|Você pode habilitar e desabilitar [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Integridade do servidor|Operações de servidor que indicam a integridade do servidor, medidas na utilização da CPU e de memória. Estes dados são históricos. Eles não fornecem informações em tempo real sobre a carga de processamento atual no servidor.|Nenhum. Dados de uso sempre são coletados para este evento.|  
|Atualização de dados|Operações de atualização de dados iniciadas pelo serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para atualizações de dados agendadas. O histórico de uso da atualização de dados é coletado em nível de aplicativo para relatórios operacionais e é refletido nas páginas Gerenciar Atualização de Dados para pastas de trabalho individuais.<br /><br /> **Observação:** Para o [!INCLUDE[ssSQL11SP1_md](../../includes/sssql11sp1-md.md)] e as implantações do SharePoint 2013, a atualização de dados é gerenciada pelos Serviços do Excel, e não pelo servidor do Analysis Services.|Nenhum. Dados de uso de atualização de dados sempre são coletados quando você habilita a atualização de dados para o aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .|  
  
##  <a name="servicesjobs"></a> Serviços e trabalhos de timer  
 A tabela a seguir descreve os serviços e os armazenamentos de coleta de dados no sistema de coleta de dados de uso. Para obter instruções sobre como substituir os agendamentos de trabalho de timer forçar uma atualização de dados de dados de uso e integridade do servidor em [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] relatórios do painel de gerenciamento, consulte [Inserir link da descrição aqui](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md). Os trabalhos de timer serão exibidos na Administração Central do SharePoint. Vá para **Monitoramento**e clique em **Verificar Status do Trabalho**. Clique em **Revisar Definições de Trabalho**.  
  
|Componente|Cronograma padrão|Description|  
|---------------|----------------------|-----------------|  
|Serviço de timer do SharePoint (SPTimerV4)||Esse serviço do Windows é executado localmente em cada computador membro do farm e processa todos os trabalhos de timer definidos em nível de farm.|  
|Importação de Dados de Uso do Microsoft SharePoint Foundation|A cada 30 minutos no SharePoint 2010. A cada 5 minutos no SharePoint 2013.|Esse trabalho de timer é configurado globalmente no nível do farm. Ele move dados de uso de arquivos de log de uso locais para o banco de dados de coleta de dados de uso central. É possível executar esse trabalho de timer manualmente para forçar uma operação de importação de dados.|  
|Trabalho de timer de processamento de dados de uso do Microsoft SharePoint Foundation|Diariamente às 3h|Do SQL Server 2012 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint em diante, há suporte para este trabalho do temporizador nos cenários de atualização ou migração em que ainda possa haver dados de uso antigos nos bancos de dados de uso do SharePoint. Do SQL Server 2012 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint em diante, o banco de dados de uso do SharePoint não é usado para o fluxo de trabalho de coleta de uso do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] e do painel de gerenciamento. Os trabalhos do temporizador podem ser executados manualmente para mover todos os dados restantes relacionados ao [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] do banco de dados de uso do SharePoint para os bancos de dados de aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .<br /><br /> Esse trabalho de timer é configurado globalmente no nível do farm. Ele verifica dados de uso expirados no banco de dados de coleta de dados de uso central (ou seja, qualquer registro com mais de 30 dias). Para servidores do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] no farm, este trabalho do temporizador executa uma verificação adicional para dados de uso do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Quando dados de uso do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] são detectados, o trabalho do temporizador move os dados para um banco de dados de aplicativo de serviço usando um identificador de aplicativo para localizar o banco de dados correto.<br /><br /> É possível executar esse trabalho do temporizador manualmente para forçar uma verificação nos dados expirados ou uma importação dos dados de uso do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para um banco de dados de aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .|  
|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Trabalho do temporizador do Processamento de Painel de Gerenciamento|Diariamente às 3h|Esse trabalho de temporizador atualiza a pasta de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] interna, que fornece dados administrativos ao Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Ele obtém informações atualizadas que são gerenciadas pelo SharePoint, inclusive nomes de servidores, nomes de usuários, nomes de aplicativos e nomes de arquivos que aparecem em relatórios de painel de gerenciamento ou em Web Parts.|  
  
##  <a name="reporting"></a> Relatórios sobre dados de uso  
 Para exibir dados de uso sobre dados do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , é possível exibir relatórios internos no Painel de Gerenciamento do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Os relatórios internos consolidam dados de uso que são recuperados de estruturas de dados de relatórios no banco de dados de aplicativo de serviço. Como os dados de relatório subjacentes são atualizados diariamente, os relatórios de uso internos só mostrarão informações atualizadas depois que o trabalho do temporizador de Processamento de Dados de Uso do Microsoft SharePoint Foundation copiar dados em um banco de dados do aplicativo de serviço [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Por padrão, isso ocorre uma vez por dia.  
  
 Para obter mais informações sobre como exibir relatórios, consulte [Painel de Gerenciamento Power Pivot e dados de uso](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
## <a name="see-also"></a>Consulte também  
 [Painel de Gerenciamento Power Pivot e dados de uso](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)   
 [Referência de parâmetro de configuração &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
