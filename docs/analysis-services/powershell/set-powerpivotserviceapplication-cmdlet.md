---
title: Cmdlet Set-PowerPivotServiceApplication | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 16d10e2d-d7e1-40f1-bc9d-a4e10c61af95
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0def855b93ce209aa923fd57e60d01c142a7fd0d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="set-powerpivotserviceapplication-cmdlet"></a>Cmdlet Set-PowerPivotServiceApplication
  
 [!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)] 

  Define as propriedades de um aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Set-PowerPivotServiceApplication [-Identity] <SPGeminiServiceApplicationPipeBind> [-AdministrationConnectionPoolSize <int>] [-AllowCustomWindowsCredentials] [-BusinessHoursEndTime <string>] [-BusinessHoursStartTime <string>] [-CachedDatabaseholdLimit <int>] [-Confirm <switch>] [-ConnectionPoolSize <int>] [-ConnectionPoolTimeout <int>] [-DataLoadTimeout <int>] [-DataRefreshFailureThreshold <int>] [-DataRefreshInactiveWorkbooksThreshold <int>] [-DataRefreshMaxHistory <int>] [-HealthBasedAllocation <switch>] [-LoadsToConnectionsRatioCollectionInterval <int>] [-LoadsToConnectionsRatioLimit <int>] [-MemoryDatabaseHoldLimit <int>] [-QueryReportingInterval <int>] [-RoundRobinAllocation <switch>] [-UnattendedAccount <string>] [-UsageDataRetentionPeriod <int>] [-UsageExpectedResponseUpperLimit <int>] [-UsageLongResponseUpperLimit <int>] [-UsageQuickResponseUpperLimit <int>] [-UsageTrivialResponseUpperLimit <int>] [-UsageUpdateDayLimit <int>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet Set-PowerPivotServiceApplication atualiza as propriedades de um aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. O parâmetro Identity é necessário. Você deve fornecer o GUID do aplicativo de serviço para o qual está atualizando as propriedades.  
  
 Para verificar as alterações, execute o seguinte cmdlet: Get-PowerPivotServiceApplication-Identity \<GUID > | format-list.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>-Identity \<SPGeminiServiceApplicationPipeBind >  
 Especifica o aplicativo de serviço a ser atualizado. O tipo deve ser um GUID válido ou uma instância de um objeto de aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] válido. Você pode usar Get-PowerPivotServiceApplication para retornar uma instância do objeto.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-administrationconnectionpoolsize-int"></a>-AdministrationConnectionPoolSize \<int >  
 Especifica o número de conexões abertas em um pool de conexões criado para uma conexão de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] com o Analysis Services. Cada instância de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] abre uma conexão administrativa separada para a instância do Analysis Services no mesmo computador. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cria um pool separado para reutilizar conexões administrativas com a finalidade de verificar conexões ociosas e monitorar a integridade do servidor. O valor padrão é de 200 conexões. Os valores válidos são -1 (ilimitado), 0 (desabilita pool de conexões administrativas) ou 1 a 10000. Se você selecionar 0, todas as conexões serão recriadas.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|200|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-allowcustomwindowscredentials-switchparameter"></a>-AllowCustomWindowsCredentials [\<SwitchParameter >]  
 Especifica se os proprietários do agendamento podem inserir credenciais arbitrárias do Windows para executar um agendamento de atualização de dados. Se você marcar essa caixa de seleção, o aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] criará e gerenciará um aplicativo de destino para cada conjunto de credenciais armazenadas. O padrão é definido como true. Para desativar esse recurso, defina AllowCustomWindowsCredentials:$false.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-businesshoursendtime-string"></a>-BusinessHoursEndTime \<cadeia de caracteres >  
 Especifica o ponto final em um intervalo de horas que define um dia útil. Os agendamentos de atualização de dados podem ser realizados depois do fim de um dia útil para escolher dados transacionais que foram gerados durante o horário comercial normal. O padrão é 8:00 p.m.  Valores válidos são especificados entre aspas, no formato a.m. ou p.m. (por exemplo, "08:00PM". O intervalo de horas deve ficar entre 1 e 12. O intervalo de minutos deve ficar entre 1 e 59.  
  
 Para especificar o intervalo total de horas de um dia útil, você deve definir BusinessHoursStartTime e BusinessHoursEndTime. Os dois parâmetros definem o intervalo de horas que constituem um dia útil.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|8 PM|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-businesshoursstarttime-string"></a>-BusinessHoursStartTime \<cadeia de caracteres >  
 Especifica o ponto inicial em um intervalo de horas que define um dia útil. Os agendamentos de atualização de dados podem ser realizados depois do fim de um dia útil para escolher dados transacionais que foram gerados durante o horário comercial normal. O padrão é 4:00 a.m.  Valores válidos são especificados entre aspas, no formato a.m. ou p.m. (por exemplo, "04:00AM". O intervalo de horas deve ficar entre 1 e 12. O intervalo de minutos deve ficar entre 1 e 59.  
  
 Para especificar o intervalo total de horas de um dia útil, você deve definir BusinessHoursStartTime e BusinessHoursEndTime. Os dois parâmetros definem o intervalo de horas que constituem um dia útil.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|4 AM|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-cacheddatabaseholdlimit-int"></a>-CachedDatabaseholdLimit \<int >  
 Especifica a quantidade de horas que um banco de dados Inativo permanece no sistema de arquivos depois de ser descarregado da memória. O padrão é 120 horas. O trabalho de limpeza usa esta configuração para determinar os arquivos a serem excluídos. Todos os bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que estiverem inativos por 168 horas (48 horas em memória e 120 horas no cache) serão excluídos do disco pelo trabalho de limpeza.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|120|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-confirm-switch"></a>-Confirme \<alternar >  
 Solicita sua confirmação antes de executar o comando. Este valor é habilitado por padrão. Para ignorar a resposta de confirmação em um comando, especifique Confirm:$false no comando.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-connectionpoolsize-int"></a>-ConnectionPoolSize \<int >  
 Especifica o número máximo de conexões ociosas que o serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] criará em pools de conexões individuais para cada usuário do SharePoint, conjunto de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e combinações de versão. O valor padrão é de 1000 conexões ociosas. Os valores válidos são -1 (ilimitado), 0 (desabilita pool de conexões do usuário) ou de 1 a 10000. Esses pools de conexões permitem que o serviço dê suporte mais eficiente a conexões contínuas para os mesmos dados somente leitura pelo mesmo usuário. Se você desabilitar o pooling de conexão, todas as conexões serão recriadas. Observe que a alteração do limite no tamanho do pool de conexões, inclusive a definição como 0, não resultará em conexões removidas. Há pools de conexões para reduzir tempos de espera durante a conexão com os dados. O serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nunca negará uma conexão com base nas configurações do pool de conexões.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|1.000|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-connectionpooltimeout-int"></a>-ConnectionPoolTimeout \<int >  
 Especifica por quantos minutos uma conexão de dados ociosa permanecerá aberta. O valor padrão é 1.800 segundos (ou 30 minutos). Durante esse período, o aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] reutilizará uma conexão de dados ociosa para solicitações somente leitura do mesmo usuário do SharePoint aos mesmos dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se nenhuma solicitação adicional for recebida para obter esses dados durante o período especificado, a conexão será removida do pool. Os valores válidos são de 1 a 3.600 segundos.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|1800|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-dataloadtimeout-int"></a>-DataLoadTimeout \<int >  
 Especifica quanto tempo o aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aguarda uma resposta da instância do SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) para a qual encaminhou uma solicitação de carregamento de dados. Como conjuntos de dados muito grandes levam muito tempo para serem transferidos eletronicamente, você deve aguardar um tempo suficiente para que a instância de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] recupere a pasta de trabalho do Excel e mova os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para uma instância do Analysis Services para processamento da consulta. O valor padrão é 1.800 segundos (ou 30 minutos). Os valores válidos variam de 1 a 3.600 segundos.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|1800|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-datarefreshfailurethreshold-int"></a>-DataRefreshFailureThreshold \<int >  
 Especifica o número de falhas sucessivas após o qual um agendamento é desabilitado. O padrão é 10. Você também pode inserir 0 para nunca desabilitar um agendamento devido a falhas de atualização.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|10|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-datarefreshinactiveworkbooksthreshold-int"></a>-DataRefreshInactiveWorkbooksThreshold \<int >  
 Especifique o número de ciclos de atualização de dados após o qual um agendamento é desabilitado ou insira 0 para nunca desabilitar um agendamento devido à inatividade. O padrão é 10 ciclos.  
  
 A inatividade da pasta de trabalho é medida como a ausência de eventos de conexão em vários ciclos de atualização de dados. Um ciclo de atualização de dados é contado cada vez que uma operação de atualização de dados é disparada (pela agenda ou uma operação Executar Agora), independentemente de a operação ser bem-sucedida ou apresentar falhas. Se vários ciclos passarem (10 por padrão) sem solicitações de conexão para a pasta de trabalho, a agenda de atualização de dados será desabilitada em função da inatividade.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|10|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-datarefreshmaxhistory-int"></a>-DataRefreshMaxHistory \<int >  
 Especifica quanto tempo manter um registro histórico de processamento de atualização de dados. Essas informações aparecem nas páginas do histórico de atualização de dados mantidas para cada pasta de trabalho que usa atualização de dados. Elas também são exibidas no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O valor padrão é de 365 dias.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|365|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-healthbasedallocation-switch"></a>-HealthBasedAllocation \<alternar >  
 Especifica o algoritmo de alocação baseado em integridade que encaminha solicitações de conexão ao servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint que tem mais recursos de CPU e memória disponíveis. Esse é o algoritmo de alocação padrão. HealthBasedAllocation e RoundRobinBasedAllocation são mutuamente exclusivos. Você deve especificar um ou outro. Se você definir ambos como false, HealthBasedAllocation será usado porque é o padrão. Se você definir ambos como true, receberá um erro de validação. A sintaxe desses parâmetros inclui a inserção apenas do nome do parâmetro ou parameter:$true ou parameter:$false.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-loadstoconnectionsratiocollectioninterval-int"></a>-LoadsToConnectionsRatioCollectionInterval \<int >  
 Especifique o intervalo (em horas) para contagem de eventos de carregamento e conexão para calcular a proporção carregamento-para-conexão. Por padrão, o sistema calculará uma nova proporção a cada 4 horas. Os valores válidos são 1 a 24.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|4|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-loadstoconnectionsratiolimit-int"></a>-LoadsToConnectionsRatioLimit \<int >  
 Especifica a proporção de eventos de carregamento em relação a eventos de conexão, usada como um indicador de integridade de servidor. O padrão é 20%.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|20|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-memorydatabaseholdlimit-int"></a>-MemoryDatabaseHoldLimit \<int >  
 Especifica quantas horas um banco de dados inativo permanece na memória para atender novas solicitações desses dados. Um banco de dados ativo sempre será mantido em memória contanto que você esteja consultando-o, mas depois ele não permanecerá ativo. O sistema manterá o banco de dados em memória por um período de tempo adicional caso existam mais solicitações desses dados. O padrão é 48 horas.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|48|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-queryreportinginterval-int"></a>-QueryReportingInterval \<int >  
 Especifica o número de segundos para coleta de estatísticas de resposta à consulta antes de relatar isso como um evento de uso. O padrão é 300 segundos.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|300|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-roundrobinallocation-switch"></a>-RoundRobinAllocation \<alternar >  
 Especifica o algoritmo de alocação round robin que encaminha solicitações de conexão ao seguinte servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, alternando solicitações igualmente entre os servidores disponíveis, independentemente da carga do servidor. HealthBasedAllocation e RoundRobinBasedAllocation são mutuamente exclusivos. Você deve especificar um ou outro. Se você definir ambos como false, HealthBasedAllocation será usado porque é o padrão. Se você definir ambos como true, receberá um erro de validação. A sintaxe desses parâmetros inclui a inserção apenas do nome do parâmetro ou parameter:$true ou parameter:$false.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-unattendedaccount-string"></a>-UnattendedAccount \<cadeia de caracteres >  
 Especifica o nome do aplicativo de destino de um aplicativo de Serviço de Repositório Seguro que armazena uma conta predefinida para execução de trabalhos de atualização de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-usagedataretentionperiod-int"></a>-UsageDataRetentionPeriod \<int >  
 Especifica o número de dias para manter um histórico de dados de uso e estatísticas de integridade de servidor. O padrão é 365 dias. A definição desse valor como 0 mantém todo o histórico indefinidamente.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|365|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-usageexpectedresponseupperlimit-int"></a>-UsageExpectedResponseUpperLimit \<int >  
 Define um limite superior que define uma troca de solicitação-resposta esperada. O padrão é 3.000 milissegundos. Qualquer solicitação concluída entre 1.000 e 3.000 milissegundos é considerada uma resposta esperada para fins de relatórios.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|3000|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-usagelongresponseupperlimit-int"></a>-UsageLongResponseUpperLimit \<int >  
 Define um limite superior que define uma troca de solicitação-resposta demorada.  O limite superior é 10.000 milissegundos. Qualquer solicitação que exceda esse limite superior entrará na categoria Excedida, que não tem limite superior.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|10000|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-usagequickresponseupperlimit-int"></a>-UsageQuickResponseUpperLimit \<int >  
 Define um limite superior que define uma troca de solicitação-resposta rápida. O padrão é 1.000 milissegundos. Qualquer solicitação concluída entre 500 e 1.000 milissegundos é considerada uma resposta rápida para fins de relatórios.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|1.000|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-usagetrivialresponseupperlimit-int"></a>-UsageTrivialResponseUpperLimit \<int >  
 Especifica uma categoria de tempos de resposta muito pequenos para serem considerados relevantes para fins de coleta de dados. A maioria das respostas nessa categoria é constituída por comunicação de servidor-para-servidor. Por padrão, esse valor é 500 milissegundos. Qualquer solicitação concluída entre 0 e 500 milissegundos é uma solicitação trivial e ignorada para fins de relatórios.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|500|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-usageupdatedaylimit-int"></a>-UsageUpdateDayLimit \<int >  
 Especifique o limite (em dias) para o disparo de um aviso sobre uma falha para atualizar o arquivo de dados usado pelos relatórios no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Por padrão, o sistema atualiza os dados de uso diariamente. O arquivo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Management Dashboard.xlsx, que é a fonte de dados para relatórios administrativos, é atualizado de acordo com o mesmo agendamento. Se o arquivo .xlsx não for atualizado durante um determinado número de dias, uma regra de integridade será disparada, indicando que o arquivo está desatualizado. O padrão é 5 dias. Os valores válidos são 1 a 30.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|5|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer e OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -AllowCustomWindowsCredentials:$false -UnattendedAccount "MyTargetApp"  
```  
  
 Esse exemplo desativa um recurso de atualização de dados que cria automaticamente e gerencia aplicativos de destino do Serviço de Repositório Seguro para armazenar credenciais arbitrárias do Windows. Também define a conta de atualização autônoma de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para um aplicativo de destino predefinido.  
  
 Use Get-powerpivotserviceapplication para obter uma identidade válida.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -HealthBasedAllocation  
```  
  
 Este exemplo especifica o algoritmo de alocação baseado em integridade que encaminha solicitações de conexão ao servidor que tem mais recursos disponíveis.  
  
 Use Get-powerpivotserviceapplication para obter uma identidade válida.  
  
## <a name="example-3"></a>Exemplo 3  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklmn -BusinessHoursStartTime "07:15AM" -BusinessHoursEndTime "08:00PM"  
```  
  
 Este exemplo mostra como definir as horas de início e término de um dia útil, usado como opção de agendamento para agendar uma atualização de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Os agendamentos podem especificar uma opção de horário após o expediente para a execução da atualização de dados no fim de um dia útil.  
  
 Use Get-powerpivotserviceapplication para obter uma identidade válida.  
  
  
