---
title: Propriedades do servidor (página Avançado) – Reporting Services | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 01/15/2019
ms.openlocfilehash: 2560c752dd55741e1718ba60f942288093d027bb
ms.sourcegitcommit: 9d3ece500fa0e4a9f4fefc88df4af1db9431c619
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463588"
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
O número de dias para manter informações de execução de relatório no log de execução. Os valores válidos para essa propriedade incluem **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, as entradas não serão excluídas da tabela Log de Execução. O valor padrão é **60**.  

> [!NOTE]
> Definir um valor de **0** *exclui* todas as entradas do log de execução. Um valor de **-1** mantém as entradas do log de execução e não as exclui.

**RDLXReportTimetout** Valor padrão de tempo limite de processamento de relatório RDLX *(relatórios do Power View em um servidor SharePoint)* , em segundos, para todos os relatórios gerenciados no namespace do servidor de relatório. Esse valor pode ser substituído no nível do relatório. Se a propriedade estiver definida, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado expirar. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, relatórios no namespace não expirarão durante o processamento. O valor padrão é **1800**.

**SessionTimeout** A quantidade de tempo, em segundos, que uma sessão permanece ativa. O valor padrão é **600**.  

**SharePointIntegratedMode**  
Essa propriedade somente leitura indica o modo do servidor. Se este valor for Falso, o servidor de relatórios executará em modo nativo.  

**SiteName**  
O nome do site de servidor de relatórios exibido no título da página do portal da Web. O valor padrão é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Essa propriedade pode ser uma cadeia de caracteres vazia. O tamanho máximo é de 8.000 caracteres.  

**StoredParametersLifetime** Especifica o número máximo de dias que um parâmetro armazenado pode ser armazenado. Os valores válidos são de **-1**, **+1** até **2,147,483,647**. O valor padrão é **180** dias.  

**StoredParametersThreshold**  
Especifica o número máximo de valores de parâmetro que pode ser armazenado pelo servidor de relatórios. Os valores válidos são de **-1**, **+1** até **2,147,483,647**. O valor padrão é **1500**.  

**UseSessionCookies**  
Indica se o servidor de relatório dever usar cookies de sessão ao se comunicar com navegadores clientes. O valor padrão é **true**.  

**ExternalImagesTimeout**  
Determina a quantidade de tempo dentro do qual um arquivo de imagem externa deve ser recuperado antes que a conexão expire. O padrão é **600** segundos.  

**SnapshotCompression** Um instantâneo do servidor de relatório nesse momento.

**SnapshotCompression**  
Define como os instantâneos são compactados. O valor padrão é **SQL**. Os valores válidos são os seguintes:

|Valores|Descrição|
|---------|---------|
|**SQL**|Instantâneos são compactados quando armazenados no banco de dados do servidor de relatório. Essa compactação é o comportamento atual.|
|**Nenhuma**|Instantâneos não são compactados.|
|**Todos**|Instantâneos são compactados para todas as opções de armazenamento, que incluem o banco de dados do servidor de relatório ou o sistema de arquivos.|

**SystemReportTimeout**  
O valor do tempo limite de processamento do relatório padrão, em segundos, para todos os relatórios gerenciados no namespace do servidor de relatório. Esse valor pode ser substituído no nível do relatório. Se a propriedade estiver definida, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado expirar. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, relatórios no namespace não expirarão durante o processamento. O valor padrão é **1800**.  

**SystemSnapshotLimit**  
O número máximo de instantâneos que são armazenados para um relatório. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, não haverá limite de instantâneo.  

**AccessControlAllowCredentials**  
Indica se a resposta à solicitação do cliente pode ser exposta quando o sinalizador “credentials” está definido como verdadeiro. O valor padrão é **false**.

**AccessControlAllowHeaders** Uma lista de cabeçalhos separada por vírgula que o servidor permitirá quando um cliente fizer uma solicitação. Essa propriedade pode ser uma cadeia de caracteres vazia e especificar * permitirá todos os cabeçalhos.

**AccessControlAllowMethods** Uma lista de métodos HTTP separada por vírgula que o servidor permitirá quando um cliente fizer uma solicitação. Os valores padrão são (GET, PUT, POST, PATCH, DELETE) e especificar * permitirá todos os métodos.

**AccessControlAllowOrigin** Uma lista de origens separada por vírgula que o servidor permitirá quando um cliente fizer uma solicitação. O valor padrão é em branco, o que impede todas as solicitações, e especificar * permitirá todas as origens quando as credenciais não estiverem definidas; se as credenciais forem especificadas, uma lista explícita de origens deverá ser especificada.

**AccessControlExposeHeaders** Uma lista de cabeçalhos separada por vírgula que o servidor exporá para os clientes. O valor padrão é vazio.

**AccessControlMaxAge** Especifica o número de segundos durante os quais os resultados da solicitação de simulação podem ser armazenados em cache. O valor padrão é 600 (10 minutos).

**AllowedResourceExtensionsForUpload** conjunto de extensões de recursos que podem ser carregados para o servidor de relatório. Extensões para tipos de arquivo internos, como &ast;.rdl e &ast;.pbix não precisam ser incluídos. O padrão é "&ast;, &ast;.xml, &ast;.xsd, &ast;.xsl, &ast;.png, &ast;.gif, &ast;.jpg, &ast;.tif, &ast;.jpeg, &ast;.tiff, &ast;.bmp, &ast;.pdf, &ast;.svg, &ast;.rtf, &ast;.txt, &ast;.doc, &ast;.docx, &ast;.pps, &ast;.ppt, &ast;.pptx".

