---
title: Definir a senha do Active Directory - Analytics Platform System | Microsoft Docs
description: Definir senha de logon de administrador do Active Directory nós no modo de restauração dos serviços de diretório no Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3df6203a4d98bace5d23a92e70a596a34dedb60e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678351"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>Definir senha de administrador para fazer logon em nós nos serviços de diretório do AD restaurar o modo (DSRM) - Analytics Platform System
Directory Services Restore DSRM (modo) é um modo de inicialização para reparo ou recuperação de serviços de domínio Active Directory (AD DS). Ele é usado para fazer logon para os nós de dispositivo AD depois que o AD DS falhou ou quando o AD DS precisa ser restaurado. A senha do DSRM foi inicializada durante a configuração de dispositivo no site do fornecedor de hardware e deve ser alterada pelo administrador do dispositivo. O Analytics Platform System tem dois AD DS (controladores de domínio);  **_appliance_domain_-AD01** e  **_appliance_domain_-AD02**. Para cada nó de dispositivo do AD, altere a senha do DSRM usando as etapas a seguir.  
  
## <a name="HowToDSRM"></a>Para redefinir a senha de administrador  
  
1.  Abra uma janela de Prompt de comando em um nó de dispositivo do AD  <strong>_appliance_domain_-AD_xx_</strong>máquina virtual.  
  
2.  No prompt de comando, digite `ntdsutil`.  
  
3.  Com o **ntdsutil** , digite `set dsrm password`.  
  
4.  No **redefinição de senha do administrador:** , digite `reset password on server null`.  
  
5.  No prompt, digite a nova senha.  
  
6.  Repita as etapas 1 a 5 acima para cada máquina virtual de dispositivo do AD.  
  
    > [!WARNING]  
    > O Analytics Platform System não suporta o caractere de cifrão ($) no administrador de domínio ou senhas de administrador local. Uma senha que contenha um cifrão validará e ser utilizáveis mas podem bloquear atividades de atualização e manutenção.  
  
> [!NOTE]  
> Se os serviços de domínio do Active Directory ou a máquina virtual for corrompida para uma máquina virtual AD, executando **ReplaceVM** para o AD afetado a máquina virtual é a ação corretiva recomendada. Entre em contato com CSS para obter assistência.  
  
## <a name="see-also"></a>Consulte também  
[Redefinição de senha &#40;Analytics Platform System&#41;](password-reset.md)  
  
