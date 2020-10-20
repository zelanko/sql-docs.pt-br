---
description: Referência de configuração da Web (Master Data Services)
title: Referência de configuração da Web
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7f4baf9f3ef626f5e2dcdc62092afaf1e586df33
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196087"
---
# <a name="web-configuration-reference-master-data-services"></a>Referência de configuração da Web (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa um arquivo Web.config que contém as definições de configuração que permitem que o IIS (Serviços de Informações da Internet) hospede o serviço Web e o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . O arquivo Web.config está localizado na pasta WebApplication do caminho de instalação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações sobre o caminho e as permissões, consulte [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos do Web.Config  
 O arquivo de Web.config contém um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] elemento personalizado, além dos **\<masterDataServices>** elementos de configuração padrão IIS, .NET Framework, ASP.NET e Windows Communication Foundation (WCF). A tabela a seguir descreve os elementos incluídos no arquivo Web.config.  
  
|Elemento de configuração|Descrição|  
|---------------------------|-----------------|  
|**masterDataServices**|Elemento personalizado. Conecta o serviço Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**connectionStrings**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento connectionStrings (Esquema de Configuração do ASP.NET)](/previous-versions/dotnet/netframework-4.0/bf7sd233(v=vs.100)) na Biblioteca MSDN.|  
|**System. Web**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web (Esquema de Configuração do ASP.NET)](/previous-versions/dotnet/netframework-4.0/dayb112d(v=vs.100)) na Biblioteca MSDN.|  
|**inicialização**|Elemento .NET Framework. Para obter mais informações, consulte [ \<startup> elemento](/dotnet/framework/configure-apps/file-schema/startup/startup-element) na biblioteca MSDN.|  
|**appmodel**|Elemento .NET Framework. Para obter mais informações, consulte [ \<runtime> elemento](/dotnet/framework/configure-apps/file-schema/runtime/runtime-element) na biblioteca MSDN.|  
|**system.codedom**|Elemento .NET Framework. Para obter mais informações, consulte [ \<system.codedom> elemento](/dotnet/framework/configure-apps/file-schema/compiler/system-codedom-element) na biblioteca MSDN.|  
|**System. Web. Extensions**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web.extensions (Esquema de Configuração do ASP.NET)](/previous-versions/dotnet/netframework-4.0/bb546044(v=vs.100)) na Biblioteca MSDN.|  
|**system.webServer**|Grupo de seções que contém elementos IIS. Para obter mais informações, consulte [Grupo de Seção system.webServer \[Esquema de Configurações do IIS 7\]](/previous-versions/iis/settings-schema/ms689429(v=vs.90)) na Biblioteca MSDN.|  
|**system.serviceModel**|Elemento WCF. Para obter mais informações, consulte [\<system.serviceModel>](/dotnet/framework/configure-apps/file-schema/wcf/system-servicemodel) na biblioteca MSDN.|  
|**system.diagnostics**|Elemento .NET Framework. Para obter mais informações, consulte [ \<system.diagnostics> elemento](/dotnet/framework/configure-apps/file-schema/trace-debug/system-diagnostics-element) na biblioteca MSDN.|  
|**appSettings**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento appSettings (Esquema de Configuração Geral)](/previous-versions/dotnet/netframework-4.0/ms228154(v=vs.100)) na Biblioteca MSDN.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 O **\<masterDataServices>** elemento é um elemento personalizado que é usado para conectar um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] serviço Web a um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] banco de dados.  
  
### <a name="syntax"></a>Sintaxe  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Elementos e atributos  
  
|Item|Descrição|  
|----------|-----------------|  
|**instância**|Elemento filho. Contém atributos que especificam informações para o serviço Web e a cadeia de conexão do banco de dados.|  
|**virtualPath**|Atributo. Especifica o caminho virtual do aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Isso corresponde ao atributo **path** do **\<application>** elemento sob o **\<site>** elemento no arquivo de ApplicationHost.config do IIS.|  
|**siteName**|Atributo. Especifica o nome do site que hospeda o aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Isso corresponde ao atributo **Name** do **\<site>** elemento em **\<sites>** no arquivo IIS ApplicationHost.config.|  
|**connectionName**|Atributo. Especifica o nome da conexão a usar. Isso corresponde ao atributo **Name** do **\<add>** elemento sob o **\<connectionStrings>** elemento em Web.config.|  
|**serviceName**|Atributo. Especifica o nome do serviço Web. Isso corresponde ao atributo **Name** do **\<service>** elemento sob o **\<services>** elemento em Web.config.|  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra um serviço chamado MDS1 no site Contoso e no caminho /MDS usando uma cadeia de conexão especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
