---
title: "Referência de configuração (Master Data Services) Web | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1be0e90d7d2ba9b2751677015957ca249d91119e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="web-configuration-reference-master-data-services"></a>Referência de configuração da Web (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]usa um arquivo Web. config para conter as definições de configuração que permitem que os serviços de informações da Internet (IIS) para hospedar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] aplicativo Web e o serviço Web. O arquivo Web.config está localizado na pasta WebApplication do caminho de instalação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obter mais informações sobre o caminho e as permissões, consulte [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos do Web.Config  
 O arquivo Web. config contém um personalizado [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] elemento  **\<masterDataServices >**, além dos elementos de configuração padrão do IIS, .NET Framework, ASP.NET e Windows Communication Foundation (WCF). A tabela a seguir descreve os elementos incluídos no arquivo Web.config.  
  
|Elemento de configuração|Description|  
|---------------------------|-----------------|  
|**masterDataServices**|Elemento personalizado. Conecta o serviço Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**connectionStrings**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento connectionStrings (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178347) na Biblioteca MSDN.|  
|**system.web**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178348) na Biblioteca MSDN.|  
|**inicialização**|Elemento .NET Framework. Para obter mais informações, consulte [ \<inicialização > elemento](http://go.microsoft.com/fwlink/?LinkId=178349) na biblioteca MSDN.|  
|**tempo de execução**|Elemento .NET Framework. Para obter mais informações, consulte [ \<tempo de execução > elemento](http://go.microsoft.com/fwlink/?LinkId=178350) na biblioteca MSDN.|  
|**system.codedom**|Elemento .NET Framework. Para obter mais informações, consulte [ \<System. CodeDom > elemento](http://go.microsoft.com/fwlink/?LinkId=178351) na biblioteca MSDN.|  
|**system.web.extensions**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento system.web.extensions (Esquema de Configuração do ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178352) na Biblioteca MSDN.|  
|**system.webServer**|Grupo de seções que contém elementos IIS. Para obter mais informações, consulte [Grupo de Seção system.webServer \[Esquema de Configurações do IIS 7\]](http://go.microsoft.com/fwlink/?LinkId=178353) na Biblioteca MSDN.|  
|**system.serviceModel**|Elemento WCF. Para obter mais informações, consulte [ \<System. ServiceModel >](http://go.microsoft.com/fwlink/?LinkId=178354) na biblioteca MSDN.|  
|**system.diagnostics**|Elemento .NET Framework. Para obter mais informações, consulte [ \<System. Diagnostics > elemento](http://go.microsoft.com/fwlink/?LinkId=178355) na biblioteca MSDN.|  
|**appSettings**|Elemento ASP.NET. Para obter mais informações, consulte [Elemento appSettings (Esquema de Configuração Geral)](http://go.microsoft.com/fwlink/?LinkId=178356) na Biblioteca MSDN.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 O  **\<masterDataServices >** é um elemento personalizado que é usado para conectar um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] serviço Web um [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] banco de dados.  
  
### <a name="syntax"></a>Sintaxe  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Elementos e atributos  
  
|Item|Description|  
|----------|-----------------|  
|**instância**|Elemento filho. Contém atributos que especificam informações para o serviço Web e a cadeia de conexão do banco de dados.|  
|**virtualPath**|Atributo. Especifica o caminho virtual do aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Isso corresponde ao **caminho** atributo do  **\<aplicativo >** elemento sob o  **\<site >** elemento no arquivo IIS applicationHost. config.|  
|**siteName**|Atributo. Especifica o nome do site que hospeda o aplicativo Web e serviço Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Isso corresponde do **nome** atributo do  **\<site >** elemento em  **\<sites >** no arquivo IIS applicationHost. config.|  
|**connectionName**|Atributo. Especifica o nome da conexão a usar. Isso corresponde ao **nome** atributo do  **\<Adicionar >** elemento sob o  **\<connectionStrings >** elemento no Web. config.|  
|**serviceName**|Atributo. Especifica o nome do serviço Web. Isso corresponde ao **nome** atributo do  **\<serviço >** elemento sob o  **\<services >** elemento no Web. config.|  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra um serviço chamado MDS1 no site Contoso e no caminho /MDS usando uma cadeia de conexão especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
