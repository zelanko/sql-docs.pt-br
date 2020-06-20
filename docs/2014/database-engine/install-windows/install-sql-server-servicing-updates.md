---
title: Instalar atualizações de serviço do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0c36fbe634fbc2b17547f127290cfbaed6e745c7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932505"
---
# <a name="install-sql-server-2014-servicing-updates"></a>Instalar atualizações de serviço do SQL Server 2014
  Este tópico fornece informações sobre como instalar atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esta seção fornece informações sobre o seguinte:  
  
-   Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante uma nova instalação  
  
-   Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depois que já tiver sido instalado.  
  
 Nós recomendamos que os clientes avaliem e instalem as atualizações mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o mais rápido possível para ter certeza de que os sistemas estejam atualizados com as atualizações de segurança mais recentes.  
  
## <a name="installing-updates-for-sscurrent-during-a-new-installation"></a>Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante uma nova instalação  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra as últimas atualizações de produto com a instalação principal de produto, de forma que o produto principal e suas atualizações aplicáveis sejam instalados ao mesmo tempo. A atualização de produto pode pesquisar as atualizações aplicáveis de:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (atualizar)  
  
-   Windows Server Update Services (WSUS)  
  
-   Uma pasta local  
  
-   Um compartilhamento de rede  
  
 Depois que a Instalação localizar as versões mais recentes das atualizações aplicáveis, ela baixará e integrará essas atualizações com o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. A Atualização de Produto pode incluir uma atualização cumulativa, service pack ou service pack mais atualização cumulativa. A funcionalidade Atualização de Produto é uma extensão da [funcionalidade de instalação integrada](https://go.microsoft.com/fwlink/?LinkId=219945) que estava disponível no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1.  
  
## <a name="installing-updates-for-sscurrent-after-it-has-already-been-installed"></a>Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depois que já tiver sido instalado  
 Em uma instância instalada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , recomendamos que você aplique todas as atualizações disponíveis: lançamentos de distribuição geral (atualizações de segurança/crítica GDR), Service Packs (SP), bem como a atualização cumulativa mais recente disponível (cu).  
  
 Dependendo do tipo de versão de serviço, SQL Server atualizações estão disponíveis via Microsoft Update (MU), o centro de download da Microsoft e/ou o servidor de hotfix dos serviços de atendimento ao cliente. As atualizações de segurança e críticas para SQL Server são fornecidas automaticamente pelo Microsoft Update (para poder ver essas atualizações, você precisa aceitar o MU por meio de Windows Update no painel de controle). Os service packs estão disponíveis no MU como downloads opcionais/importantes, bem como no centro de download. As atualizações cumulativas estão disponíveis no Microsoft hotfix Download Server fornecido em CU artigos da base de dados de conhecimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Instale o SQL Server 2014 do assistente de instalação &#40;a instalação&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 A [instalação de atualizações do prompt de comando](installing-updates-from-the-command-prompt.md) [adiciona recursos a uma instância do SQL Server 2014 &#40;instalação&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [Remover uma instalação do SQL Server 2014](repair-a-failed-sql-server-installation.md)  
  
  
