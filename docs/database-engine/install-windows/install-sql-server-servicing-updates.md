---
title: Instalar as atualizações de manutenção do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 290a3a9d307e19820af7f59cd5d6f821bcefc1a3
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412779"
---
# <a name="install-sql-server-servicing-updates"></a>Instalar as atualizações de manutenção do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece informações sobre como instalar atualizações para o [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]. Esta seção fornece informações sobre o seguinte:
  
- Instalando atualizações para o [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] durante uma nova instalação  
  
- Instalando atualizações para o [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] depois que já tiver sido instalado.  
  
Instale as atualizações mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o mais rápido possível para ter certeza de que os sistemas estejam atualizados com as atualizações de segurança mais recentes.  
  
## <a name="installing-updates-for-includenoversionincludesssnoversion-mdmd-during-a-new-installation"></a>Instalando atualizações para o [!INCLUDE[noVersion](../../includes/ssNoVersion-md.md)] durante uma nova instalação  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra as últimas atualizações de produto com a instalação principal de produto, de forma que o produto principal e suas atualizações aplicáveis sejam instalados ao mesmo tempo. A atualização de produto pode pesquisar as atualizações aplicáveis de:  
  
- [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (atualizar)  
  
- Windows Server Update Services (WSUS)  
  
- Uma pasta local  
  
- Um compartilhamento de rede  
  
Depois que a Instalação localizar as versões mais recentes das atualizações aplicáveis, ela baixará e integrará essas atualizações com o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. A Atualização de Produto pode incluir uma atualização cumulativa, service pack ou service pack mais atualização cumulativa.  
  
## <a name="installing-updates-for-includessnoversionincludesssnoversion-mdmd-after-it-has-already-been-installed"></a>Instalando atualizações para o [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] depois que já tiver sido instalado  
Em uma instância instalada do [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)], recomendamos que você aplique as últimas atualizações de segurança e atualizações críticas, incluindo GDRs (versões de distribuição geral), SPs (service packs) e CUs (atualizações cumulativas). Para obter mais informações, consulte o [Comunicado de março de 2016 sobre o ISM (Modelo de Manutenção Incremental) do SQL Server](https://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/).

> [!NOTE]
> A partir do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], adotamos um ciclo de vida de manutenção base simplificado e previsível e os SPs (service packs) não estarão mais disponíveis. Somente os CUs (atualizações cumulativas) e os GDRs (versões de distribuição geral), quando necessário.
> Para obter mais informações, consulte o [Comunicado de setembro de 2017 sobre o MSM (Modelo de Manutenção Moderna) para o SQL Server](https://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server/).
  
As atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão disponíveis com a atualização do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (MU), o Windows Server Update Services (WSUS) e o Centro de Download da Microsoft. As atualizações de segurança e atualizações críticas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão disponíveis pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update e, para ver estas atualizações, você precisará optar pelo MU por meio do applet do Windows Update no Painel de Controle.  
  
Quando você receber uma atualização por meio do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, atualizará todos os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a versão mais recente em um modo autônomo. Se precisar de mais flexibilidade ou não tiver Internet ou acesso WSUS, você precisará obter as atualizações no Centro de Download da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[Instalar o SQL Server por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)        
[Adicionar recursos a uma instância do SQL Server &#40;instalação&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)         
[Reparar uma instalação com falha do SQL Server](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)  

