---
title: Definir senha do Active Directory - Analytics Platform System | Microsoft Docs
description: Definir senha de logon do administrador do Active Directory nós no modo de restauração dos serviços de diretório Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e74689216c1485fc0c11c588acb151269e2b5d2b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>Definir senha de administrador para fazer logon no AD nós nos serviços de diretório restaurar modo (DSRM) - Analytics Platform System
Modo de restauração de serviços de diretório (DSRM) é um modo de inicialização para reparo ou recuperação de serviços de domínio Active Directory (AD DS). Ele é usado para fazer logon em nós de dispositivo AD após a falha do AD DS ou quando o AD DS precisa ser restaurado. A senha do DSRM foi inicializada durante a configuração de dispositivo no site do fornecedor de hardware e deve ser alterada pelo administrador do dispositivo. Analytics Platform System tem dois AD DS (controladores de domínio); ***appliance_domain *-AD01** e ***appliance_domain *-AD02**. Para cada nó de dispositivo AD, altere a senha do DSRM usando as etapas a seguir.  
  
## <a name="HowToDSRM"></a>Para redefinir a senha de administrador  
  
1.  Abra uma janela de Prompt de comando em um nó de dispositivo AD ***appliance_domain*– AD*xx***máquina virtual.  
  
2.  No prompt de comando, digite `ntdsutil`.  
  
3.  No **ntdsutil** , digite `set dsrm password`.  
  
4.  No **redefinir a senha do administrador:** , digite `reset password on server null`.  
  
5.  No prompt, digite a nova senha.  
  
6.  Repita as etapas 1 a 5 acima para cada máquina virtual de utilitário AD.  
  
    > [!WARNING]  
    > Sistema de plataforma de análise não oferece suporte para o caractere de cifrão ($) no administrador de domínio ou senhas de administrador local. Uma senha que contém um sinal de cifrão será validar e ser utilizável mas podem bloquear a atualização e atividades de manutenção.  
  
> [!NOTE]  
> Se os serviços de domínio Active Directory ou a máquina virtual for corrompida para uma máquina virtual AD, executando **ReplaceVM** para o AD afetado máquina virtual é a ação corretiva recomendada. Entre em contato com CSS para obter assistência.  
  
## <a name="see-also"></a>Consulte também  
[Redefinição de senha &#40;Analytics Platform System&#41;](password-reset.md)  
  
