---
title: Criar um administrador de domínio
description: Algumas operações exigem privilégios de administrador de domínio de sistema de plataforma de análise. Isso explica como criar administradores de domínio de dispositivo adicionais.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1a0d50e485f0e8f48de11b2e5a3c27c9f9be047e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401231"
---
# <a name="create-an-aps-domain-administrator"></a>Criar um administrador de domínio APS
Algumas operações exigem privilégios de administrador de domínio de sistema de plataforma de análise. Isso explica como criar administradores de domínio de dispositivo adicionais.  
  
## <a name="create-a-domain-administrator"></a>Criar um administrador de domínio  
Para ter permissões suficientes para configurar todos os nós APS, o usuário que executa o **APS Configuration Manager** (`dwconfig.exe`) deve ser um membro do grupo **Admins** . do domínio. Para iniciar e parar os serviços APS, o usuário deve ser um membro do grupo **PdwControlNodeAccess** .  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Para adicionar um usuário ao grupo Admins. do domínio  
  
1.  Faça logon no nó ativo do AD **(_domínio do dispositivo\__– AD01** ou domínio do ** _dispositivo\__-AD02**) usando uma conta de administrador de domínio do dispositivo existente.  
  
2.  No menu Iniciar, clique em **Executar**. Na caixa **abrir** , digite **DSA. msc**. Clique em **OK**.  
  
3.  No **Active Directory programa usuários e computadores** , clique com o botão direito do mouse em **usuários**, aponte para **novo**e clique em **usuário**.  
  
4.  Na caixa de diálogo **novo objeto – usuário** , conclua a descrição do novo usuário e clique em **Avançar**.  
  
    Preencha a caixa de diálogo senha e clique em **Avançar**.  
  
    > [!WARNING]  
    > SQL Server PDW não dá suporte ao caractere de cifrão ($) nas senhas de administrador de domínio ou de administrador local. Uma senha contendo um cifrão será válida e poderá ser usada, mas poderá bloquear as atividades de atualização e manutenção  
  
    Confirme a descrição do novo usuário e clique em **concluir**.  
  
5.  Na lista de usuários, clique duas vezes no novo usuário para abrir a caixa de diálogo Propriedades do usuário.  
  
6.  Na guia **Membro de**, clique em **Adicionar**.  
  
    Digite **Administradores de domínio; PdwControlNodeAccess** e clique em **verificar nomes**. Clique em **OK**.  
  
    Isso adiciona o novo usuário ao grupo **Admins** . do domínio e ao grupo **PdwControlNodeAccess** . Clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
[Inicie o Configuration Manager &#40;o sistema de plataforma de análise&#41;](launch-the-configuration-manager.md)  
  
