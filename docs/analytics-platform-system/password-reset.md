---
title: Redefinição de senha - Analytics Platform System | Microsoft Docs
description: A página de redefinição de senha permite que você altere a senha para as contas de administrador usada pelo sistema de plataforma de análise.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 63fbb097bf1ca926223ce7c0114c8da5d10cd969
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639943"
---
# <a name="password-reset---analytics-platform-system"></a>Redefinição de senha - Analytics Platform System
O **redefinição de senha** página permite que você altere a senha para as contas de administrador usada pelo sistema de plataforma de análise.  
  
> [!WARNING]  
> Sempre use a **Configuration Manager** para atualizar a senha de administrador de domínio do dispositivo. Outros métodos não poderão ser atualizados para todos os componentes do Analytics Platform System e pode causar problemas de acesso do dispositivo.  
  
Você recebe as senhas do Analytics Platform System quando o dispositivo é entregue. Sempre altere as senhas para novos valores quando você assume a responsabilidade para o seu dispositivo. Há três senhas para atualizar. As senhas não precisa ser o mesmo que uns aos outros.  
  
**F<*xxxx*>\Administrator**  
O **administrador** do domínio do dispositivo.  
  
**.\Administrator**  
O local **administrador** conta nos computadores que hospedam as máquinas virtuais.  
  
> [!IMPORTANT]  
> Para o dispositivo de atualização 1, **Configuration Manager** não zerar alterar a senha das contas de administrador local em todo o PDW VM. Se isso for necessário, entre em contato com o CSS para obter instruções adicionais.  
  
**sa**  
O **sa** logon no SQL Server. **SA** é um membro do **sysadmin** função de servidor fixa e é um administrador do SQL Server. A senha das **sa** logon também pode ser alterado usando o **ALTER LOGIN** instrução.  
  
## <a name="password-requirements"></a>Requisitos de senha  
As credenciais de administrador de domínio e as credenciais de administrador de sistema seguem as políticas de força de senha para cada tipo de credencial. Ao alterar as credenciais de administrador de domínio, a nova senha é atualizada para o domínio onde for necessário em todo o SQL Server PDW.  
  
> [!IMPORTANT]  
> SQL Server PDW não suporta o caractere de cifrão (**$**) no administrador de domínio ou senhas de administrador local. Os caracteres **^ % &** são permitidos em senhas, no entanto, PowerShell considera como caracteres especiais. Se qualquer um desses caracteres são usados em senhas para o administrador do sistema ou do SQL Server**sa** contas (o **AdminPassword** e **PdwSAPassword** parâmetros durante a a instalação), em seguida, a instalação, incluindo instalação, atualização, REPLACENODE e a aplicação de patch, falhará. Para garantir uma atualização bem-sucedida quando senhas atuais contêm caracteres sem suporte, altere essas senhas para que eles não contêm esses caracteres antes de executar a atualização. Após a conclusão da atualização, você pode definir essas senhas de volta para seus valores originais. Para obter mais informações sobre os requisitos de senha, consulte [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Para redefinir uma senha  
  
1.  Conectar-se no nó de controle e inicie o **Configuration Manager** (**dwconfig.exe**). Para obter mais informações, consulte [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do **Configuration Manager**, clique em **de redefinição de senha**.  
  
3.  Selecione o tipo de administrador do **conta** menu suspenso e, em seguida, insira a nova senha na **senha** e **Confirmar senha** caixas. Clique em **aplicar** para salvar suas alterações.  
  
    As alterações feitas a essas contas não afetam as sessões ativas no momento, mas serão aplicadas na próxima tentativa de logon para cada usuário.  
  
    ![SQL Server DWConfig Password](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Consulte também  
[Definir senha de administrador para fazer logon em nós do AD no modo de restauração de serviços de diretório &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
