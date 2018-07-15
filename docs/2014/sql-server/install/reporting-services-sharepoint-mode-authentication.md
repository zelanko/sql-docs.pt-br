---
title: Reporting Services a autenticação de modo do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Upgrade SharePoint Mode [Reporting Services]
- SharePoint integration
- SharePoint Mode
ms.assetid: 2c19794a-dd55-4fe5-b901-6dd93e9f6beb
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 704d104b8834675f7511c952db7fafb9fcccafd3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247806"
---
# <a name="reporting-services-sharepoint-mode-authentication"></a>Reporting Services no modo de autenticação do SharePoint
  Use a página **Autenticação do modo do SharePoint do Reporting Services** do Assistente de instalação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar as credenciais da conta do serviço que é usado na instalação atual do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As credenciais serão usadas para criar um novo pool de aplicativos do SharePoint. Além disso, um novo aplicativo de serviço SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será criado. O nome do aplicativo de serviço conterá o nome da instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anterior.  
  
## <a name="options"></a>Opções  
  
-   A opção **Nome da conta do pool de aplicativos do SSRS:** é somente leitura. O valor é automaticamente populado com o valor atual da instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] existente que você está atualizando.  
  
-   A opção **Senha da conta do pool de aplicativos do SSRS:** será desabilitada se a conta do pool de aplicativos não exigir uma senha. Por exemplo, “NT Authority\NetworkSerivce”. Se a conta do pool de aplicativos exigir uma senha, você só poderá continuar com a atualização se digitar a senha correta.  
  
 Para obter mais informações, consulte [Upgrade and Migrate Reporting Services](http://go.microsoft.com/fwlink/?LinkID=245628) (http://go.microsoft.com/fwlink/?LinkID=245628).  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar e migrar o Reporting Services](http://go.microsoft.com/fwlink/?LinkID=245628)  
  
  
