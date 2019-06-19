---
title: Criar um administrador de domínio - Analytics Platform System | Microsoft Docs
description: Algumas operações exigem privilégios de administrador de domínio do Analytics Platform System. Isso explica como criar os administradores de domínio de dispositivo adicionais.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 852fb3c6cee7c65f8799102bbd65ab368cd0d9e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63134373"
---
# <a name="create-an-aps-domain-administrator"></a>Criar um administrador de domínio APS
Algumas operações exigem privilégios de administrador de domínio do Analytics Platform System. Isso explica como criar os administradores de domínio de dispositivo adicionais.  
  
## <a name="create-a-domain-administrator"></a>Criar um administrador de domínio  
Ter permissões suficientes para configurar todos os nós APS, o usuário que executa o **APS Configuration Manager** (`dwconfig.exe`) deve ser um membro do **Admins. do domínio** grupo. Para iniciar e parar os serviços de pontos de acesso, o usuário deve ser um membro do **PdwControlNodeAccess** grupo.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Para adicionar um usuário ao grupo Admins. do domínio  
  
1.  Faça logon no nó ativo do AD **(_appliance\_domínio_-AD01** ou  **_appliance\_domínio_-AD02**) usando uma conta de administrador de domínio existente do dispositivo.  
  
2.  No menu Iniciar, clique em **Executar**. No **aberto** , digite **DSA. msc**. Clique em **OK**.  
  
3.  No **Active Directory Users and Computers** programa, clique com botão direito **usuários**, aponte para **New**e, em seguida, clique em **usuário**.  
  
4.  No **novo objeto - usuário** caixa de diálogo, a descrição do novo usuário completa e, em seguida, clique em **próxima**.  
  
    Complete a caixa de diálogo de senha e, em seguida, clique em **próxima**.  
  
    > [!WARNING]  
    > SQL Server PDW não dá suporte para o caractere de cifrão ($) no administrador de domínio ou senhas de administrador local. Uma senha que contenha um cifrão será válida e ser utilizável, mas pode bloquear atividades de atualização e manutenção  
  
    Confirme a nova descrição de usuário e, em seguida, clique em **concluir**.  
  
5.  Na lista de usuários, clique duas vezes o novo usuário para abrir a caixa de diálogo de propriedades do usuário.  
  
6.  Sobre o **membro de** , clique em **Add**.  
  
    Tipo **Admins. do domínio; PdwControlNodeAccess** e, em seguida, clique em **verificar nomes**. Clique em **OK**.  
  
    Isso adiciona o novo usuário para o **Admins. do domínio** grupo e o **PdwControlNodeAccess** grupo. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
