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
manager: craigg
ms.openlocfilehash: 07f438f86a22b866351a0b83ee7634338f3ad2cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775339"
---
# <a name="install-sql-server-2014-servicing-updates"></a>Instalar atualizações de serviço do SQL Server 2014
  Este tópico fornece informações sobre como instalar atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esta seção fornece informações sobre o seguinte:  
  
-   Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante uma nova instalação  
  
-   Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depois que já tiver sido instalado.  
  
 Nós recomendamos que os clientes avaliem e instalem as atualizações mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o mais rápido possível para ter certeza de que os sistemas estejam atualizados com as atualizações de segurança mais recentes.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-during-a-new-installation"></a>Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante uma nova instalação  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra as últimas atualizações de produto com a instalação principal de produto, de forma que o produto principal e suas atualizações aplicáveis sejam instalados ao mesmo tempo. A atualização de produto pode pesquisar as atualizações aplicáveis de:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (atualizar)  
  
-   Windows Server Update Services (WSUS)  
  
-   Uma pasta local  
  
-   Um compartilhamento de rede  
  
 Depois que a Instalação localizar as versões mais recentes das atualizações aplicáveis, ela baixará e integrará essas atualizações com o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. A Atualização de Produto pode incluir uma atualização cumulativa, service pack ou service pack mais atualização cumulativa. A funcionalidade Atualização de Produto é uma extensão da [funcionalidade de instalação integrada](https://go.microsoft.com/fwlink/?LinkId=219945) que estava disponível no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depois que já tiver sido instalado  
 Em uma instância instalada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é recomendável que você aplique todas as atualizações disponíveis: Versões de distribuição geral (GDR - atualizações críticas/de segurança), Service Packs (SP), bem como a mais recente disponível atualização cumulativa (CU).  
  
 Dependendo do tipo de versão de serviço, as atualizações do SQL Server estão disponíveis por meio do Microsoft Update (MU), Microsoft Download Center e/ou o hotfix de serviços de atendimento ao servidor. Atualizações críticas e de segurança para o SQL Server são fornecidas automaticamente pelo Microsoft Update (deve ser capaz de ver estas atualizações que necessárias para participar de MU por meio do Windows Update no painel de controle). Service Packs estão disponíveis no MU como opcional/importante baixa, bem como o Centro de Download. As atualizações cumulativas estão disponíveis no servidor de download do hotfix do Microsoft fornecido nos artigos da Base de dados de conhecimento do CU.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o SQL Server 2014 do Assistente de instalação &#40;programa de instalação&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [Instalando atualizações do prompt de comando](installing-updates-from-the-command-prompt.md) [adicionar recursos a uma instância do SQL Server 2014 &#40;programa de instalação&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [Remover uma instalação do SQL Server 2014](repair-a-failed-sql-server-installation.md)  
  
  