**RestrictedResourceMimeTypeForUpload** não podem carregar conteúdo com conjunto de usuários de tipos de mime. Todos os recursos que já são armazenados com um tipo de mime restrito somente podem ser baixados como um aplicativo/octet-stream em vez de ser aberto/executada pelo navegador.  Por padrão, não há restritos itens nessa lista, mas é recomendável que as organizações preenchem isso para fornecer a experiência mais segura.

**EditSessionCacheLimit**  
Especifica o número de entradas de cache de dados que podem estar ativas em uma sessão de edição de relatório. O número padrão é 5.  

**EditSessionTimeout**  
Especifica o número de segundos antes que o tempo limite de uma sessão de edição de relatório seja excedido. O valor padrão é 7200 segundos (duas horas).  

**EnableIntegratedSecurity**  
Determina se a segurança integrada do Windows tem suporte para conexões de fontes de dados de relatório. O padrão é **True**. Os valores válidos são os seguintes:

|Valores|Descrição|
|---------|---------|
|**Verdadeiro**|A segurança integrada do Windows está habilitada.|
|**Falso**|A segurança integrada do Windows não está habilitada. As fontes de dados de relatório configuradas para usar a segurança integrada do Windows não serão executadas.|

**EnableLoadReportDefinition**  
Selecione essa opção para especificar se os usuários podem realizar uma execução de relatório não planejada de um relatório do Construtor de Relatórios. A definição dessa opção determina o valor da propriedade **EnableLoadReportDefinition** no servidor de relatórios.  

Se desmarcar essa opção, a propriedade será definida como False. O servidor de relatório não gera relatórios de clickthrough para relatórios que usam um modelo de relatório como fonte de dados. Chamadas ao método LoadReportDefinition são bloqueadas.  

A desativação dessa opção reduz uma ameaça de que um usuário mal-intencionado inicie um ataque de negação de serviço, carregando o servidor de relatórios com solicitações de LoadReportDefinition.  

**EnableRemoteErrors**  
Inclui informações de erro externo (por exemplo, informações de erros sobre fontes de dados de relatório) com as mensagens de erro retornadas aos usuários que solicitam relatórios de computadores remotos. Os valores válidos são **true** e **false**. O valor padrão é **false**. Para obter mais informações, consulte [Habilitar erros remotos &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

**EnableCustomVisuals** ***(somente Servidor de Relatórios do Power BI)*** Para habilitar a exibição de visuais personalizados do Power BI. Os valores aceitos são verdadeiro/falso. *O padrão é True.*  

**ExecutionLogLevel** Defina o nível do Log de execução. *O padrão é Normal.*

**InterProcessTimeoutMinutes** Defina o tempo limite do processo em minutos. *O padrão é 30.*

**MaxFileSizeMb** Defina o tamanho máximo do arquivo do relatório em MB. *O padrão é 1000.  O máximo é 2000.*

**ModelCleanupCycleminutes** Defina o ciclo de limpeza do modelo em minutos. *O padrão é 15.*

**OfficeAccessTokenExpirationSeconds** ***(somente Servidor de Relatórios do Power BI)*** Defina o tempo após o qual você deseja que o token de acesso do office para expire, em segundos. *O padrão é 60.*

**OfficeOnlineDiscoveryURL** ***(somente Servidor de Relatórios do Power BI)*** Defina o endereço da sua instância de servidor do Office Online para exibir pastas de trabalho do Excel.

**RequireIntune** Requer o Intune para acessar os relatórios da sua organização por meio do aplicativo móvel do Power BI. *O padrão é False.*

**ScheduleRefreshTimeoutMinutes** ***(somente Servidor de Relatórios do Power BI)*** Defina o tempo limite para a atualização agendada. *O padrão é 120.*

**ShowDownloadMenu** Habilita o menu de download das ferramentas de cliente. *O padrão é true.*

**SupportedHyperlinkSchemes** ***(somente Servidor de Relatórios do Power BI)*** Define uma lista separada por vírgulas dos esquemas de URI que podem ser definidos em ações de Hiperlink que têm permissão para serem renderizadas ou "&ast;" para habilitar todos os esquemas de hiperlink. Por exemplo, definir "http,https" permitiria hiperlinks para "https://www. contoso.com", mas removeria hiperlinks para "mailto:bill@contoso.com" ou “javascript:window.open(‘www.contoso.com’, ‘_blank’)”. O padrão é "&ast;".

**TimeInitialDelaySeconds** Defina o quanto você deseja que o tempo inicial seja atrasado, em segundos. *O padrão é 60.*

**TrustedFileFormat** Defina todos os formatos de arquivo externos abertos no navegador no site de portal do Reporting Services. Formatos de arquivo externos não listados solicitam download da opção no navegador. Os valores padrão são jpg, jpeg, jpe, wav, bmp, pdf, img, gif, json, mp4, web e png.

**EnablePowerBIReportExportData** ***(somente Servidor de Relatório do Power BI)***  
Habilite a exportação de dados do Servidor de Relatórios do Power BI dos visuais do Power BI. Os valores são True ou False.  O padrão é True.  

**ScheduleRefreshTimeoutMinutes** ***(somente Servidor de Relatório do Power BI)***  
Tempo limite de atualização de dados em minutos, para a atualização Agendada em relatórios do Power BI com modelos AS inseridos. O padrão é 120 minutos.

**EnableTestConnectionDetailedErrors**  
Indica se devem ser enviadas mensagens de erro detalhadas ao computador cliente quando os usuários testam as conexões de fonte de dados usando o servidor de relatório. O valor padrão é **true**. Se a opção for definida como **false**, apenas as mensagens de erro genéricas serão enviadas.

## <a name="see-also"></a>Consulte Também

[Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Propriedades do Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Propriedades do sistema do servidor de relatório](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Implantação de script e tarefas administrativas](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Habilitar e desabilitar Meus Relatórios](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
