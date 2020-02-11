---
title: Coleta de dados de uso do PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9057cb89-fb17-466e-a1ce-192c8ca20692
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46504906b13323ac4881ca2289e87e31f1cea72f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071084"
---
# <a name="powerpivot-usage-data-collection"></a>Coleta de dados de uso do PowerPivot
  A coleta de dados de uso é um recurso do SharePoint em nível de farm. O PowerPivot para SharePoint usa e estende esse sistema para fornecer relatórios no Painel de Gerenciamento PowerPivot que mostram como os dados e serviços PowerPivot são usados. Dependendo da forma como você instala o SharePoint, a coleta de dados de uso poderá ser desativada para o farm. Um administrador de farm deve habilitar o registro em log de uso para criar os dados de uso exibidos no Painel de Gerenciamento PowerPivot. Para obter mais informações sobre como habilitar e configurar a coleta de dados de uso para eventos do PowerPivot, consulte [Configurar coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 Para obter informações sobre os dados de uso no Painel de Gerenciamento PowerPivot, consulte [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
 **Neste tópico:**  
  
 [Coleta de dados de uso e arquitetura de relatórios](#usagearch)  
  
 [Fontes de dados de uso](#sources)  
  
 [Serviços e trabalhos de timer](#servicesjobs)  
  
 [Relatórios sobre dados de uso](#reporting)  
  
##  <a name="usagearch"></a>Coleta de dados de uso e arquitetura de relatórios  
 Dados de uso do PowerPivot são coletados, armazenados e gerenciados usando uma combinação de recursos da infraestrutura do SharePoint e componentes de servidor do PowerPivot. A infraestrutura do SharePoint fornece um serviço de uso centralizado e trabalhos de timer internos. O PowerPivot para SharePoint adiciona o repositório de prazo mais longo para dados de uso do PowerPivot e relatórios exibidos na Administração Central do SharePoint.  
  
 No sistema de coleta de dados de uso, informações de evento inserem o sistema de coleção de uso no servidor de aplicativos ou front-end da Web. Dados de uso se movem pelo sistema em resposta a trabalhos de timer que levam dados a se moverem de arquivos de dados temporários no servidor físico para o repositório persistente em um servidor de banco de dados. O diagrama a seguir ilustra os componentes e processos que movem dados de uso pela coleta de dados e pelo sistema de relatórios.  
  
 **Observação:** Verifique se a coleta de dados de uso está habilitada. Para verificar, vá para **Monitoramento** na Administração Central do SharePoint. Para obter mais informações, consulte [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 ![Componentes e processos de coleta de dados de uso.](../media/gmni-usagedata.gif "Componentes e processos de coleta de dados de uso.")  
  
|Fase|DESCRIÇÃO|  
|-----------|-----------------|  
|1|A coleta de dados de uso é disparada por eventos gerados pelos componentes do PowerPivot e provedores de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nas implantações do SharePoint. Eventos configuráveis que podem ser ativados ou desativados incluem solicitações de conexão, solicitações de carga/descarga e eventos de tempo de resposta de consulta que são monitorados pelo serviço PowerPivot no servidor de aplicativos. Outros eventos que são gerenciados somente pelo servidor e não podem ser desativados. Entre eles estão eventos de atualização de dados e de integridade do servidor.<br /><br /> Inicialmente, os dados de uso são coletados e armazenados em arquivos de log locais usando os recursos de coleta de dados do sistema do SharePoint. Os arquivos e sua localização fazem parte do sistema de coleta de dados de uso padrão no SharePoint. A localização dos arquivos é a mesma em todos os servidores do farm. Para exibir ou modificar o local do diretório de log, vá para **Monitoramento** na Administração Central do SharePoint e clique em **Configurar coleta de dados de integridade e uso**.|  
|2|Em intervalos agendados (a cada hora, por padrão), o trabalho de timer Importação de Dados de Uso do Microsoft SharePoint Foundation move os dados de uso dos arquivos locais para o banco de dados de aplicativo de serviço PowerPivot. Se você tiver vários aplicativos de serviço PowerPivot em um farm, cada um deles terá seu próprio banco de dados. Os eventos incluem informações internas que identificam qual aplicativo de serviço PowerPivot produziu o evento. Os identificadores de aplicativo verificam se dados de uso estão associados ao aplicativo que os criou.|  
|3|Dados são copiados em um banco de dados de relatórios internos que está disponível no Painel de Gerenciamento do PowerPivot em Administração Central.|  
|4|A fonte de dados é uma pasta de trabalho PowerPivot que você pode acessar para criar relatórios personalizados no Excel. Há somente uma instância da pasta de trabalho de origem. Todos os relatórios localizados baseiam-se na mesma pasta de trabalho de origem.|  
|5|Os dados de uso são apresentados em relatórios de aplicativos de serviço PowerPivot para administradores que gerenciam o desempenho e a disponibilidade do servidor. As instâncias localizadas das pastas de trabalho são criadas para os idiomas do SharePoint com suporte.<br /><br /> Para obter mais informações, consulte [Relatórios sobre dados de uso](#reporting) neste tópico.|  
  
##  <a name="sources"></a>Fontes de dados de uso  
 Quando a coleta de dados de uso está habilitada, dados são gerados para os eventos de servidor a seguir.  
  
|Evento|DESCRIÇÃO|Configurável|  
|-----------|-----------------|------------------|  
|conexões|Conexões de servidor feitas em nome de um usuário que está consultando dados PowerPivot em uma pasta de trabalho do Excel. Eventos de conexão identificam quem abriu uma conexão com uma pasta de trabalho PowerPivot. Em relatórios, estas informações são usadas para identificar os usuários mais frequentes, as fontes de dados PowerPivot que são acessadas pelos mesmos usuários e tendências em conexões com o passar do tempo.|Você pode habilitar e desabilitar [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Tempos de resposta de consulta|Estatísticas de resposta de consulta com base no tempo que levam para serem concluídas. As estatísticas de resposta de consulta mostram padrões em relação ao tempo que o servidor leva para responder a solicitações de consulta.|Você pode habilitar e desabilitar [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Carregamento de dados|Operações de carregamento de dados pelo [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Eventos de carregamento de dados identificam quais fontes de dados são usadas com mais frequência.|Você pode habilitar e desabilitar [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Descarregamento de dados|Operações de descarregamento de dados através de aplicativos de serviço PowerPivot. Um [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] descarregará fontes de dados inativas do PowerPivot se elas não estiverem sendo usadas ou quando o servidor estiver sob pressão de memória ou precisar de mais memória para executar trabalhos de atualização de dados.|Você pode habilitar e desabilitar [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Integridade do servidor|Operações de servidor que indicam a integridade do servidor, medidas na utilização da CPU e de memória. Estes dados são históricos. Eles não fornecem informações em tempo real sobre a carga de processamento atual no servidor.|Não. Dados de uso sempre são coletados para este evento.|  
|Atualização dedados|Operações de atualização de dados iniciadas pelo serviço PowerPivot para atualizações de dados agendadas. O histórico de uso da atualização de dados é coletado em nível de aplicativo para relatórios operacionais e é refletido nas páginas Gerenciar Atualização de Dados para pastas de trabalho individuais.<br /><br /> **Observação:** Para [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] implantações do e do SharePoint 2013, a atualização de dados é gerenciada pelos serviços do Excel e não pelo servidor Analysis Services.|Não. Dados de uso de atualização de dados sempre são coletados quando você habilita a atualização de dados para o aplicativo de serviço PowerPivot.|  
  
##  <a name="servicesjobs"></a>Serviços e trabalhos de timer  
 A tabela a seguir descreve os serviços e os armazenamentos de coleta de dados no sistema de coleta de dados de uso. Para obter instruções sobre como substituir as agendas de trabalho de timer para forçar uma atualização de dados de integridade do servidor e dados de uso nos relatórios do painel de gerenciamento PowerPivot, consulte [atualização de dados PowerPivot com o SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md). Os trabalhos de timer serão exibidos na Administração Central do SharePoint. Vá para **Monitoramento**e clique em **Verificar Status do Trabalho**. Clique em **examinar definições de trabalho**.  
  
|Componente|Cronograma padrão|DESCRIÇÃO|  
|---------------|----------------------|-----------------|  
|Serviço de timer do SharePoint (SPTimerV4)||Esse serviço do Windows é executado localmente em cada computador membro do farm e processa todos os trabalhos de timer definidos em nível de farm.|  
|Importação de Dados de Uso do Microsoft SharePoint Foundation|A cada 30 minutos no SharePoint 2010. A cada 5 minutos no SharePoint 2013.|Esse trabalho de timer é configurado globalmente no nível do farm. Ele move dados de uso de arquivos de log de uso locais para o banco de dados de coleta de dados de uso central. É possível executar esse trabalho de timer manualmente para forçar uma operação de importação de dados.|  
|Trabalho de timer de processamento de dados de uso do Microsoft SharePoint Foundation|Diariamente às 3h|**(\*)** A partir do SQL Server 2012 PowerPivot para SharePoint, esse trabalho de tempo tem suporte para cenários de atualização ou migração em que você pode ter dados de uso mais antigos ainda nos bancos de dado de uso do SharePoint. A partir do SQL Server 2012 PowerPivot para SharePoint, o banco de dados de uso do SharePoint não é usado para o fluxo de trabalho de coleta de uso do PowerPivot e do painel de gerenciamento. Os trabalhos de timer podem ser executados manualmente para mover todos os dados restantes relacionados ao PowerPivot do banco de dados de uso do SharePoint para os bancos de dados de aplicativo de serviço PowerPivot.<br /><br /> Esse trabalho de timer é configurado globalmente no nível do farm. Ele verifica dados de uso expirados no banco de dados de coleta de dados de uso central (ou seja, qualquer registro com mais de 30 dias). Para servidores do PowerPivot no farm, este trabalho de timer executa uma verificação adicional para dados de uso do PowerPivot. Quando dados de uso do PowerPivot são detectados, o trabalho de timer move os dados para um banco de dados de aplicativo de serviço usando um identificador de aplicativo para localizar o banco de dados correto.<br /><br /> É possível executar esse trabalho de timer manualmente para forçar uma verificação nos dados expirados ou uma importação dos dados de uso do PowerPivot para um banco de dados de aplicativo de serviço PowerPivot.|  
|Trabalho de Timer do Processamento de Painel de Gerenciamento PowerPivot|Diariamente às 3h|Esse trabalho de timer atualiza a pasta de trabalho PowerPivot interna, que fornece dados administrativos ao Painel de Gerenciamento do PowerPivot. Ele obtém informações atualizadas que são gerenciadas pelo SharePoint, inclusive nomes de servidores, nomes de usuários, nomes de aplicativos e nomes de arquivos que aparecem em relatórios de painel de gerenciamento ou em Web Parts.|  
  
##  <a name="reporting"></a>Relatórios sobre dados de uso  
 Para exibir dados de uso sobre dados PowerPivot, é possível exibir relatórios internos no Painel de Gerenciamento do PowerPivot. Os relatórios internos consolidam dados de uso que são recuperados de estruturas de dados de relatórios no banco de dados de aplicativo de serviço. Como os dados de relatório subjacentes são atualizados diariamente, os relatórios de uso internos só mostrarão informações atualizadas depois que o trabalho de timer de Processamento de Dados de Uso do Microsoft SharePoint Foundation copiar dados em um banco de dados do aplicativo de serviço PowerPivot. Por padrão, isso ocorre uma vez por dia.  
  
 Para obter mais informações sobre como exibir relatórios, consulte [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Painel de gerenciamento PowerPivot e dados de uso](power-pivot-management-dashboard-and-usage-data.md)   
 [Referência de definição de configuração &#40;PowerPivot para SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Configurar a coleta de dados de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
