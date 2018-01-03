---
title: "Procedimento armazenado de validação (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 332d3c86-4440-4f12-a6cb-ffbfbccde52c
caps.latest.revision: "8"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72b676c8bd9b0cee4b55c9bcd45a8089db7a6bcd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="validation-stored-procedure-master-data-services"></a>Procedimento armazenado de validação (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], valide uma versão para aplicar regras de negócio a todos os membros da versão do modelo.  
  
 Este tópico explica como usar o procedimento armazenado **mdm.udpValidateModel** para validar dados. Se você for um administrador no aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , poderá fazer validação na interface do usuário em vez disso. Para obter mais informações, consulte [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
> [!NOTE]  
>  Se você invocar a validação antes de o processo de preparo ser concluído, os membros que não concluíram o preparo não serão validados.  
  
## <a name="example"></a>Exemplo  
  
```  
DECLARE @ModelName nVarchar(50) = 'Customer'   
DECLARE @Model_id int   
DECLARE @UserName nvarchar(50)= 'DOMAIN\user_name'   
DECLARE @User_ID int   
DECLARE @Version_ID int   
  
SET @User_ID = (SELECT ID    
                 FROM mdm.tblUser u   
                 WHERE u.UserName = @UserName)   
SET @Model_ID = (SELECT Top 1 Model_ID   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_Name = @ModelName)   
SET @Version_ID = (SELECT MAX(ID)   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_ID = @Model_ID)  
  
EXECUTE mdm.udpValidateModel @User_ID, @Model_ID, @Version_ID, 1  
  
```  
  
## <a name="parameters"></a>Parâmetros  
 Os parâmetros desse procedimento são os seguintes:  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|UserID|A ID do usuário.|  
|Model_ID|A ID do modelo.|  
|Version_ID|A ID da versão.|  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
  
