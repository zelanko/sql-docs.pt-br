---
title: 'Lista de verificação: Usar o PowerShell para verificar o PowerPivot para SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 73a13f05-3450-411f-95f9-4b6167cc7607
caps.latest.revision: 21
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: a7d62eaa7acda26384b3bf8eb7dbb49af3ab5096
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122516"
---
# <a name="checklist-use-powershell-to-verify-powerpivot-for-sharepoint"></a>Lista de verificação: use o PowerShell para verificar o PowerPivot para SharePoint
  Nenhuma instalação do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] ou operação de recuperação será completa sem um teste de verificação rigoroso que confirme o funcionamento correto dos serviços e dos dados. Neste artigo, mostramos como executar essas etapas usando o Windows PowerShell. Colocamos cada etapa em sua própria seção para que você possa ir diretamente para as tarefas específicas. Por exemplo, execute o script na seção [Bancos de dados](#bkmk_databases) deste tópico para verificar o nome dos bancos de dados de conteúdo e aplicativo de serviço se quiser agendá-los para manutenção ou backup.  
  
|||  
|-|-|  
|![Conteúdo relacionado ao PowerShell](../../../reporting-services/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")|Um script completo do PowerShell é incluído na parte final do tópico. Use o script completo como ponto de partida para criar um script personalizado para fazer a auditoria da implantação completa do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].|  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **Neste tópico**: os itens indicados após o sumário correspondem às áreas do diagrama. O diagrama ilustra os  
  
|||  
|-|-|  
|[Preparar o ambiente do PowerShell](#bkmk_prerequisites)<br /><br /> [Sintomas e ações recomendadas](#bkmk_symptoms)<br /><br /> **(A)** [Serviço Windows do Analysis Services](#bkmk_windows_service)<br /><br /> **(B)** [PowerPivotSystemService e PowerPivotEngineSerivce](#bkmk_engine_and_system_service)<br /><br /> **(C)** [Aplicativos de serviço e proxies do PowerPivot](#bkmk_powerpivot_service_application)<br /><br /> **(D)** [Bancos de dados](#bkmk_databases)<br /><br /> [Recursos do SharePoint](#bkmk_features)<br /><br /> [Trabalhos de timer](#bkmk_timer_jobs)<br /><br /> [Regras de integridade](#bkmk_health_rules)<br /><br /> **(E)** [Logs do Windows e do ULS](#bkmk_logs)<br /><br /> [Provedor MSOLAP](#bkmk_msolap)<br /><br /> [Biblioteca de cliente ADOMD.Net](#bkmk_adomd)<br /><br /> [Regras de coleta de dados de integridade](#bkmk_health_collection)<br /><br /> [Soluções](#bkmk_solutions)<br /><br /> [Etapas de verificação manual](#bkmk_manual)<br /><br /> [Mais recursos](#bkmk_more_resources)<br /><br /> [Script completo do PowerShell](#bkmk_full_script)|![verificação de PowerShell do powerpivot](../../../sql-server/install/media/ssas-powershell-component-verification.png "verificação de powershell do powerpivot")|  
  
##  <a name="bkmk_prerequisites"></a> Preparar o ambiente do PowerShell  
 As etapas desta seção preparam o ambiente do PowerShell. As etapas podem não ser necessárias, dependendo de como o ambiente de script está configurado no momento.  
  
 **Permissões do PowerShell**  
  
 Abra uma janela do PowerShell ou o ISE (Ambiente de Script Integrado) do PowerShell com **privilégios administrativos**. Se você não tiver privilégios administrativos ao executar comandos, receberá uma mensagem de erro semelhante à seguinte:  
  
 Get-SPLogEvent: você precisa ter **privilégios de administrador** no computador para executar este cmdlet.  
  
 **Módulo do SharePoint e do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]**  
  
 Se uma mensagem de erro semelhante à seguinte for exibida quando você executar cmdlets relacionados ao SharePoint, execute o comando Add-PSSnapin:  
  
 O termo “Get-PowerPivotSystemService” **não é reconhecido como nome de um cmdlet**, uma função, um arquivo de script nem um programa operável. Verifique a ortografia do nome ou, se um caminho tiver sido incluído, verifique se ele está correto e tente novamente.  
  
```  
Add-PSSnapin Microsoft.Sharepoint.Powershell –EA 0  
```  
  
 **Windows PowerShell**  
  
 Para obter mais informações sobre o PowerShell ISE, consulte [Introdução ao Windows PowerShell ISE](http://technet.microsoft.com/library/dd315244.aspx) e [Usar o Windows PowerShell para administrar o SharePoint 2013](http://technet.microsoft.com/library/ee806878\(v=office.15\).aspx).  
  
|||  
|-|-|  
|![PowerPivot para sharepoint gerais do aplicativo conjunto](../../../sql-server/install/media/ssas-powerpivot-logo.png "powerpivot no conjunto de aplicativos em geral do sharepoint")|Se desejar, você pode verificar a maioria dos componentes na Administração Central, usando o painel de gerenciamento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Para abrir o painel na Administração Central, clique em **Configurações Gerais do Aplicativo**e clique em **Painel de Gerenciamento** no **PowerPivot**. Para obter mais informações sobre o painel de controle, consulte [PowerPivot Management Dashboard and Usage Data](../../power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).|  
  
##  <a name="bkmk_symptoms"></a> Sintomas e ações recomendadas  
 A tabela a seguir é uma lista de sintomas ou problemas e a ação sugerida deste tópico para ajudar você a resolver o problema.  
  
|Sintoma|Consulte a seção|  
|-------------|-----------------|  
|A atualização de dados não está em execução|Consulte a seção [Timer Jobs](#bkmk_timer_jobs) e verifique se o **Trabalho de timer online de atualização de dados PowerPivot** está online.|  
|Os dados do painel de gerenciamento são antigos|Consulte a seção [Trabalhos de timer](#bkmk_timer_jobs) e verifique se o **Trabalho de timer de processamento do painel de gerenciamento** está online.|  
|Algumas partes do Painel de Gerenciamento|Se você instalar o PowerPivot para SharePoint em um farm que tenha a topologia de Administração Central, sem Serviços do Excel ou PowerPivot para SharePoint, deverá baixar e instalar a biblioteca cliente do Microsoft ADOMD.NET se quiser acesso completo aos relatórios internos no painel de gerenciamento PowerPivot. Alguns relatórios no painel usam ADOMD.NET para acessar dados internos que fornecem dados de relação sobre o processamento de consultas do PowerPivot e a integridade de servidor no farm. Veja a seção [Biblioteca de cliente do ADOMD.Net](#bkmk_adomd) e o tópico [Instalar o ADOMD.NET em servidores Web front-end executando a Administração Central](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).|  
|\<conteúdo futuro >||  
  
##  <a name="bkmk_windows_service"></a> Serviço Windows do Analysis Services  
 O script nesta seção verifica a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Verifique se o serviço está **em execução**.  
  
```  
get-service | select name, displayname, status | where {$_.Name -eq "msolap`$powerpivot"} | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
Name              DisplayName                                Status  
----              -----------                                ------  
MSOLAP$POWERPIVOT SQL Server Analysis Services (POWERPIVOT) Running  
```  
  
##  <a name="bkmk_engine_and_system_service"></a> PowerPivotSystemService e PowerPivotEngineSerivce  
 Os scripts desta seção verificam os serviços de sistema do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] . Há um serviço de sistema para uma implantação do SharePoint 2013 e dois serviços para uma implantação do SharePoint 2010.  
  
 **PowerPivotSystemService**  
  
 Verifique se o status é **Online**.  
  
```  
Get-PowerPivotSystemService | select typename, status, applications, farm | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
TypeName                                  Status Applications                             Farm  
--------                                  ------ ------------                             ----  
SQL Server PowerPivot Service Application Online {Default PowerPivot Service Application} SPFarm Name=SharePoint_Config_77d8ab0744a34e8aa27c806a2b8c760c  
```  
  
 **PowerPivotEngineSerivce**  
  
> [!NOTE]  
>  **Ignore este script se** você estiver usando o SharePoint 2013. O PowerPivotEngineService não faz parte de uma implantação do SharePoint 2013. Se você executar o cmdlet Get-PowerPivot**Engine**Service no SharePoint 2013, receberá uma mensagem de erro semelhante à seguinte. Essa mensagem de erro será retornada mesmo se você tiver executado o comando Add-PSSnapin descrito na seção de pré-requisitos deste tópico.  
>   
>  O termo 'Get-PowerPivotEngineService' não é reconhecido como o nome de um cmdlet  
  
 Em uma implantação do SharePoint 2010, verifique se o status é **Online**.  
  
```  
Get-PowerPivotEngineService | select typename, status, name, instances, farm | format-table -property * -autosize | out-default   
```  
  
 **Exemplo de saída**  
  
```  
TypeName  : SQL Server Analysis Services  
Status    : Online  
Name      : MSOLAP$POWERPIVOT  
Instances : {POWERPIVOT}  
Farm      : SPFarm Name=SharePoint_Config  
```  
  
##  <a name="bkmk_powerpivot_service_application"></a> Aplicativos de serviço PowerPivot e proxies  
 Verifique se o status é **Online**. O aplicativo de Serviços do Excel não usa uma banco de dados de aplicativo de serviço e, portanto, o cmdlet não retorna um nome de banco de dados. Observe o banco de dados usado pelo aplicativo de serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , para que você possa verificar se o banco de dados está online na seção de banco de dados mais adiante neste tópico.  
  
 **O PowerPivot e aplicativos de serviço do Excel**  
  
 Em uma implantação do SharePoint 2010, verifique se o status é **Online**.  
  
```  
Get-PowerPivotServiceApplication | select typename,name, status, unattendedaccount, applicationpool, farm, database  
Get-SPExcelServiceApplication | select typename, DisplayName, status  
```  
  
 **Exemplo de saída**  
  
```  
TypeName          : PowerPivot Service Application  
Name              : PowerPivotServiceApplication1  
Status            : Online  
UnattendedAccount : PowerPivotUnattendedAccount  
ApplicationPool   : SPIisWebServiceApplicationPool Name=sqlbi_serviceapp  
Farm              : SPFarm Name=SharePoint_Config  
Database          : GeminiServiceDatabase Name=PowerPivotServiceApplication1_19648f3f2c944e27acdc6c20aab8487a  
  
TypeName    : Excel Services Application Web Service Application  
DisplayName : Excel Services Application  
Status      : Online  
```  
  
 **Pool de aplicativos de serviço**  
  
> [!NOTE]  
>  O exemplo de código a seguir retorna primeiro a propriedade applicationpool do aplicativo de serviço padrão do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] . O nome é analisado na cadeia de caracteres e usado para obter o status do objeto do pool de aplicativos.  
>   
>  Verifique se o status é **Online**. Se o status não for Online ou a mensagem “erro de HTTP” for exibida quando você navegar no site do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , verifique se as credenciais de identidade nos pools de aplicativos do IIS ainda estão corretas. O nome do pool do IIS é o valor da propriedade ID retornada pelo comando Get-SPServiceApplicationPool.  
  
```  
$poolname=[string](Get-PowerPivotServiceApplication | select -property applicationpool)  
$position=$poolname.lastindexof("=")  
$poolname=$poolname.substring($position+1)  
$poolname=$poolname.substring(0,$poolname.length-1)  
Get-SPServiceApplicationPool | select name, status, processaccountname, id | where {$_.Name -eq $poolname} | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
Name                           Status ProcessAccountName Id  
----                           ------ ------------------ -------   
SharePoint Web Services System Online DOMAIN\account     89b50ec3-49e3-4de7-881a-2cec4b8b73ea  
```  
  
 ![Observação](../../../reporting-services/media/rs-fyinote.png "Observação")o pool de aplicativos também pode ser verificado na página Administração Central **gerenciar aplicativos de serviço**. Clique no nome do aplicativo de serviço e, em seguida, clique em **propriedades** na faixa de opções.  
  
 **Proxies do aplicativo de serviço do Excel e PowerPivot**  
  
 Verifique se o status é **Online**.  
  
```  
Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like “*powerpivot*” -or $_.TypeName -like “*excel services*”} | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
TypeName                                                 Status UnattendedAccount           DisplayName  
--------                                                 ------ -----------------           -----------  
PowerPivot Service Application Proxy                     Online PowerPivotUnattendedAccount PowerPivotServiceApplication1  
Excel Services Application Web Service Application Proxy Online                             Excel Services Application  
```  
  
##  <a name="bkmk_databases"></a> Bancos de dados  
 O script a seguir retorna o status dos bancos de dados de aplicativo de serviço e de todos os bancos de dados de conteúdo. Verifique se o status é **Online**.  
  
```  
Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq “content database” -or $_.TypeName -like “*Gemini*”} | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
Name                                                                       Status Server                  TypeName   
----                                                                       ------ ------                  --------   
DefaultPowerPivotServiceApplicationDB-38422181-2b68-4ab2-b2bb-9c00c39e5a5e Online SPServer Name=TESTSERVER Microsoft.AnalysisServices.SPAddin.GeminiServiceDatabase  
DefaultWebApplicationDB-f0db1a8e-4c22-408c-b9b9-153bd74b0312               Online TESTSERVER\POWERPIVOT    Content Database   
SharePoint_Admin_3cadf0b098bf49e0bb15abd487f5c684                          Online TESTSERVER\POWERPIVOT    Content Database  
  
```  
  
##  <a name="bkmk_features"></a> Recursos do SharePoint  
 Verifique se o site e os recursos do farm estão online.  
  
```  
Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like “*powerpivot*”} | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
DisplayName     Status Scope Farm                           
-----------     ------ ----- ----                           
PowerPivotSite  Online  Site SPFarm Name=SharePoint_Config  
PowerPivotAdmin Online   Web SPFarm Name=SharePoint_Config  
PowerPivot      Online  Farm SPFarm Name=SharePoint_Config  
```  
  
##  <a name="bkmk_timer_jobs"></a> Trabalhos de timer  
 Verifique se os trabalhos de timer estão **Online**. O EngineService do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] não está instalado no SharePoint 2013, portanto, o script não listará os trabalhos de timer do EngineService em uma implantação do SharePoint 2013.  
  
```  
Get-SPTimerJob | where {$_.service -like "*power*" -or $_.service -like "*mid*"} | select status, displayname, LastRunTime, service | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
  
      Status DisplayName                                                                          LastRunTime          Service                               
------ -----------                                                                          -----------          -------                               
Online Health Analysis Job (Daily, SQL Server Analysis Services, All Servers)               4/9/2014 12:00:01 AM EngineService Name=MSOLAP$POWERPIVOT  
Online Health Analysis Job (Hourly, SQL Server Analysis Services, All Servers)              4/9/2014 1:00:01 PM  EngineService Name=MSOLAP$POWERPIVOT  
Online Health Analysis Job (Weekly, SQL Server Analysis Services, All Servers)              4/6/2014 12:00:10 AM EngineService Name=MSOLAP$POWERPIVOT  
Online PowerPivot Management Dashboard Processing Timer Job                                 4/8/2014 3:45:38 AM  MidTierService  
Online PowerPivot Health Statistics Collector Timer Job                                     4/9/2014 1:00:12 PM  MidTierService  
Online PowerPivot Data Refresh Timer Job                                                    4/9/2014 1:09:36 PM  MidTierService  
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, All Servers)  4/9/2014 12:00:00 AM MidTierService  
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, Any Server)   4/9/2014 12:00:00 AM MidTierService  
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, All Servers) 4/6/2014 12:00:03 AM MidTierService  
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, Any Server)  4/6/2014 12:00:03 AM MidTierService  
Online PowerPivot Setup Extension Timer Job                                                 4/1/2014 1:40:31 AM  MidTierService  
```  
  
##  <a name="bkmk_health_rules"></a> Regras de integridade  
 Há menos regras em uma implantação do SharePoint 2013. Para obter uma lista completa de regras para cada ambiente do SharePoint e uma explicação de como usar as regras, consulte [configurar regras de integridade do PowerPivot -](../../power-pivot-sharepoint/configure-power-pivot-health-rules.md).  
  
```  
Get-SPHealthAnalysisRule | select name, enabled, summary | where {$_.summary -like “*power*”}  | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
Name                          Enabled Summary  
----                          ------- -------           
SecondaryLogonHealthRule         True PowerPivot:  Secondary Logon service (seclogon) is disabled  
DataRefreshTimerJobHealthRule    True PowerPivot: The PowerPivot Data Refresh timer job is disabled.  
ASUsageLoadHealthRule            True PowerPivot: The ratio of load events to connections is too high.  
ASMiniDumpHealthRule             True PowerPivot: One or more minidump files were found in the Logs directory, indicating a program crash  
ASUsageCubeRule                  True PowerPivot: Usage data is not getting updated at the expected frequency.  
ASADOMDNETHealthRule             True PowerPivot: ADOMD.NET is not installed on a standalone WFE that is configured for central admin  
MidTierAcctReadPermissionRule    True PowerPivot: MidTier process account should have 'Full Read' permission on all associated SPWebApplications.  
```  
  
##  <a name="bkmk_logs"></a> Logs do Windows e do ULS  
 **Log de eventos do Windows**  
  
 O comando a seguir pesquisará o log de eventos do Windows em busca dos eventos relacionados à instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Para obter informações sobre como desabilitar eventos ou alterar o nível do evento, consulte [configurar e exibir arquivos de Log do SharePoint e log de diagnóstico &#40;PowerPivot para SharePoint&#41;](../../power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
 **Nome do serviço:** MSOLAP$POWERPIVOT  
  
 **Nome de exibição nos Serviços Windows:** SQL Server Analysis Services (POWERPIVOT)  
  
```  
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
TimeGenerated           EntryType Source            Message  
-------------           --------- ------            -------  
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.  
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Service started. Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM 12.0.1997.5.  
4/16/2014 1:45:18 PM  Information MSOLAP$POWERPIVOT The flight recorder was started.  
4/14/2014 6:45:37 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.  
```  
  
 **Log do ULS do SharePoint, últimas 48 horas**  
  
 O comando a seguir retornará as mensagens do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] do log do ULS que foram criadas nas últimas 48 horas. Ajuste o parâmetro addhours de acordo com as suas necessidades.  
  
```  
Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | select timestamp, area, category, eventid,level, message| format-table -property * -autosize | out-default  
```  
  
 A seguinte variação do comando retorna apenas eventos de log da categoria **atualização de dados** :  
  
```  
Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message  
```  
  
 **Exemplo de saída**  
  
```  
Timestamp   : 4/14/2014 7:15:01 PM  
Area        : PowerPivot Service  
Category    : Data Refresh  
EventID     : 43  
Level       : High  
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77  
Message     : The following error occured when working with the service application, Default PowerPivot Service Application. Skipping the service application..  
  
