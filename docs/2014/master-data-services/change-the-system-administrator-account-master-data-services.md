---
title: Alterar a conta de administrador do sistema (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], changing
ms.assetid: cf30312e-4338-49a7-90f0-6e4f7b431ff8
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a6d15bf7b140445ca80f23fe22e058a78d6fdce0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298606"
---
# <a name="change-the-system-administrator-account-master-data-services"></a>Alterar a conta de administrador do sistema (Master Data Services)
  Você pode alterar a conta de usuário que é designada como o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] administrador do sistema.  
  
> [!WARNING]  
>  Quando esse procedimento for concluído, a conta de usuário de administrador do sistema anterior será excluída.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve adicionar o nome de usuário do novo administrador à lista Usuários do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Para obter mais informações, consulte [adicionar um usuário &#40;Master Data Services&#41;](add-a-user-master-data-services.md).  
  
-   Você deve ter permissão para exibir mdm.tblUser e para executar o procedimento armazenado mdm.udpSecurityMemberProcessRebuildModel no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obter mais informações, consulte [Segurança do objeto de banco de dados &#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md).  
  
### <a name="to-change-the-administrator-account"></a>Para alterar a conta de administrador  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e conecte-se à instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] de seu banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Em tbluser, localize o usuário que será o novo administrador e copie o valor no `SID` coluna.  
  
3.  Crie uma nova consulta.  
  
4.  Digite o texto a seguir, substituindo *DOMAIN\user_name* com o novo nome de usuário administrador e *SID* com o valor que você copiou na etapa 2.  
  
    ```  
    EXEC [mdm].[udpSecuritySetAdministrator] @UserName='DOMAIN\user_name', @SID = 'SID', @PromoteNonAdmin = 1  
    ```  
  
5.  Executa a consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Os administradores de &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
  
