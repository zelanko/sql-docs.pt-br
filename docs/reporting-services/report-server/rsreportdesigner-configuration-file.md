---
title: Arquivo de configuração RSReportDesigner | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], configuration file
- RSReportDesigner configuration file
ms.assetid: fdcc9c58-3bad-45b3-ba8e-c7816d64f14c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a24b1a2f008c23adc5445ec5ed36c51ade181486
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581336"
---
# <a name="rsreportdesigner-configuration-file"></a>arquivo de configuração RSReportDesigner
  O arquivo RSReportDesigner.config armazena configurações sobre as extensões de renderização e processamento de dados disponíveis no Designer de Relatórios. Informações de extensão de processamento de dados são armazenadas no elemento **Data** . Informações de extensão de renderização são armazenadas no elemento **Render** . O elemento **Designer** enumera os construtores de consulta usados no Designer de Relatórios.  
  
 O Designer de Relatórios usa funcionalidade de servidor de relatório inserida para uma visualização prévia dos relatórios. Configurações relacionadas a servidor podem ser especificadas para oferecer suporte a processamento do lado do servidor local para operações de visualização prévia. Para obter mais informações sobre definições de configuração do servidor de relatório, consulte [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
## <a name="file-location"></a>Local do arquivo  
 Este arquivo está localizado em \Arquivos de Programas\Microsoft Visual Studio 8\Common7\IDE\PrivateAssemblies.  
  
## <a name="editing-guidelines"></a>Editando diretrizes  
 Não modifique as configurações neste arquivo, exceto se estiver implantando ou removendo uma extensão personalizada, desabilitando o cache durante a visualização prévia ou registrando uma nova extensão de processamento de dados após a atualização do Service Pack.  
  
 As instruções específicas para a edição de arquivos de configuração serão disponibilizadas se você estiver personalizando as configurações de extensão de renderização. Para obter mais informações, consulte [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).  
  
 Para obter instruções gerais sobre como editar arquivos de configuração, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
## <a name="example-configuration-file"></a>Arquivo de configuração de exemplo  
 O exemplo a seguir ilustra o formato do arquivo RSReportDesigner.config.  
  
```  
<Configuration>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="InstanceName" Value="Microsoft.ReportingServices.PreviewServer" />  
  <Add Key="SessionCookies" Value="true" />  
  <Add Key="SessionTimeoutMinutes" Value="3" />  
  <Add Key="PolicyLevel" Value="rspreviewpolicy.config" />  
  <Add Key="CacheDataForPreview" Value="true" />  
  <Extensions>  
    <Render> . . . </Render>  
    <Data> . . . </Data>  
    <Designer> . . . </Designer>  
```  
  
## <a name="configuration-settings"></a>Definições de configuração  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**SecureConnectionLevel**|Especifica o grau de segurança da conexão de serviço Web. Os valores válidos variam de 0 a 3, sendo que 0 é o menos seguro. Para obter mais informações, consulte [Usando métodos seguros do serviço Web](../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md).|  
|**InstanceName**|Um identificador para o servidor de visualização prévia. Não modifique esse valor.|  
|**SessionCookies**|Especifica se o servidor de relatório usa cookies de navegador para manter informações de sessão. Os valores válidos são **true** e **false**. O padrão é **true**. Se você definir este valor como falso, dados de sessão serão armazenados no banco de dados **reportservertempdb** .|  
|**SessionTimeoutMinutes**|Especifica o período para o qual um cookie de sessão é válido. O padrão é 3 minutos.|  
|**PolicyLevel**|Especifica o arquivo de configuração de política de segurança. O valor válido é Rspreviewpolicy.config. Para obter mais informações, consulte [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|  
|**CacheDataForPreview**|Quando definido como **True**, o Designer de Relatórios armazena dados em um arquivo de cache no computador local. Os valores válidos são **True** (padrão) e **False**. Para obter mais informações, consulte [Visualizando relatórios](../../reporting-services/reports/previewing-reports.md).|  
|**Render**|Enumera as extensões de renderização disponíveis ao Designer de Relatórios para propósitos de visualização prévia. O conjunto de extensões de renderização usado para a visualização prévia deve ser idêntico ao instalado com o servidor de relatório.<br /><br /> **Nome** especifica a extensão de renderização. Se você estiver invocando uma extensão de renderização por código, use este valor para chamar uma extensão específica.<br /><br /> **Tipo** especifica o nome de classe totalmente qualificado da classe de extensão, além do nome de biblioteca, separado por vírgula.<br /><br /> **Visível** especifica se o nome será exibido em qualquer interface do usuário. Esse valor pode ser **True** (padrão) ou **False**. Se **True**, será exibido em interfaces de usuário.|  
|**Dados**|Enumera as extensões de processamento de dados disponíveis para o Designer de Relatórios para propósitos de conexão com fontes de dados que fornecem dados aos relatórios. O conjunto de extensões de processamento de dados usado no Designer de Relatórios pode ser idêntico ao instalado com o servidor de relatório. Se você estiver adicionando ou removendo extensões personalizadas, consulte [Implantando uma extensão de processamento de dados](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md).<br /><br /> **Nome** especifica a extensão de processamento de dados.<br /><br /> **Tipo** especifica o nome de classe totalmente qualificado da classe de extensão, além do nome de biblioteca, separado por vírgula.|  
|**Designer**|Enumera os construtores de consulta disponíveis para o Designer de Relatórios. Construtores de consulta fornecem uma interface de usuário para construir consultas que recuperam dados usados em relatórios. Construtores de consulta podem variar de acordo com extensões de processamento de dados diferentes. Por padrão, o Reporting Services fornece uma interface de usuário de ferramenta de dados visuais para todas as extensões de processamento de dados incluídas no produto. Entretanto, se você estiver construindo ou usando extensões de processamento de dados de terceiros, outras interfaces de construtor de consulta poderão ser aplicáveis.|  
|**PreviewProcessingServiceStartupTimeoutSeconds**|Especifica o período para esperar pelo serviço de processamento de visualização para começar antes de mostrar uma mensagem de erro. O padrão é 15 segundos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Ferramentas de Design da Consulta &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)  
  
  
