---
title: Procedimento armazenado de validação (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 332d3c86-4440-4f12-a6cb-ffbfbccde52c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 89e0b57501eb948d0c67a6dc0a055051b7d19b18
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481336"
---
# <a name="validation-stored-procedure-master-data-services"></a>Procedimento armazenado de validação (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], valide uma versão para aplicar regras de negócio a todos os membros da versão do modelo.  
  
 Este tópico explica como usar o procedimento armazenado **mdm.udpValidateModel** para validar dados. Se você for um administrador no aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , poderá fazer validação na interface do usuário em vez disso. Para obter mais informações, consulte [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md).  
  
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
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|UserID|A ID do usuário.|  
|Model_ID|A ID do modelo.|  
|Version_ID|A ID da versão.|  
  
## <a name="see-also"></a>Consulte Também  
 [Master Data Services de importação de dados &#40;&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md)  
  
  
