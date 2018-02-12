---
title: "Criar um administrador de domínio de pontos de acesso (APS)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed52bf78-2b0a-4252-98a7-8c2805e22d3d
caps.latest.revision: 
ms.openlocfilehash: 0ebc616d28fe734b9dac52303641390ce9bc0957
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="create-an-aps-domain-administrator"></a>Criar um administrador de domínio APS
Algumas operações exigem privilégios de administrador de domínio Analytics Platform System. Explica como criar administradores de domínio de dispositivo adicionais.  
  
## <a name="create-a-domain-administrator"></a>Criar um administrador de domínio  
Ter permissões suficientes para configurar todos os nós de pontos de acesso, o usuário que executa o **APS Configuration Manager** (`dwconfig.exe`) deve ser um membro do **Admins. do domínio** grupo. Para iniciar e parar os serviços de pontos de acesso, o usuário deve ser um membro do **PdwControlNodeAccess** grupo.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Para adicionar um usuário ao grupo Admins. do domínio  
  
1.  Faça logon no nó ativo do AD **(*appliance_domain*-AD01** ou ***appliance_domain *-AD02**) usando uma conta de administrador de domínio existente do dispositivo.  
  
2.  No menu Iniciar, clique em **Executar**. No **abrir** , digite **dsa.msc**. Clique em **OK**.  
  
3.  No **computadores e usuários do Active Directory** de programa, clique no **usuários**, aponte para **novo**e, em seguida, clique em **usuário**.  
  
4.  No **novo objeto – usuário** caixa de diálogo, a descrição do novo usuário completa e, em seguida, clique em **próximo**.  
  
    Preencha a caixa de diálogo senha e, em seguida, clique em **próximo**.  
  
    > [!WARNING]  
    > SQL Server PDW não dá suporte para o caractere de cifrão ($) no administrador de domínio ou senhas de administrador local. Uma senha que contém um sinal de cifrão será válida e ser usado, mas pode bloquear a atualização e atividades de manutenção  
  
    Confirme a nova descrição de usuário e, em seguida, clique em **concluir**.  
  
5.  Na lista de usuários, clique duas vezes o novo usuário para abrir a caixa de diálogo de propriedades do usuário.  
  
6.  Sobre o **membro de** , clique em **adicionar**.  
  
    Tipo **Admins. do domínio; PdwControlNodeAccess** e, em seguida, clique em **verificar nomes**. Clique em **OK**.  
  
    Isso adiciona o novo usuário para o **Admins. do domínio** grupo e o **PdwControlNodeAccess** grupo. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
[Inicie o Gerenciador de configuração &#40; Analytics Platform System &#41;](launch-the-configuration-manager.md)  
  
