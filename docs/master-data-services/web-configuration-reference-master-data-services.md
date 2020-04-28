---
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
ms.openlocfilehash: e9d3cd20fc219a7159de0b271dafcc0e9fb2c3ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728833"
---
# <a name="web-configuration-reference-master-data-services"></a>Referência de configuração da Web (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa um arquivo Web.config que contém as definições de configuração que permitem que o IIS (Serviços de Informações da Internet) hospede o serviço Web e o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . O arquivo Web.config está localizado na pasta WebApplication do caminho de instalação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações sobre o caminho e as permissões, consulte [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos do Web.Config  
 O arquivo Web. config contém um elemento [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] personalizado, ** \<masterDataServices>**, além dos elementos de configuração padrão do IIS, .NET Framework, ASP.net e Windows Communication Foundation (WCF). A tabela a seguir descreve os elementos incluídos no arquivo Web.config.  
  
|Elemento de configuração|Descrição|  
|---------------------------|-----------------|  
|**masterDataServices**|Elemento personalizado. Conecta o serviço Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**connectionStrings**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento connectionStrings (Esquema de Configuração do ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178347) na Biblioteca MSDN.|  
|**System. Web**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web (Esquema de Configuração do ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178348) na Biblioteca MSDN.|  
|**inicialização**|Elemento .NET Framework. Para obter mais informações, consulte [ \<o elemento Startup>](https://go.microsoft.com/fwlink/?LinkId=178349) na biblioteca MSDN.|  
|**appmodel**|Elemento .NET Framework. Para obter mais informações, consulte [ \<o elemento Runtime>](https://go.microsoft.com/fwlink/?LinkId=178350) na biblioteca MSDN.|  
|**system.codedom**|Elemento .NET Framework. Para obter mais informações, consulte [ \<o elemento System. CodeDom>](https://go.microsoft.com/fwlink/?LinkId=178351) na biblioteca MSDN.|  
|**System. Web. Extensions**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web.extensions (Esquema de Configuração do ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178352) na Biblioteca MSDN.|  
|**system.webServer**|Grupo de seções que contém elementos IIS. Para obter mais informações, consulte [Grupo de Seção system.webServer \[Esquema de Configurações do IIS 7\]](https://go.microsoft.com/fwlink/?LinkId=178353) na Biblioteca MSDN.|  
|**system.serviceModel**|Elemento WCF. Para obter mais informações, consulte [ \<System. ServiceModel>](https://go.microsoft.com/fwlink/?LinkId=178354) na biblioteca MSDN.|  
|**system.diagnostics**|Elemento .NET Framework. Para obter mais informações, consulte [ \<o elemento System. Diagnostics>](https://go.microsoft.com/fwlink/?LinkId=178355) na biblioteca MSDN.|  
|**appSettings**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento appSettings (Esquema de Configuração Geral)](https://go.microsoft.com/fwlink/?LinkId=178356) na Biblioteca MSDN.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 O ** \<elemento>masterDataServices** é um elemento personalizado usado para conectar um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] serviço Web a um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] banco de dados.  
  
### <a name="syntax"></a>Sintaxe  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Elementos e atributos  
  
|Item|Descrição|  
|----------|-----------------|  
|**cópia**|Elemento filho. Contém atributos que especificam informações para o serviço Web e a cadeia de conexão do banco de dados.|  
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
  
  
