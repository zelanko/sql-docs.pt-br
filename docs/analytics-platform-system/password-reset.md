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
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539416"
---
# <a name="password-reset---analytics-platform-system"></a>Redefinição de senha - Analytics Platform System
O **de redefinição de senha** página permite que você altere a senha para as contas de administrador usada pelo sistema de plataforma de análise.  
  
> [!WARNING]  
> Use sempre o **do Configuration Manager** para atualizar a senha de administrador de domínio do dispositivo. Outros métodos não podem atualizar todos os componentes do sistema de plataforma de análise e podem causar problemas de acesso ao dispositivo.  
  
Você terá as senhas Analytics Platform System quando o dispositivo é entregue. Altere as senhas para novos valores sempre quando você assumir a responsabilidade de seu dispositivo. Há três senhas para atualizar. As senhas não precisa ser igual ao outro.  
  
**F <*xxxx*> \Administrator**  
O **administrador** do domínio do dispositivo.  
  
**.\Administrator**  
Local **administrador** conta nos computadores que hospedam as máquinas virtuais.  
  
> [!IMPORTANT]  
> Para o dispositivo atualização 1, **do Configuration Manager** não zerar alterar a senha das contas de administrador local em toda a PDW VM. Se isso for necessário, entre em contato com o CSS para obter instruções adicionais.  
  
**sa**  
O **sa** logon no SQL Server. **SA** é membro do **sysadmin** função de servidor fixa e é um administrador do SQL Server. A senha das **sa** logon também pode ser alterado usando o **ALTER LOGIN** instrução.  
  
## <a name="password-requirements"></a>Requisitos de senha  
As credenciais de administrador de domínio e as credenciais de administrador de sistema cumprir as políticas de força de senha para cada tipo de credencial. Ao alterar as credenciais de administrador de domínio, a nova senha é atualizada para o domínio onde necessário ao longo do SQL Server PDW.  
  
> [!IMPORTANT]  
> SQL Server PDW não dá suporte para o caractere de cifrão (**$**) no administrador de domínio ou senhas de administrador local. Os caracteres **^ % &** são permitidos em senhas, no entanto, PowerShell considera como caracteres especiais. Se nenhum desses caracteres usados em senhas para o administrador do sistema ou o SQL Server**sa** contas (o **AdminPassword** e **PdwSAPassword** parâmetros durante a a instalação), em seguida, a instalação, incluindo instalação, atualização, REPLACENODE e a aplicação de patch, falharão. Para garantir uma atualização bem-sucedida quando senhas atuais contêm caracteres sem suporte, altere as senhas para que elas não contêm esses caracteres antes de executar a atualização. Após a conclusão da atualização, você pode definir essas senhas de volta para seus valores originais. Para obter mais informações sobre os requisitos de senha, consulte [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Para redefinir uma senha  
  
1.  Conecte-se o nó de controle e inicie o **do Configuration Manager** (**dwconfig.exe**). Para obter mais informações, consulte [iniciar o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do **do Configuration Manager**, clique em **de redefinição de senha**.  
  
3.  Selecione o tipo de administrador do **conta** menu suspenso e, em seguida, digite a senha nova no **senha** e **Confirmar senha** caixas. Clique em **aplicar** para salvar suas alterações.  
  
    As alterações feitas a essas contas não afetam as sessões atualmente ativas, mas serão aplicadas na próxima tentativa de logon para cada usuário.  
  
    ![SQL Server DWConfig Password](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Consulte também  
[Definir senha de administrador para fazer logon em nós do AD no modo de restauração de serviços de diretório &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
