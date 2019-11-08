---
title: Caixa de diálogo Criar Aplicativo Web
ms.custom: seo-lt-2019
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createapp.f1
ms.assetid: e045b41a-4836-47f6-8e78-2b09494b461f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b35c47704915ec9e85f0c4f2ac083bfb7a6017ac
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729510"
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>Caixa de diálogo Criar Aplicativo Web (Gerenciador de Configuração do Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use a caixa de diálogo **Criar Aplicativo Web** para criar o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Esse aplicativo Web é criado no site que você selecionou na página **Configuração da Web** .  
  
## <a name="web-application"></a>Aplicativo Web  
 O servidor Web entrega o conteúdo para esse aplicativo Web por meio da pasta [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **WebApplication** folder in the file system. Esse local é especificado durante a Instalação e, por padrão, o caminho é *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|Caminho virtual|Selecione o caminho virtual no qual você deseja criar o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Um caminho virtual faz parte da URL que é usada para acessar um aplicativo Web.<br /><br /> Esta lista está filtrada para exibir apenas caminhos virtuais de aplicativos nos quais o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] pode ser criado. Não é possível criar um aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] em outro aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].|  
|Alias|Digite um nome para o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ou use o nome padrão. Esse nome é usado em uma URL para acessar o aplicativo Web em um navegador da Web.|  
  
## <a name="application-pool"></a>Pool de Aplicativos  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Nome**|Digite um nome amigável e exclusivo para um novo pool de aplicativos ou use o nome padrão. O aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] é adicionado a esse pool de aplicativos.<br /><br /> Os pools de aplicativos fornecem limites que impedem que os aplicativos em um pool de aplicativos afetem aplicativos em outro pool de aplicativos.|  
|**Nome de usuário**|Digite um domínio e nome de usuário do Active Directory. Essa conta de serviço é a identidade do pool de aplicativos no qual o aplicativo Web é executado. Esta conta deve ser a mesma conta especificada como a conta de serviço quando o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] foi criado.<br /><br /> Essa conta é adicionada à função de banco de dados mds_exec no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para acesso ao banco de dados. Para obter mais informações, veja [Logons, usuários e funções de banco de dados &#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md). Também é adicionada a um grupo do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] no Windows, **MDS_ServiceAccounts**, que recebe permissão para o diretório temporário de compilação, **MDSTempDir**, no sistema de arquivos. Para obter mais informações, veja [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Senha**|Digite a senha da conta de usuário especificada.|  
|**Confirmar senha**|Digite novamente a senha da conta de usuário especificada. Os campos **Senha** e **Confirmar senha** devem conter a mesma senha.|  
  
## <a name="see-also"></a>Consulte também  
 [Página Configuração da Web &#40;Master Data Services Configuration Manager&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Instalação e configuração do Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)[Requisitos do aplicativo Web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
