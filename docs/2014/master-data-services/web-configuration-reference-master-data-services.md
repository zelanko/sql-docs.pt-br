---
title: Referência de configuração da Web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f52ca10bd9d857d4e87a54f19cfaa87f1e92575
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130956"
---
# <a name="web-configuration-reference-master-data-services"></a>Referência de configuração da Web (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa um arquivo Web.config que contém as definições de configuração que permitem que o IIS (Serviços de Informações da Internet) hospede o serviço Web e o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . O arquivo Web.config está localizado na pasta WebApplication do caminho de instalação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações sobre o caminho e as permissões, consulte [Permissões de pasta e arquivo &#40;Master Data Services&#41;](folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos do Web.Config  
 O arquivo Web.config contém um elemento [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] personalizado, **\<masterDataServices>**, além dos elementos de configuração padrão IIS, .NET Framework, ASP.NET e WCF (Windows Communication Foundation). A tabela a seguir descreve os elementos incluídos no arquivo Web.config.  
  
|Elemento de configuração|Description|  
|---------------------------|-----------------|  
|`masterDataServices`|Elemento personalizado. Conecta o serviço Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|`connectionStrings`|Elemento ASP.NET. Para obter mais informações, consulte [Elemento connectionStrings (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178347) na Biblioteca MSDN.|  
|`system.web`|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178348) na Biblioteca MSDN.|  
|`startup`|Elemento .NET Framework. Para obter mais informações, consulte [Elemento \<startup>](http://go.microsoft.com/fwlink/?LinkId=178349) na Biblioteca MSDN.|  
|`runtime`|Elemento .NET Framework. Para obter mais informações, consulte [Elemento \<runtime>](http://go.microsoft.com/fwlink/?LinkId=178350) na Biblioteca MSDN.|  
|`system.codedom`|Elemento .NET Framework. Para obter mais informações, consulte [Elemento \<system.codedom>](http://go.microsoft.com/fwlink/?LinkId=178351) na Biblioteca MSDN.|  
|`system.web.extensions`|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web.extensions (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178352) na Biblioteca MSDN.|  
|`system.webServer`|Grupo de seções que contém elementos IIS. Para obter mais informações, consulte [Grupo de Seção system.webServer \[Esquema de Configurações do IIS 7\]](http://go.microsoft.com/fwlink/?LinkId=178353) na Biblioteca MSDN.|  
|`system.serviceModel`|Elemento WCF. Para obter mais informações, consulte [\<system.serviceModel>](http://go.microsoft.com/fwlink/?LinkId=178354) na Biblioteca MSDN.|  
|`system.diagnostics`|Elemento .NET Framework. Para obter mais informações, consulte [Elemento \<system.diagnostics>](http://go.microsoft.com/fwlink/?LinkId=178355) na Biblioteca MSDN.|  
|`appSettings`|Elemento ASP.NET. Para obter mais informações, consulte [Elemento appSettings (Esquema de Configuração Geral)](http://go.microsoft.com/fwlink/?LinkId=178356) na Biblioteca MSDN.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 O elemento **\<masterDataServices>** é um elemento personalizado usado para conectar um serviço Web do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
### <a name="syntax"></a>Sintaxe  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Elementos e atributos  
  
|Item|Description|  
|----------|-----------------|  
|`instance`|Elemento filho. Contém atributos que especificam informações para o serviço Web e a cadeia de conexão do banco de dados.|  
|`virtualPath`|Atributo. Especifica o caminho virtual do aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Isso corresponde à `path` atributo do  **\<aplicativo >** elemento sob o  **\<site >** elemento no arquivo IIS applicationHost. config.|  
|`siteName`|Atributo. Especifica o nome do site que hospeda o aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Isso corresponde à `name` atributo o  **\<site >** sob o elemento  **\<sites >** no arquivo IIS applicationHost. config.|  
|`connectionName`|Atributo. Especifica o nome da conexão a usar. Isso corresponde à `name` atributo do  **\<Adicionar >** elemento sob o  **\<connectionStrings >** elemento no Web. config.|  
|`serviceName`|Atributo. Especifica o nome do serviço Web. Isso corresponde à `name` atributo do  **\<service >** sob o elemento a  **\<services >** elemento no Web. config.|  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra um serviço chamado MDS1 no site Contoso e no caminho /MDS usando uma cadeia de conexão especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
