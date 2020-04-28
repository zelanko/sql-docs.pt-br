---
title: Redefinição de senha
description: A página de redefinição de senha permite que você altere a senha das contas de administrador usadas pelo sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 952dbda04b4f7132406e3a6de4479afea1be92e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400902"
---
# <a name="password-reset---analytics-platform-system"></a>Redefinição de senha-sistema de plataforma de análise
A página de **redefinição de senha** permite que você altere a senha das contas de administrador usadas pelo sistema de plataforma de análise.  
  
> [!WARNING]  
> Sempre use o **Configuration Manager** para atualizar a senha do administrador de domínio do dispositivo. Outros métodos podem não atualizar todos os componentes do Analytics Platform System e causar problemas de acesso ao dispositivo.  
  
Você recebe as senhas do sistema de plataforma de análise quando o dispositivo é entregue. Sempre altere as senhas para novos valores quando você assumir a responsabilidade pelo seu dispositivo. Há três senhas a serem atualizadas. As senhas não precisam ser as mesmas.  
  
**F<*xxxx*> \Administrador**  
O **administrador** do domínio do dispositivo.  
  
**.\Administrator**  
A conta de **administrador** local nos computadores que hospedam as máquinas virtuais.  
  
> [!IMPORTANT]  
> Para a atualização 1 do dispositivo, **Configuration Manager** não altera corretamente a senha das contas de administrador local em todas as VMs do PDW. Se isso for necessário, entre em contato com o CSS para obter instruções adicionais.  
  
**sa**  
O logon do **SA** no SQL Server. **SA** é um membro da função de servidor fixa **sysadmin** e é um administrador de SQL Server. A senha do logon **SA** também pode ser alterada usando a instrução **ALTER LOGIN** .  
  
## <a name="password-requirements"></a>Requisitos de senha  
As credenciais de administrador de domínio e as credenciais de administrador do sistema aderem às políticas de força de senha para cada tipo de credencial. Ao alterar as credenciais de administrador de domínio, a nova senha é atualizada para o domínio onde necessário durante SQL Server PDW.  
  
> [!IMPORTANT]  
> SQL Server PDW não dá suporte ao caractere de cifrão (**$**) nas senhas de administrador de domínio ou de administrador local. Os caracteres **^% &** são permitidos em senhas, no entanto, o PowerShell considera como caracteres especiais. Se qualquer um desses caracteres for usado em senhas para o administrador do sistema ou SQL Server contas**SA** (os parâmetros **AdminPassword** e **PdwSAPassword** durante a instalação), a instalação, incluindo instalação, atualização, REPLACENODE e aplicação de patches, falhará. Para garantir uma atualização bem-sucedida quando as senhas atuais contiverem caracteres sem suporte, altere essas senhas para que elas não contenham esses caracteres antes de executar a atualização. Após a conclusão da atualização, você pode definir essas senhas de volta para seus valores originais. Para obter mais informações sobre os requisitos de senha, consulte [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Para redefinir uma senha  
  
1.  Conecte-se ao nó de controle e inicie o **Configuration Manager** (**dwconfig. exe**). Para obter mais informações, consulte [iniciar o Configuration Manager &#40;&#41;do sistema de plataforma de análise ](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo da **Configuration Manager**, clique em **redefinição de senha**.  
  
3.  Selecione o tipo de administrador no menu suspenso **conta** e, em seguida, insira a nova senha nas caixas **senha** e **Confirmar senha** . Clique em **aplicar** para salvar as alterações.  
  
    As alterações feitas nessas contas não afetam as sessões ativas no momento, mas serão aplicadas na próxima tentativa de logon para cada usuário.  
  
    ![Senha do SQL Server DWConfig](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Consulte Também  
[Defina a senha de administrador para fazer logon em nós do AD no Modo de Restauração dos Serviços de Diretório &#40;DSRM&#41; &#40;sistema de plataforma de análise&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Inicie o Configuration Manager &#40;o sistema de plataforma de análise&#41;](launch-the-configuration-manager.md)  
  
