---
title: "Página de configuração (Gerenciador de configuração do Master Data Services) da Web | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 32cc0f559017846efbc349377255634e89515c7d
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>Página Configuração da Web (Gerenciador de Configuração do Master Data Services)
  Use a página **Configuração Web** para configurar um site e aplicativo Web. Você também pode habilitar os Serviços de Qualidade de Dados.  
  
## <a name="configure-the-web-application"></a>Configurar o aplicativo Web  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Site**|Crie um novo site, selecione o site padrão ou selecione outro site disponível (se estiver listado). Esta lista exibe os sites que são definidos no ISS (Serviços de Informações da Internet) no computador local. Quando você cria um novo site, um novo aplicativo Web é criado automaticamente. Quando você selecionar o padrão ou outro site existente, crie um aplicativo manualmente.|  
|**Aplicativo Web**|Selecione um aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para configuração. Esta caixa mostra os aplicativos Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] apenas no site selecionado.<br /><br /> Se nada for exibido, clique em **Criar** para criar um site.|  
|**Criar**|Abre a caixa de diálogo **Criar Aplicativo Web** , na qual você cria um aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] no site selecionado. Este botão é habilitado apenas quando o site selecionado não tem aplicativo Web raiz configurado como o aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .|  
  
## <a name="associate-application-with-database"></a>Associar um aplicativo ao banco de dados  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Select (selecionar)**|Abre a caixa de diálogo **Conectar ao Servidor** , na qual você se conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e seleciona um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para associar ao aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selecionado.|  
|**Instância do SQL Server**|Exibe o nome da instância selecionada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que hospeda o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Esse é um espaço em branco até você se conectar a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selecionar um banco de dados.|  
|**Banco de dados**|Exibe o nome do banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] associado ao aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selecionado. Esse é um espaço em branco até você se conectar a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selecionar um banco de dados.|  
  
## <a name="enable-dqs-integration"></a>Habilitar a integração DQS  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Habilitar a integração com o Data Quality Services**|Selecione esta opção para habilitar a funcionalidade de qualidade de dados disponível no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Para obter mais informações, consulte [Enable Data Quality Services Integration with Master Data Services](../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md).|  
  
## <a name="see-also"></a>Consulte também  
[Configuração e instalação do Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md) [Web requisitos de aplicativo &#40; Master Data Services &#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Criar um aplicativo Web Master Data Manager &#40; Master Data Services &#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
