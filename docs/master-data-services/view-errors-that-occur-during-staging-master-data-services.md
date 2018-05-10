---
title: Exibir erros que ocorrem durante o preparo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 63fd428b3f6ce1cb59420dc1dfa4f0e10bd20137
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="view-errors-that-occur-during-staging-master-data-services"></a>Exibir erros que ocorrem durante o preparo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode exibir os erros ocorridos durante o processo de preparo. No banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , há duas exibições que mostram erros:  
  
-   stg.viw_name_MemberErrorDetails para atualizações de membro folha ou consolidado.  
  
-   stg.viw_name_RelationshipErrorDetails para atualizações de relação de hierarquia.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   No banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , você deve ter permissões SELECT para a exibição stg.viw_name_MemberErrorDetails ou stg.viw_name_RelationshipErrorDetails.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-view-staging-errors"></a>Para exibir erros de preparo  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e conecte-se à instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] de seu banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Abra uma nova consulta.  
  
3.  Digite o texto a seguir, substituindo name pelo nome de sua tabela de preparo, por exemplo, viw_Product_MemberErrorDetails.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  Execute a consulta. Os detalhes do erro são exibidos no campo **ErrorDescription** .  
  
## <a name="next-steps"></a>Next Steps  
 Para obter mais detalhes sobre mensagens de erro, consulte [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Solucionando problemas do processo de preparo (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
