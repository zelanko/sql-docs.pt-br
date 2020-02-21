---
title: Página Propriedades Avançadas do Servidor | Microsoft Docs
description: Use a página Propriedades Avançadas do Servidor para definir as propriedades do sistema no servidor de relatório. Essa ferramenta fornece uma interface gráfica do usuário para que você possa definir propriedades sem gravar código.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 01/28/2020
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 6f7a1e8d3d6341da5812bb44726c5bf8186d3b19
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "76831939"
---
# <a name="server-properties-advanced-page---power-bi-report-server--reporting-services"></a>Página Propriedades Avançadas do Servidor – Servidor de Relatórios do Power BI e Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Use essa página para definir propriedades do sistema no servidor de relatórios. Há vários modos de definir propriedades do sistema. Essa ferramenta fornece uma interface gráfica do usuário para que você possa definir propriedades sem precisar gravar código.

Para abrir essa página, inicie o SQL Server Management Studio, conecte-se a uma instância do servidor de relatório, clique com o botão direito do mouse no nome do servidor de relatório e selecione **Propriedades**. Selecione **Avançado** para abrir essa página.

## <a name="options"></a>Opções

### <a name="accesscontrolallowcredentials"></a>AccessControlAllowCredentials
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Indica se a resposta à solicitação do cliente pode ser exposta quando o sinalizador `credentials` está definido como true. O valor padrão é **false**.

### <a name="accesscontrolallowheaders"></a>AccessControlAllowHeaders
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Uma lista de cabeçalhos separada por vírgula que o servidor permitirá quando um cliente fizer uma solicitação. Essa propriedade pode ser uma cadeia de caracteres vazia e especificar * permitirá todos os cabeçalhos.

### <a name="accesscontrolallowmethods"></a>AccessControlAllowMethods
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Uma lista de métodos HTTP separada por vírgula que o servidor permitirá quando um cliente fizer uma solicitação. Os valores padrão são (GET, PUT, POST, PATCH, DELETE) e especificar * permitirá todos os métodos.

### <a name="accesscontrolalloworigin"></a>AccessControlAllowOrigin
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Uma lista de origens separada por vírgula que o servidor permitirá quando um cliente fizer uma solicitação. O valor padrão é em branco, o que impede todas as solicitações, e especificar * permitirá todas as origens quando as credenciais não estiverem definidas; se as credenciais forem especificadas, uma lista explícita de origens deverá ser especificada.

### <a name="accesscontrolexposeheaders"></a>AccessControlExposeHeaders
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Uma lista de cabeçalhos separada por vírgula que o servidor exporá aos clientes. O valor padrão é vazio.

### <a name="accesscontrolmaxage"></a>AccessControlMaxAge
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Especifica o número de segundos dos resultados da solicitação de simulação que podem ser armazenados em cache. O valor padrão é 600 (10 minutos).

### <a name="allowedresourceextensionsforupload"></a>AllowedResourceExtensionsForUpload
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Define extensões de recursos que podem ser carregados no servidor de relatórios. Extensões para tipos de arquivo internos, como &ast;.rdl e &ast;.pbix não precisam ser incluídos. O padrão é "&ast;, &ast;.xml, &ast;.xsd, &ast;.xsl, &ast;.png, &ast;.gif, &ast;.jpg, &ast;.tif, &ast;.jpeg, &ast;.tiff, &ast;.bmp, &ast;.pdf, &ast;.svg, &ast;.rtf, &ast;.txt, &ast;.doc, &ast;.docx, &ast;.pps, &ast;.ppt, &ast;.pptx".

### <a name="customheaders"></a>CustomHeaders 

(Servidor de Relatórios do Power BI [janeiro de 2020], somente Reporting Services 2019 e posteriores)

Define valores de cabeçalho para todas as URLs correspondentes ao padrão regex especificado. Os usuários podem atualizar o valor CustomHeaders com um XML válido para definir valores de cabeçalho para as URLs de solicitação selecionadas. Os administradores podem adicionar qualquer número de cabeçalhos ao XML. Por padrão, não há nenhum cabeçalho personalizado e o valor está em branco. 

> [!NOTE]
> Muitos cabeçalhos podem afetar o desempenho. 

É recomendável validar a configuração da topologia para garantir que o conjunto de cabeçalhos seja compatível com a implantação do Reporting Services. Se os navegadores não tiverem as configurações corretas, você correrá o risco de escolher configurações que causam erros. Por exemplo, não adicione uma configuração HSTS se o servidor não estiver configurado para HTTPS. Cabeçalhos incompatíveis podem resultar em erros de renderização no navegador.

#### <a name="customheaders-xml-format"></a>Formato XML CustomHeaders

