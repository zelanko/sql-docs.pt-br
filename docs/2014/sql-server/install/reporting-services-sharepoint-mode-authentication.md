---
title: Reporting Services a autenticação do modo do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade SharePoint Mode [Reporting Services]
- SharePoint integration
- SharePoint Mode
ms.assetid: 2c19794a-dd55-4fe5-b901-6dd93e9f6beb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ff0a4f38bf9ee7d9c27fbc07308084ed3272f95d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952097"
---
# <a name="reporting-services-sharepoint-mode-authentication"></a>Reporting Services no modo de autenticação do SharePoint
  Use a página **Autenticação do modo do SharePoint do Reporting Services** do Assistente de instalação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar as credenciais da conta do serviço que é usado na instalação atual do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As credenciais serão usadas para criar um novo pool de aplicativos do SharePoint. Além disso, um novo aplicativo de serviço SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será criado. O nome do aplicativo de serviço conterá o nome da instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anterior.  
  
## <a name="options"></a>Opções  
  
-   A opção **Nome da conta do pool de aplicativos do SSRS:** é somente leitura. O valor é automaticamente populado com o valor atual da instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] existente que você está atualizando.  
  
-   A opção **Senha da conta do pool de aplicativos do SSRS:** será desabilitada se a conta do pool de aplicativos não exigir uma senha. Por exemplo, "NT Authority\NetworkService". Se a conta do pool de aplicativos exigir uma senha, você só poderá continuar com a atualização se digitar a senha correta.  
  
 Para obter mais informações, consulte [atualizar e migrar Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628) (https://go.microsoft.com/fwlink/?LinkID=245628).  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizar e migrar o Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628)  
  
  
