---
title: Definir Active Directory senha
description: Defina os nós de Active Directory senha de logon do administrador em Modo de Restauração dos Serviços de Diretório no sistema de plataforma de análise (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbbf42106602a25b03072a9c9abfb04f04d3c49
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400330"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>Definir a senha de administrador para fazer logon em nós do AD no Modo de Restauração dos Serviços de Diretório (DSRM)-sistema de plataforma de análise
O Modo de Restauração dos Serviços de Diretório (DSRM) é um modo de inicialização para reparar ou recuperar Active Directory Domain Services (AD DS). Ele é usado para fazer logon nos nós do dispositivo AD após a AD DS falhar ou quando AD DS precisar ser restaurado. A senha do DSRM foi inicializada durante a configuração do dispositivo no site do fornecedor de hardware e deve ser alterada pelo administrador do dispositivo. O sistema de plataforma de análise tem duas AD DS (controladores de domínio); ** _appliance_domain_-AD01** e ** _appliance_domain_-AD02**. Para cada nó de dispositivo do AD, altere a senha do DSRM usando as etapas a seguir.  
  
## <a name="HowToDSRM"></a>Para redefinir a senha do administrador  
  
1.  Abra uma janela de prompt de comando em um nó de anúncio de dispositivo <strong> _appliance_domain_-AD_xx_</strong>máquina virtual.  
  
2.  No prompt de comando, digite `ntdsutil`.  
  
3.  No prompt do **Ntdsutil** , digite `set dsrm password`.  
  
4.  Na tela **Redefinir senha do administrador:** , digite `reset password on server null`.  
  
5.  No prompt, digite a nova senha.  
  
6.  Repita as etapas 1-5 acima para cada máquina virtual do AD do dispositivo.  
  
    > [!WARNING]  
    > O Analytics Platform System não dá suporte ao caractere de cifrão ($) nas senhas de administrador de domínio ou de administrador local. Uma senha contendo um cifrão será validada e poderá ser usada, mas pode bloquear atividades de atualização e manutenção.  
  
> [!NOTE]  
> Se o Active Directory Domain Services ou a máquina virtual for corrompida para uma máquina virtual específica do AD, a execução de **ReplaceVM** para a máquina virtual do AD afetada será a ação corretiva recomendada. Contate o CSS para obter assistência.  
  
## <a name="see-also"></a>Consulte Também  
[Redefinição de senha &#40;sistema de plataforma de análise&#41;](password-reset.md)  
  