```xml
<CustomHeaders>
    <Header>
        <Name>{Name of the header}</Name>
        <Pattern>{Regex pattern to match URLs}</Pattern>
        <Value>{Value of the header}</Value>
    </Header>
</CustomHeaders>
```

#### <a name="setting-the-customheaders-property"></a>Configuração da propriedade CustomHeaders

- É possível defini-la usando o ponto de extremidade do SOAP [SetSystemProperties](https://docs.microsoft.com/dotnet/api/reportservice2010.reportingservice2010.setsystemproperties), passando a propriedade CustomHeaders como um parâmetro.
- Use o ponto de extremidade REST [UpdateSystemProperties](https://app.swaggerhub.com/apis/microsoft-rs/PBIRS/2.0#/System/UpdateSystemProperties): `/System/Properties` passando a propriedade CustomHeaders

#### <a name="example"></a>Exemplo

O exemplo a seguir mostra como configurar o HSTS e outros cabeçalhos personalizados para URLs com um padrão regex correspondente.

```xml
<CustomHeaders>
    <Header>
        <Name>Strict-Transport-Security</Name>
        <Pattern>\/Reports\/mobilereport</Pattern>
        <Value>max-age=86400</Value>
    </Header>
    <Header>
        <Name>Embed</Name>
        <Pattern>(.+)(/reports/)(.+)(rs:embed=true)</Pattern>
        <Value>True</Value>
    </Header>
</CustomHeaders>
```

O primeiro cabeçalho no XML acima adiciona o cabeçalho `Strict-Transport-Security: max-age=86400` às solicitações correspondentes.
- http://adventureworks/Reports/mobilereport/New%20Mobile%20Report – regex correspondente e configurará o cabeçalho HSTS
- http://adventureworks/ReportServer/mobilereport/New%20Mobile%20Report – Falha na correspondência

O segundo cabeçalho no XML acima adiciona o cabeçalho `Embed: True` à URL que contém `/reports/` e o parâmetro de consulta `rs:embed=true`.
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=true – Correspondência
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=false – Falha na correspondência

### <a name="editsessioncachelimit"></a>EditSessionCacheLimit
Especifica o número de entradas de cache de dados que podem estar ativas em uma sessão de edição de relatório. O número padrão é 5.  

### <a name="editsessiontimeout"></a>EditSessionTimeout
Especifica o número de segundos antes que o tempo limite de uma sessão de edição de relatório seja excedido. O valor padrão é 7200 segundos (duas horas). 

### <a name="enablecdnvisuals"></a>EnableCDNVisuals 
(Somente Servidor de Relatórios do Power BI) Quando habilitado, o relatório do Power BI carrega os visuais personalizados certificados mais recentes de uma CDN (rede de distribuição de conteúdo) hospedada pela Microsoft. Se o servidor não tiver acesso a recursos da Internet, desligue esta opção. Nesse caso, os visuais personalizados serão carregados do relatório publicado no servidor. O padrão é **True**.  

###  <a name="enableclientprinting"></a>EnableClientPrinting  
Determina se o controle ActiveX de RSClientPrint está disponível para download no servidor de relatório. Os valores válidos são **true** e **false**. O valor padrão é **true**. Para obter mais informações sobre configurações adicionais necessárias para esse controle, consulte [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  

### <a name="enablecustomvisuals"></a>EnableCustomVisuals 
(Somente Servidor de Relatórios do Power BI) Para habilitar a exibição de visuais personalizados do Power BI. Os valores são true ou false. *O padrão é True.*  

###  <a name="enableexecutionlogging"></a>EnableExecutionLogging  
Indica se o log de execução de relatório está habilitado. O valor padrão é **true**. Para obter mais informações sobre o log de execução do servidor de relatório, consulte [ExecutionLog do Servidor de Relatório e a exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

### <a name="enableintegratedsecurity"></a>EnableIntegratedSecurity
Determina se a segurança integrada do Windows é compatível com as conexões de fonte de dados de relatório. O padrão é **True**. Os valores válidos são os seguintes:

|Valores|Descrição|
|---------|---------|
|**Verdadeiro**|A segurança integrada do Windows está habilitada.|
|**Falso**|A segurança integrada do Windows não está habilitada. As fontes de dados de relatório configuradas para usar a segurança integrada do Windows não serão executadas.|

### <a name="enableloadreportdefinition"></a>EnableLoadReportDefinition
Selecione essa opção para especificar se os usuários podem realizar uma execução de relatório não planejada de um relatório do Report Builder. A definição dessa opção determina o valor da propriedade **EnableLoadReportDefinition** no servidor de relatórios.  

Se desmarcar essa opção, a propriedade será definida como False. O servidor de relatório não gera relatórios de clickthrough para relatórios que usam um modelo de relatório como fonte de dados. Chamadas ao método LoadReportDefinition são bloqueadas.  

A desativação dessa opção reduz uma ameaça de que um usuário mal-intencionado inicie um ataque de negação de serviço, carregando o servidor de relatórios com solicitações de LoadReportDefinition.  

### <a name="enablemyreports"></a>EnableMyReports  
Indica se o recurso Meus Relatórios está habilitado. Um valor **true** indica que o recurso está habilitado.  

### <a name="enablepowerbireportexportdata"></a>EnablePowerBIReportExportData 
(Somente Servidor de Relatórios do Power BI) Habilite a exportação de dados do Servidor de Relatórios do Power BI dos visuais do Power BI. Os valores são True ou False.  O padrão é True. 

### <a name="enableremoteerrors"></a>EnableRemoteErrors
Inclui informações de erro externo (por exemplo, informações de erros sobre fontes de dados de relatório) com as mensagens de erro retornadas aos usuários que solicitam relatórios de computadores remotos. Os valores válidos são **true** e **false**. O valor padrão é **false**. Para obter mais informações, consulte [Habilitar erros remotos &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

### <a name="enabletestconnectiondetailederrors"></a>EnableTestConnectionDetailedErrors
Indica se devem ser enviadas mensagens de erro detalhadas ao computador cliente quando os usuários testam as conexões de fonte de dados usando o servidor de relatório. O valor padrão é **true**. Se a opção for definida como **false**, apenas as mensagens de erro genéricas serão enviadas.

###  <a name="executionlogdayskept"></a>ExecutionLogDaysKept  
O número de dias para manter informações de execução de relatório no log de execução. Os valores válidos para essa propriedade incluem **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, as entradas não serão excluídas da tabela Log de Execução. O valor padrão é **60**.  

> [!NOTE]
> Configurar um valor de **0** *exclui* todas as entradas do log de execução. Um valor de **-1** mantém as entradas do log de execução e não as exclui.

### <a name="executionloglevel"></a>ExecutionLogLevel
Defina o nível do log de execução. *O padrão é Normal.*

### <a name="externalimagestimeout"></a>ExternalImagesTimeout
Determina a quantidade de tempo dentro do qual um arquivo de imagem externa deve ser recuperado antes que a conexão expire. O padrão é **600** segundos.  

### <a name="interprocesstimeoutminutes"></a>InterProcessTimeoutMinutes
(Servidor de Relatórios do Power BI, somente Reporting Services 2019 e posteriores) Define o tempo limite do processo em minutos. *O padrão é 30.*

### <a name="maxfilesizemb"></a>MaxFileSizeMb
Define o tamanho máximo do arquivo do relatório em MB. *O padrão é 1000.  O máximo é 2000.*

### <a name="modelcleanupcycleminutes"></a>ModelCleanupCycleMinutes 
(Somente Servidor de Relatórios do Power BI) Define a frequência para verificar se há modelos não usados na memória em minutos. *O padrão é 15.*

### <a name="modelexpirationminutes"></a>ModelExpirationMinutes 
(Somente Servidor de Relatórios do Power BI) Define a frequência quando modelos não usados são removidos da memória em minutos. *O padrão é 60.*

###  <a name="myreportsrole"></a>MyReportsRole  
O nome da função usado ao criar políticas de segurança nas pastas de usuário Meus Relatórios. O valor padrão é **My Reports Role**.  

### <a name="officeaccesstokenexpirationseconds"></a>OfficeAccessTokenExpirationSeconds 
(Servidor de Relatórios do Power BI, somente Reporting Services 2019 e posteriores) Define o tempo após o qual você deseja que o token de acesso do Office expire, em segundos. *O padrão é 60.*

### <a name="officeonlinediscoveryurl"></a>OfficeOnlineDiscoveryURL 
(Somente Servidor de Relatórios do Power BI) Define o endereço da sua instância de servidor do Office Online para exibir pastas de trabalho do Excel.

### <a name="rdlxreporttimetout"></a>RDLXReportTimetout
Valor de tempo limite de processamento de relatório RDLX *(relatórios do Power View em um servidor SharePoint)* , em segundos, para todos os relatórios gerenciados no namespace do servidor de relatório. Esse valor pode ser substituído no nível do relatório. Se a propriedade estiver definida, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado expirar. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, relatórios no namespace não atingirão o tempo limite durante o processamento. O valor padrão é **1800**.

### <a name="requireintune"></a>RequireIntune
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Solicita que o Intune acesse os relatórios da organização por meio do aplicativo móvel do Power BI. *O padrão é False.*

### <a name="restrictedresourcemimetypeforupload"></a>RestrictedResourceMimeTypeForUpload
(Servidor de Relatórios do Power BI [janeiro de 2019], somente Reporting Services 2017 e posteriores) Conjunto de usuários de tipos MIME não têm permissão para carregar conteúdo. Todos os recursos que já estão armazenados com um tipo MIME restrito só podem ser baixados como um aplicativo/octet-stream, em vez de serem abertos/executados pelo navegador.  Por padrão, não há itens restritos nesta lista, mas é recomendável que as organizações preencham isso para fornecer a experiência mais segura.

### <a name="schedulerefreshtimeoutminutes"></a>ScheduleRefreshTimeoutMinutes 
(Somente Servidor de Relatórios do Power BI) Tempo limite de atualização de dados em minutos para a atualização agendada em relatórios do Power BI com modelos AS inseridos. O padrão é 120 minutos.

### <a name="sessiontimeout"></a>SessionTimeout
A quantidade de tempo, em segundos, que uma sessão permanece ativa. O valor padrão é **600**.  

### <a name="sharepointintegratedmode"></a>SharePointIntegratedMode
Essa propriedade somente leitura indica o modo do servidor. Se este valor for Falso, o servidor de relatórios executará em modo nativo.  

### <a name="showdownloadmenu"></a>ShowDownloadMenu
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Habilita o menu de download das ferramentas de cliente. *O padrão é true.*

### <a name="sitename"></a>SiteName
O nome do site de servidor de relatórios exibido no título da página do portal da Web. O valor padrão é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Essa propriedade pode ser uma cadeia de caracteres vazia. O tamanho máximo é de 8.000 caracteres.  

### <a name="snapshotcompression"></a>SnapshotCompression
Define como os instantâneos são compactados. O valor padrão é **SQL**. Os valores válidos são os seguintes:

|Valores|Descrição|
|---------|---------|
|**SQL**|Instantâneos são compactados quando armazenados no banco de dados do servidor de relatório. Essa compactação é o comportamento atual.|
|**Nenhuma**|Instantâneos não são compactados.|
|**Todos**|Instantâneos são compactados para todas as opções de armazenamento, que incluem o banco de dados do servidor de relatório ou o sistema de arquivos.|

### <a name="storedparameterslifetime"></a>StoredParametersLifetime
Especifica o número máximo de dias que um parâmetro armazenado pode ser armazenado. Os valores válidos são de **-1**, **+1** até **2,147,483,647**. O valor padrão é **180** dias.  

### <a name="storedparametersthreshold"></a>StoredParametersThreshold
Especifica o número máximo de valores de parâmetro que pode ser armazenado pelo servidor de relatórios. Os valores válidos são de **-1**, **+1** até **2,147,483,647**. O valor padrão é **1500**.  

### <a name="supportedhyperlinkschemes"></a>SupportedHyperlinkSchemes 
(Servidor de Relatórios do Power BI [janeiro de 2019], somente Reporting Services 2019 e posteriores) Define uma lista separada por vírgula dos esquemas de URI que podem ser definidos em ações de Hiperlink que têm permissão para serem renderizadas ou "&ast;" para habilitar todos os esquemas de hiperlink. Por exemplo, definir "http,https" permitiria hiperlinks para "https://www. contoso.com", mas removeria hiperlinks para "mailto:bill@contoso.com" ou “javascript:window.open(‘ www.contoso.com’, ‘_blank’)”. O padrão é "&ast;".

### <a name="systemreporttimeout"></a>SystemReportTimeout
O valor do tempo limite de processamento do relatório padrão, em segundos, para todos os relatórios gerenciados no namespace do servidor de relatório. Esse valor pode ser substituído no nível do relatório. Se a propriedade estiver definida, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado expirar. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, relatórios no namespace não atingirão o tempo limite durante o processamento. O valor padrão é **1800**.  

### <a name="systemsnapshotlimit"></a>SystemSnapshotLimit
O número máximo de instantâneos que são armazenados para um relatório. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, não haverá limite de instantâneo.  

### <a name="timerinitialdelayseconds"></a>TimerInitialDelaySeconds
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Define o tempo após o qual você deseja que o tempo inicial seja atrasado, em segundos. *O padrão é 60.*

### <a name="trustedfileformat"></a>TrustedFileFormat
(Servidor de Relatórios do Power BI, somente Reporting Services 2017 e posteriores) Define todos os formatos de arquivo externos abertos no navegador no site de portal do Reporting Services. Formatos de arquivo externos não listados solicitam download da opção no navegador. Os valores padrão são jpg, jpeg, jpe, wav, bmp, pdf, img, gif, json, mp4, web e png.

### <a name="usesessioncookies"></a>UseSessionCookies
Indica se o servidor de relatório dever usar cookies de sessão ao se comunicar com navegadores clientes. O valor padrão é **true**.  

## <a name="see-also"></a>Veja também

[Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Propriedades do Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Propriedades do sistema do servidor de relatório](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Implantação de script e tarefas administrativas](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Habilitar e desabilitar Meus Relatórios](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