Timestamp   : 4/14/2014 7:15:02 PM  
Area        : PowerPivot Service  
Category    : Data Refresh  
EventID     : 99  
Level       : High  
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77  
Message     : EXCEPTION: System.TimeoutException: The request channel timed out while waiting for a reply after 00:00:47.0625313. Increase the timeout value passed to   
              the call to Request or increase the SendTimeout value on the Binding. The time allotted to this operation may have been a portion of a longer timeout.   
              ---> System.TimeoutException: The HTTP request to 'http://localhost:32843/SecurityTokenServiceApplication/securitytoken.svc/actas' has exceeded the   
              allotted timeout of 00:00:54.5930000. The time allotted to this operation may have been a portion of a longer timeout. ---> System.Net.WebException: The   
              operation has timed out     at System.Net.HttpWebRequest.GetResponse()     at   
              System.ServiceModel.Channels.HttpChannelFactory`1.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout...  
```  
  
##  <a name="bkmk_msolap"></a> Provedor MSOLAP  
 Verifique o provedor MSOLAP. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] requerem o MSOLAP.5.  
  
```  
$excelApp=Get-SPExcelServiceApplication  
get-spexceldataprovider -ExcelServiceApplication $excelApp |select providerid,providertype,description | where {$_.providerid -like “msolap*” } | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
ProviderId ProviderType Description  
---------- ------------ -----------  
MSOLAP     Oledb        Microsoft OLE DB Provider for OLAP Services       
MSOLAP.3   Oledb        Microsoft OLE DB Provider for OLAP Services 9.0   
MSOLAP.4   Oledb        Microsoft OLE DB Provider for OLAP Services 10.0  
MSOLAP.5   Oledb        Microsoft OLE DB Provider for OLAP Services 11.0  
```  
  
 Para saber mais, confira [Instalar o provedor OLE DB do Analysis Services nos servidores do SharePoint](../../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) e [Adicionar MSOLAP.5 como um provedor de dados confiável aos Serviços do Excel](http://technet.microsoft.com/library/hh758436.aspx).  
  
##  <a name="bkmk_adomd"></a> Biblioteca de cliente ADOMD.Net  
  
```  
get-wmiobject -class win32_product | Where-Object {$_.name -like "*ado*"} | select name, version, vendor | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
name                                                  version      vendor  
----                                                  -------      ------  
Microsoft SQL Server 2008 Analysis Services ADOMD.NET 10.1.2531.0  Microsoft Corporation  
Microsoft SQL Server 2005 Analysis Services ADOMD.NET 9.00.1399.06 Microsoft Corporation  
```  
  
 Para obter mais informações, confira [Instalar o ADOMD.NET em servidores Web front-end executando a Administração Central](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).  
  
##  <a name="bkmk_health_collection"></a> Regras de coleta de dados de integridade  
 Verifique se o **Status** é Online e se **Habilitado** está definido como True.  
  
```  
get-spusagedefinition | select name, status, enabled, tablename, DaysToKeepDetailedData | where {$_.name -like "powerpivot*"} | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída**  
  
```  
Name                         Status Enabled TableName                   DaysToKeepDetailedData  
----                         ------ ------- ---------                   ----------------------  
PowerPivot Connections       OnlineTrue AnalysisServicesConnections  14  
PowerPivot Load Data Usage   Online    True AnalysisServicesLoads                           14  
PowerPivot Query Usage       Online    True AnalysisServicesRequests                        14  
PowerPivot Unload Data Usage Online    True AnalysisServicesUnloads                         14  
```  
  
 Para obter mais informações, consulte [coleta de dados de uso do PowerPivot](../../power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="bkmk_solutions"></a> Soluções  
 Se os outros componentes estiverem online, você poderá ignorar a verificação das soluções. Se, no entanto, as regras de integridade estiverem ausentes, verifique se as duas soluções existem e mostravam Verifique se as duas soluções do PowerPivot estão **Online** e **Implantadas**.  
  
```  
get-spsolution | select name, status, deployed, DeploymentState, DeployedServers | where {$_.Name -like “*powerpivot*”} | format-table -property * -autosize | out-default  
```  
  
 **Exemplo de saída do SharePoint 2013**  
  
```  
Name                                 Status Deployed        DeploymentState DeployedServers  
----                                 ------ --------        --------------- ---------------  
powerpivotfarm14solution.wsp         Online     True         GlobalDeployed {UETESTA00}  
powerpivotfarmsolution.wsp           Online     True         GlobalDeployed {UETESTA00}  
powerpivotwebapplicationsolution.wsp Online     True WebApplicationDeployed {UETESTA00}  
```  
  
 **Exemplo de saída do SharePoint 2010**  
  
```  
Name                 Status Deployed        DeploymentState DeployedServers   
----                 ------ --------        --------------- ---------------   
powerpivotfarm.wsp   Online     True         GlobalDeployed {uesql11spoint2}  
powerpivotwebapp.wsp Online     True WebApplicationDeployed {uesql11spoint2}  
```  
  
 Para obter mais informações sobre como implantar soluções do SharePoint, veja [Implantar pacotes de solução (SharePoint Server 2010)](http://technet.microsoft.com/library/cc262995\(v=office.14\).aspx).  
  
##  <a name="bkmk_manual"></a> Etapas de verificação manual  
 Esta seção descreve as etapas de verificação que não podem ser concluídas com os cmdlets do PowerShell.  
  
 **Atualização de dados agendada:** configure a agenda de atualização para uma pasta de trabalho para **Também atualizar o mais rápido possível**.  Para obter mais informações, consulte a seção "Verificar atualização de dados" [agenda de atualização de dados e dados de fontes que fazer não suporte a autenticação do Windows &#40;PowerPivot para SharePoint&#41;](../../power-pivot-sharepoint/schedule-data-refresh-and-data-sources-no-windows-authentication.md).  
  
##  <a name="bkmk_more_resources"></a> Mais recursos  
 [Cmdlets de administração do servidor Web (IIS) no Windows PowerShell](http://technet.microsoft.com/library/ee790599.aspx).  
  
 [PowerShell para verificar serviços, sites do IIS e o status do pool de aplicativos no SharePoint](http://gallery.technet.microsoft.com/office/PowerShell-to-check-a6ed72a0).  
  
 [Referência do Windows PowerShell para SharePoint 2013](http://technet.microsoft.com/library/ee890108\(v=office.15\).aspx)  
  
 [Referência do Windows PowerShell para SharePoint Foundation 2010](http://technet.microsoft.com/library/ee890105\(v=office.14\).aspx)  
  
 [Gerenciar Serviços do Excel com o Windows PowerShell (SharePoint Server 2010)](http://technet.microsoft.com/library/ff191201\(v=office.14\).aspx)  
  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
 [Usar o cmdlet Get-EvenLog](http://technet.microsoft.com/library/ee176846.aspx)  
  
##  <a name="bkmk_full_script"></a> Script completo do PowerShell  
 O script a seguir contém todos os comandos das seções anteriores. O script executa os comandos na mesma ordem em que são apresentados neste tópico. O script contém algumas variações opcionais dos comandos observados neste tópico caso você precise de filtragem adicional. As variações são desabilitadas com um caractere de comentário (#). O script também inclui algumas instruções para verificar o modo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint. As instruções [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] são desabilitadas com um caractere de comentário (#).  
  
```  
# This script audits services related to PowerPivot for SharePoint  
$starttime=Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime   
  
Write-Host  "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell –EA 0  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "Analysis Services Windows Service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
get-service | select name, displayname, status | where {$_.Name -eq "msolap`$powerpivot"} | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivotEngineSerivce and PowerPivotSystemService"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
Get-PowerPivotSystemService | select typename, status, applications, farm | format-table -property * -autosize | out-default  
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section  
#Get-PowerPivotSystemService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default  
  
Get-PowerPivotEngineService | select typename, status, name, instances, farm | format-table -property * -autosize | out-default  
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section  
#Get-PowerPivotEngineService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default  
  
#Write-Host ""  
#Write-Host -ForegroundColor Green "Service Instances - optional if you want to associate services with the server"  
#Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#Get-SPServiceInstance | select typename, status, server, service, instance | where {$_.TypeName -like “*powerpivot*” -or $_.TypeName -like “*excel*” -or $_.TypeName -like “*Analysis Services*”} | format-table -property * -autosize | out-default  
#Get-PowerPivotEngineServiceInstance  | select typename, ASServername, status, server, service, instance  
#Get-PowerPivotSystemServiceInstance  | select typename, ASSServerName, status, server, service, instance  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot And Excel Service Applications"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-PowerPivotServiceApplication | select typename,name, status, unattendedaccount, applicationpool, farm, database   
Get-SPExcelServiceApplication | select typename,  DisplayName, status   
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot Service Application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
# the following assumes there is only 1 PowerPivot Service Application, and returns that applicaitons pool name.  if you have more than one, use the 2nd version  
$poolname=[string](Get-PowerPivotServiceApplication | select -property applicationpool)  
$position=$poolname.lastindexof("=")  
$poolname=$poolname.substring($position+1)  
$poolname=$poolname.substring(0,$poolname.length-1)  
Get-SPServiceApplicationPool | select name, status, processaccountname, id | where {$_.Name -eq $poolname} | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot and Excel Service Application Proxy"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like “*powerpivot*” -or $_.TypeName -like “*excel services*”} | format-table -property * -autosize | out-default  
#Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like “*powerpivot*” -or $_.TypeName -like “*Reporting Services*” -or $_.TypeName -like “*excel services*”} | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "DATABASES"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq “content database” -or $_.TypeName -like “*Gemini*”} | format-table -property * -autosize | out-default  
#Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq “content database” -or $_.TypeName -like “*Gemini*” -or $_.TypeName -like “*ReportingServices*”}   
  
#Write-Host ""  
Write-Host -ForegroundColor Green "features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPFeature | select displayname, status, scope, farm| where {$_.displayName -like “*powerpivot*”} | format-table -property * -autosize | out-default  
#Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like “*powerpivot*” -or $_.displayName -like “*ReportServer*”}  | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "Timer Jobs (Job Definitions) -- list is the same as seen in the 'Review timer job definitions' section of the management dashboard"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPTimerJob | where {$_.service -like "*power*" -or $_.service -like "*mid*"} | select status, displayname, LastRunTime, service | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "health rules"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPHealthAnalysisRule | select name, enabled, summary | where {$_.summary -like “*power*”}  | format-table -property * -autosize | out-default  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime   
write-host -foregroundcolor DarkGray EndTime $time  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "Windows Event Log data MSSQL$POWERPIVOT and "  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default  
#The following is the same command but with the Inforamtion events filtered out.  
#Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*" -and ($_.entrytype -match "error" -or $_.entrytype -match "critical" -or $_.entrytype -match "warning")}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "ULS Log data"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | select timestamp, area, category, eventid,level, correlation, message| format-table -property * -autosize | out-default  
#the following example filters for the category 'data refresh'  
#Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime   
write-host -foregroundcolor DarkGray EndTime $time  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "MSOLAP data provider for Excel Servivces, service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
$excelApp=Get-SPExcelServiceApplication  
get-spexceldataprovider -ExcelServiceApplication $excelApp |select providerid,providertype,description | where {$_.providerid -like “msolap*” } | format-table -property * -autosize | out-default  
  
Write-Host -ForegroundColor Green "ADOMD.net client library"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
get-wmiobject -class win32_product | Where-Object {$_.name -like "*ado*"} | select name, version, vendor | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "Usage Data Rules"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
get-spusagedefinition | select name, status, enabled, tablename, DaysToKeepDetailedData | where {$_.name -like "powerpivot*"} | format-table -property * -autosize | out-default  
  
Write-Host -ForegroundColor Green "Solutions"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
get-spsolution | select name, status, deployed, DeploymentState, DeployedServers | where {$_.Name -like “*powerpivot*”} | format-table -property * -autosize | out-default  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime   
write-host -foregroundcolor DarkGray EndTime $time  
  
```  
  
  