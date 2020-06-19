---
title: Referência de configuração da Web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 239a71ced6a96c62ddead6ee2659756cbeff3681
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970896"
---
# <a name="web-configuration-reference-master-data-services"></a>Referência de configuração da Web (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa um arquivo Web.config que contém as definições de configuração que permitem que o IIS (Serviços de Informações da Internet) hospede o serviço Web e o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . O arquivo Web.config está localizado na pasta WebApplication do caminho de instalação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações sobre o caminho e as permissões, consulte [Permissões de pasta e arquivo &#40;Master Data Services&#41;](folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos do Web.Config  
 O arquivo de Web.config contém um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] elemento personalizado, além dos **\<masterDataServices>** elementos de configuração padrão IIS, .NET Framework, ASP.NET e Windows Communication Foundation (WCF). A tabela a seguir descreve os elementos incluídos no arquivo Web.config.  
  
|Elemento de configuração|Descrição|  
|---------------------------|-----------------|  
|`masterDataServices`|Elemento personalizado. Conecta o serviço Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|`connectionStrings`|Elemento ASP.NET. Para obter mais informações, consulte [Elemento connectionStrings (Esquema de Configuração do ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178347) na Biblioteca MSDN.|  
|`system.web`|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web (Esquema de Configuração do ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178348) na Biblioteca MSDN.|  
|`startup`|Elemento .NET Framework. Para obter mais informações, consulte [ \<startup> elemento](https://go.microsoft.com/fwlink/?LinkId=178349) na biblioteca MSDN.|  
|`runtime`|Elemento .NET Framework. Para obter mais informações, consulte [ \<runtime> elemento](https://go.microsoft.com/fwlink/?LinkId=178350) na biblioteca MSDN.|  
|`system.codedom`|Elemento .NET Framework. Para obter mais informações, consulte [ \<system.codedom> elemento](https://go.microsoft.com/fwlink/?LinkId=178351) na biblioteca MSDN.|  
|`system.web.extensions`|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web.extensions (Esquema de Configuração do ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178352) na Biblioteca MSDN.|  
|`system.webServer`|Grupo de seções que contém elementos IIS. Para obter mais informações, consulte [Grupo de Seção system.webServer \[Esquema de Configurações do IIS 7\]](https://go.microsoft.com/fwlink/?LinkId=178353) na Biblioteca MSDN.|  
|`system.serviceModel`|Elemento WCF. Para obter mais informações, consulte [\<system.serviceModel>](https://go.microsoft.com/fwlink/?LinkId=178354) na biblioteca MSDN.|  
|`system.diagnostics`|Elemento .NET Framework. Para obter mais informações, consulte [ \<system.diagnostics> elemento](https://go.microsoft.com/fwlink/?LinkId=178355) na biblioteca MSDN.|  
|`appSettings`|Elemento ASP.NET. Para obter mais informações, consulte [Elemento appSettings (Esquema de Configuração Geral)](https://go.microsoft.com/fwlink/?LinkId=178356) na Biblioteca MSDN.|  
  
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
|`instance`|Elemento filho. Contém atributos que especificam informações para o serviço Web e a cadeia de conexão do banco de dados.|  
|`virtualPath`|Atributo. Especifica o caminho virtual do aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Isso corresponde ao `path` atributo do **\<application>** elemento sob o **\<site>** elemento no arquivo de ApplicationHost.config do IIS.|  
|`siteName`|Atributo. Especifica o nome do site que hospeda o aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Isso corresponde ao `name` atributo do **\<site>** elemento em **\<sites>** no arquivo de ApplicationHost.config do IIS.|  
|`connectionName`|Atributo. Especifica o nome da conexão a usar. Isso corresponde ao `name` atributo do **\<add>** elemento sob o **\<connectionStrings>** elemento em Web.config.|  
|`serviceName`|Atributo. Especifica o nome do serviço Web. Isso corresponde ao `name` atributo do **\<service>** elemento sob o **\<services>** elemento em Web.config.|  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra um serviço chamado MDS1 no site Contoso e no caminho /MDS usando uma cadeia de conexão especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
