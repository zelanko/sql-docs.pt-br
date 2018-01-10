---
title: "Propriedades do servidor (página Avançado) – Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: "18"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: e8c6a475c37a953394fa51023dccdd9d80e5cb32
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="server-properties-advanced-page---reporting-services"></a>Propriedades do Servidor (página Avançado) - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Use essa página para definir propriedades do sistema no servidor de relatórios. Há vários modos de definir propriedades do sistema. Essa ferramenta fornece uma interface gráfica do usuário para que você possa definir propriedades sem precisar gravar código.

Para abrir essa página, inicie o SQL Server Management Studio, conecte-se a uma instância do servidor de relatório, clique com o botão direito do mouse no nome do servidor de relatório e selecione **Propriedades**. Selecione **Avançado** para abrir essa página.

## <a name="options"></a>Opções

**EnableMyReports**  
Indica se o recurso Meus Relatórios está habilitado. Um valor **true** indica que o recurso está habilitado.  

**MyReportsRole**  
O nome da função usado ao criar políticas de segurança nas pastas de usuário Meus Relatórios. O valor padrão é **My Reports Role**.  

**EnableClientPrinting**  
Determina se o controle ActiveX de RSClientPrint está disponível para download no servidor de relatório. Os valores válidos são **true** e **false**. O valor padrão é **true**. Para obter mais informações sobre configurações adicionais necessárias para esse controle, consulte [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  

**EnableExecutionLogging**  
Indica se o log de execução de relatório está habilitado. O valor padrão é **true**. Para obter mais informações sobre o log de execução do servidor de relatório, consulte [ExecutionLog do Servidor de Relatório e a exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

**ExecutionLogDaysKept**  
O número de dias para manter informações de execução de relatório no log de execução. Os valores válidos para essa propriedade incluem **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1** , as entradas não serão excluídas da tabela Log de Execução. O valor padrão é **60**.  

> [!NOTE] 
> Definir um valor de **0** *excluirá* todas as entradas do log de execução. Um valor de **-1** manterá as entradas do log de execução e não será excluído.

**SessionTimeout**  
A quantidade de tempo, em segundos, que uma sessão permanece ativa. O valor padrão é **600**.  

**SharePointIntegratedMode**  
Esta é uma propriedade somente leitura que indica o modo do servidor. Se este valor for Falso, o servidor de relatórios executará em modo nativo.  

**SiteName**  
O nome do site de servidor de relatórios exibido no título da página do portal da Web. O valor padrão é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Essa propriedade pode ser uma cadeia de caracteres vazia. O tamanho máximo é de 8.000 caracteres.  

**StoredParametersLifetime**  
Especifica o número máximo de dias que um parâmetro armazenado pode ser armazenado. Os valores válidos são de **-1**, **+1** até **2,147,483,647**. O valor padrão é **180** dias.  

**StoredParametersThreshold**  
Especifica o número máximo de valores de parâmetro que pode ser armazenado pelo servidor de relatórios. Os valores válidos são de **-1**, **+1** até **2,147,483,647**. O valor padrão é **1500**.  

**UseSessionCookies**  
Indica se o servidor de relatório dever usar cookies de sessão ao se comunicar com navegadores clientes. O valor padrão é **true**.  

**ExternalImagesTimeout**  
Determina a quantidade de tempo dentro do qual um arquivo de imagem externa deve ser recuperado antes que a conexão expire. O padrão é **600** segundos.  

**SnapshotCompression**  
Define como os instantâneos são compactados. O valor padrão é **SQL**. Os valores válidos são os seguintes:

|Valores|Description|
|---------|---------|
|**SQL**|Instantâneos são compactados quando armazenados no banco de dados do servidor de relatório. Esse é o comportamento atual.|
|**Nenhuma**|Instantâneos não são compactados.|
|**Todos**|Instantâneos são compactados para todas as opções de armazenamento, que incluem o banco de dados do servidor de relatório ou o sistema de arquivos.|

**SystemReportTimeout**  
O valor do tempo limite de processamento do relatório padrão, em segundos, para todos os relatórios gerenciados no namespace do servidor de relatório. Esse valor pode ser substituído no nível do relatório. Se a propriedade estiver definida, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado expirar. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, relatórios no namespace não expirarão durante o processamento. O valor padrão é **1800**.  

**SystemSnapshotLimit**  
O número máximo de instantâneos que são armazenados para um relatório. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, não haverá limite de instantâneo.  

**EnableIntegratedSecurity**  
Determina se a segurança integrada do Windows tem suporte para conexões de fonte de dados de relatório. O padrão é **True**. Os valores válidos são os seguintes:

|Valores|Description|
|---------|---------|
|**Verdadeiro**|A segurança integrada do Windows está habilitada.|
|**Falso**|A segurança integrada do Windows não está habilitada. Fontes de dados de relatório configuradas para usar a segurança integrada do Windows não serão executadas.|

**EnableLoadReportDefinition**  
Selecione essa opção para especificar se os usuários podem executar relatório ad hoc de um Construtor de Relatórios. A definição dessa opção determina o valor da propriedade **EnableLoadReportDefinition** no servidor de relatórios.  

Se você desmarcar esta opção, a propriedade será definida como False e o servidor de relatório não irá gerar relatórios de clickthrough de relatórios que usam um modelo como uma fonte de dados. Qualquer chamada ao método LoadReportDefinition será bloqueada.  

A desativação dessa opção reduz uma ameaça de que um usuário mal-intencionado inicie um ataque de negação de serviço, carregando o servidor de relatórios com solicitações de LoadReportDefinition.  

**EnableRemoteErrors**  
Inclui informações de erro externo (por exemplo, informações de erros sobre fontes de dados de relatório) com as mensagens de erro retornadas aos usuários que solicitam relatórios de computadores remotos. Os valores válidos são **true** e **false**. O valor padrão é **false**. Para obter mais informações, consulte [Habilitar erros remotos &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

**EnableReportDesignClientDownload**  
Especifica se o pacote de instalação do Construtor de Relatórios pode ser baixado no servidor de relatórios. Se você desmarcar essa configuração, a URL para o Construtor de Relatórios não funcionará. Para obter mais informações, consulte [Configurar o acesso do Construtor de Relatórios](../../reporting-services/report-server/configure-report-builder-access.md).  

**EditSessionCacheLimit**  
Especifica o número de entradas de cache de dados que podem estar ativas em uma sessão de edição de relatório. O número padrão é 5.  

**EditSessionTimeout**  
Especifica o número de segundos antes que o tempo limite de uma sessão de edição de relatório seja excedido. O valor padrão é 7200 segundos (2 horas).  

**EnableCustomVisuals** ***(somente Servidor de Relatório do Power BI)***  
Se o Servidor de Relatório do PowerBI permitir a exibição de visuais personalizados do Power BI. Os valores são True ou False.  O padrão é True.  

**EnablePowerBIReportExportData** ***(somente Servidor de Relatório do Power BI)***  
Se o Servidor de Relatório do PowerBI permitir a exportação de dados de visuais do Power BI. Os valores são True ou False.  O padrão é True.  

**ScheduleRefreshTimeoutMinutes** ***(somente Servidor de Relatório do Power BI)***  
Tempo limite de atualização de dados em minutos, para a atualização Agendada em relatórios do Power BI com modelos AS inseridos. O padrão é 120 minutos.

**EnableTestConnectionDetailedErrors**  
Indica se são enviadas mensagens de erro detalhadas ao computador cliente quando os usuários testam as conexões de fonte de dados usando o servidor de relatório. O valor padrão é **true**. Se a opção for definida como **false**, apenas as mensagens de erro genéricas serão enviadas.

**AccessControlAllowCredentials**  
Indica se a resposta à solicitação do cliente pode ser exposta quando o sinalizador “credentials” está definido como verdadeiro. O valor padrão é **false**.

**AccessControlAllowHeaders** Uma lista de separada por vírgula de cabeçalhos que o servidor permitirá quando um cliente fizer uma solicitação. Essa propriedade pode ser uma cadeia de caracteres vazia e especificar * permitirá todos os cabeçalhos.

**AccessControlAllowMethods** Uma lista de separada por vírgula de métodos HTTP que o servidor permitirá quando um cliente fizer uma solicitação. Os valores padrão são (GET, PUT, POST, PATCH, DELETE) e especificar * permitirá todos os métodos.

**AccessControlAllowOrigin** Uma lista de separada por vírgula de origens que o servidor permitirá quando um cliente fizer uma solicitação. O valor padrão é em branco, o que impede todas as solicitações e especificar * permitirá todas as origens quando as credenciais não estiverem definidas; se as credenciais forem especificadas, uma lista explícita de origens deverá ser especificada.

**AccessControlExposeHeaders** Uma lista de separada por vírgula de cabeçalhos que o servidor exporá para os clientes. O valor padrão é vazio.

**AccessControlMaxAge** Especifica o número de segundos durante os quais os resultados da solicitação de simulação podem ser armazenados em cache. O valor padrão é 600 (10 minutos).

## <a name="see-also"></a>Consulte Também

[Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Propriedades do Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Propriedades do sistema do servidor de relatório](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Implantação de script e tarefas administrativas](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Habilitar e desabilitar Meus Relatórios](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
