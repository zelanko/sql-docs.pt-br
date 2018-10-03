---
title: Referência de configuração da Web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
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
ms.openlocfilehash: 6f57d1cc99a2966ea220774366cca8aa6e2f8049
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834948"
---
# <a name="web-configuration-reference-master-data-services"></a>Referência de configuração da Web (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa um arquivo Web.config que contém as definições de configuração que permitem que o IIS (Serviços de Informações da Internet) hospede o serviço Web e o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . O arquivo Web.config está localizado na pasta WebApplication do caminho de instalação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações sobre o caminho e as permissões, consulte [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos do Web.Config  
 O arquivo Web.config contém um elemento [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] personalizado, **\<masterDataServices>**, além dos elementos de configuração padrão IIS, .NET Framework, ASP.NET e WCF (Windows Communication Foundation). A tabela a seguir descreve os elementos incluídos no arquivo Web.config.  
  
|Elemento de configuração|Descrição|  
|---------------------------|-----------------|  
|**masterDataServices**|Elemento personalizado. Conecta o serviço Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**connectionStrings**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento connectionStrings (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178347) na Biblioteca MSDN.|  
|**system.web**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178348) na Biblioteca MSDN.|  
|**inicialização**|Elemento .NET Framework. Para obter mais informações, consulte [Elemento \<startup>](http://go.microsoft.com/fwlink/?LinkId=178349) na Biblioteca MSDN.|  
|**tempo de execução**|Elemento .NET Framework. Para obter mais informações, consulte [Elemento \<runtime>](http://go.microsoft.com/fwlink/?LinkId=178350) na Biblioteca MSDN.|  
|**system.codedom**|Elemento .NET Framework. Para obter mais informações, consulte [Elemento \<system.codedom>](http://go.microsoft.com/fwlink/?LinkId=178351) na Biblioteca MSDN.|  
|**system.web.extensions**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web.extensions (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178352) na Biblioteca MSDN.|  
|**system.webServer**|Grupo de seções que contém elementos IIS. Para obter mais informações, consulte [Grupo de Seção system.webServer \[Esquema de Configurações do IIS 7\]](http://go.microsoft.com/fwlink/?LinkId=178353) na Biblioteca MSDN.|  
|**system.serviceModel**|Elemento WCF. Para obter mais informações, consulte [\<system.serviceModel>](http://go.microsoft.com/fwlink/?LinkId=178354) na Biblioteca MSDN.|  
|**system.diagnostics**|Elemento .NET Framework. Para obter mais informações, consulte [Elemento \<system.diagnostics>](http://go.microsoft.com/fwlink/?LinkId=178355) na Biblioteca MSDN.|  
|**appSettings**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento appSettings (Esquema de Configuração Geral)](http://go.microsoft.com/fwlink/?LinkId=178356) na Biblioteca MSDN.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 O elemento **\<masterDataServices>** é um elemento personalizado usado para conectar um serviço Web do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a um banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
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
|**virtualPath**|Atributo. Especifica o caminho virtual do aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Isso corresponde ao atributo **path** do elemento **\<application>** sob o elemento **\<site>** no arquivo IIS ApplicationHost.config.|  
|**siteName**|Atributo. Especifica o nome do site que hospeda o aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Isso corresponde ao atributo **name** do elemento **\<site>** sob o elemento **\<sites>** no arquivo IIS ApplicationHost.config.|  
|**connectionName**|Atributo. Especifica o nome da conexão a usar. Isso corresponde ao atributo **name** do elemento **\<add>** sob o elemento **\<connectionStrings>** em Web.config.|  
|**serviceName**|Atributo. Especifica o nome do serviço Web. Isso corresponde ao atributo **name** do elemento **\<service>** sob o elemento **\<services>** em Web.config.|  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra um serviço chamado MDS1 no site Contoso e no caminho /MDS usando uma cadeia de conexão especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
