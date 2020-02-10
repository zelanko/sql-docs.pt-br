---
title: Configurar o banco de dados e o site para Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 478dea9095fe22a437aecf138c22374b5a70885b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054099"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>Instalar o banco de dados e o site para o Master Data Services
  Use o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para instalar o banco de dados e o site do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS)  
  
 Para instalar o banco de dados e o site, conclua as seguintes tarefas.  
  
1.  Crie um banco de dados usando a página configuração [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]de banco de **dados** no.  
  
     Para obter informações, consulte [página de configuração de banco de dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md) e [Assistente para criar banco de dados &#40;](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md)Gerenciador de configuração do Master Data Services&#41;.  
  
2.  Crie um novo site, selecione o site padrão ou selecione outro site existente, usando a página **configuração da Web** no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Em seguida, associe o banco de dados do MDS ao aplicativo Web que você selecionar ou criar.  
  
     Para obter informações, consulte a [página configuração da Web &#40;Gerenciador de Configuração do Master Data Services&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) e a [caixa de diálogo criar site &#40;Gerenciador de configuração do Master Data Services ](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md)&#41;.  
  
3.  Adicional Habilite a integração com o Data Quality Services usando a página [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] **configuração da Web** no.  
  
     Para obter mais informações, consulte a [página de configuração da Web &#40;Gerenciador de Configuração do Master Data Services&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) e [habilitar a integração do Data Quality Services com o Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md).  
  
 Você também pode usar [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para especificar configurações para os aplicativos Web e serviços associados ao banco de dados do MDS. Por exemplo, você pode especificar a frequência com que os dados são carregados ou os emails de validação são enviados. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Banco de dados Master Data Services](../../2014/master-data-services/master-data-services-database.md)   
 [Aplicativo Web Master Data Manager](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
