---
title: "Criar Classes de Proxy de serviço Web Master Data Manager | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a45cd15ced90aef95feb03f8fbaafd5aa70cb746
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>Criar classes proxy do serviço Web do Master Data Manager
  O serviço Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] permite a você fazer uso programático dos recursos do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] de qualquer computador que possa acessar seu site do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Antes de começar a gravar código para acessar o serviço Web, você deve gerar classes proxy. A classe proxy principal que você usa para executar operações de serviço Web é a classe <xref:Microsoft.MasterDataServices.ServiceClient>, que implementa a interface <xref:Microsoft.MasterDataServices.IService>.  
  
## <a name="enable-web-service-metadata-publishing"></a>Habilitar a publicação de metadados de serviço Web  
 Antes de gerar classes proxy, você deve habilitar a publicação de metadados de serviço Web. Siga estas etapas para fazer isso:  
  
1.  Abra o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] arquivo Web. config em um editor de texto. Esse arquivo está na pasta WebApplication, no caminho de instalação do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Localizar o **mdsWsHttpBehavior** seção em ** \<serviceBehaviors >**. Para o ** \<serviceMetadata >** elemento, defina **httpGetEnabled** para **true**.  
  
    > [!NOTE]  
    >  Se você quiser habilitar serviços Web sobre SSL Secure Sockets Layer (), defina **httpsGetEnabled** para **true** no **mdsWsHttpBehavior** seção do arquivo Web. config. Você também precisa alterar **mdsWsHTTPBinding** para que ele seja configurado para SSL, também e comente a seção não SSL.  
  
3.  Salve as alterações no arquivo.  
  
4.  Publicação de metadados de teste, navegando até a URL do serviço, por exemplo: `http://yourserver/MDS/service/service.svc`. Se a publicação de metadados estiver habilitada, será exibida uma página que começa com   
    “Você criou um serviço”.  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Criando classes proxy usando o Visual Studio  
 Se você tiver o Visual Studio 2010 instalado, a maneira mais simples de gerar classes proxy é adicionar um **referência de serviço** ao seu projeto. O endereço da referência do serviço é a URL do aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], com /service/service.svc. Por exemplo: `http://yourserver/MDS/service/service.svc`. Para obter mais informações, consulte [como: adicionar, atualizar ou remover uma referência de serviço](http://go.microsoft.com/fwlink/?LinkId=221167).  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Criando classes proxy usando Svcutil.exe  
 Você deve ter o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK instalado para ter o Svcutil.exe em seu computador. Se você usar o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], deverá usar o prompt de comando do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para executar o comando. Para obter mais informações, consulte [Ferramenta Utilitária de metadados ServiceModel (Svcutil.exe)](http://go.microsoft.com/fwlink/?LinkId=165027) e [gerando um cliente WCF de metadados de serviço](http://go.microsoft.com/fwlink/?LinkId=164821).  
  
 Para criar um conjunto de classes proxy C# usando Svcutil.exe, utilize um comando como o seguinte:  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 Onde:  
  
-   *servername*:*porta* são o nome do computador e número da porta do computador que hospeda [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].  
  
-   *virtual_path* é o caminho virtual do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] em serviços de informações da Internet (IIS).  
  
-   *proxy_name* é o nome do arquivo proxy gerado.  
  
## <a name="see-also"></a>Consulte também  
 [Operações de serviço Web categorizadas & #40; Master Data Services & #41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
