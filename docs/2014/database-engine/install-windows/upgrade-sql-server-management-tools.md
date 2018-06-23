---
title: Fazer upgrade das Ferramentas de Gerenciamento do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- management tools, upgrading
ms.assetid: 1dab50b9-d16c-49a1-9ecc-af72adb6c378
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1cfdd0e84020a3cb9eb919b9ac5e9d8ed0055938
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130399"
---
# <a name="upgrade-sql-server-management-tools"></a>Atualizar Ferramentas de Gerenciamento do SQL Server
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dá suporte à atualização do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior. Este tópico documenta o suporte e o comportamento da atualização das Ferramentas de Gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dos componentes de gerenciamento, tais como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, Database Mail, Maintenance Plans, XPStar e XPWeb.  
  
> [!IMPORTANT]  
>  Em instalações locais, você deve executar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um administrador. Se você executar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e execução no compartilhamento remoto.  
  
## <a name="known-upgrade-issues"></a>Problemas de atualização conhecidos  
 Considere os seguintes problemas antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
### <a name="for-all-upgrade-scenarios"></a>Para todos os cenários de atualização:  
  
-   Todos os servidores TSX devem ser atualizados antes que o servidor MSX seja atualizado. Para obter mais informações sobre MSX/TSX no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md).  
  
-   Todos os componentes de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser atualizados ao mesmo tempo. Os números de versão dos componentes do [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem ser os mesmos em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   É possível adicionar componentes a uma instalação existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no momento em que você atualiza para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [atualizar para o SQL Server 2014 usando o Assistente de instalação &#40;instalação&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As Ferramentas de Cliente, tais como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]e o Orientador de otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , sqlcmd e osql não são atualizadas para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. As Ferramentas de Cliente são executadas lado a lado com ferramentas de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dá suporte a configurações de importação de versões anteriores de Ferramentas de Cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   A autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será atualizada da Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a Autenticação do Windows durante a atualização. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Não há suporte à autenticação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Os dados de trabalhos e alertas serão preservados durante a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Se o SQLMail estiver sendo usado na instância a ser atualizada, depois da atualização haverá suporte para os XPs associados e eles serão habilitados. Caso contrário, eles ficarão desligados.  
  
-   O Database Mail, também conhecido como SQLiMail, será atualizado com o componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Por padrão, o Database Mail será desligado após a atualização. Quaisquer atualizações de esquema devem ser reconciliadas com um script de atualização após a atualização.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizações de versão e edição com suporte](supported-version-and-edition-upgrades.md)   
 [Compatibilidade com versões anteriores](../../getting-started/backward-compatibility.md)   
 [Atualizar para o SQL Server 2014 usando o Assistente de instalação &#40;instalação&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  