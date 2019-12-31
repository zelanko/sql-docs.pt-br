---
title: Iniciar Configuration Manager
description: Instruções para iniciar a ferramenta de Configuration Manager para o dispositivo de sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 421265abcf3731ed48ff34a6b199ba5cd3c6af5c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401051"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>Iniciar o Configuration Manager no Analytics Platform System
Este tópico fornece instruções para iniciar o **Configuration Manager** para o dispositivo de sistema de plataforma de análise.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Pré-requisitos  
O**Configuration Manager** do sistema de plataforma de análise só pode ser executado pelo administrador de domínio do dispositivo. Para executar essa ferramenta, você precisa da senha para o administrador do domínio do dispositivo. Para criar administradores de APS adicionais, consulte [criar um administrador de domínio aps &#40;aps&#41;](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>Iniciar a ferramenta de Configuration Manager  
Para executar o Configuration Manager, use Área de Trabalho Remota para se conectar ao nó de controle do PDW (**_PDW_region_-CTL01**) e faça logon como _appliance_domain_**\Administrador**. Ao iniciar o programa de **Configuration Manager** , use a opção **Executar como administrador** para garantir que suas credenciais de administrador sejam usadas.  
  
#### <a name="to-launch-from-a-browser-window"></a>Para iniciar a partir de uma janela do navegador  
  
1.  Abra um navegador e navegue até o diretório `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
2.  Clique `dwconfig.exe` com o botão direito do mouse em e clique em **Executar como administrador**.  
  
#### <a name="to-launch-from-a-command-prompt"></a>Para iniciar a partir de um prompt de comando  
  
1.  Na área de trabalho, abra o menu **Iniciar** , clique em **programas**, clique em **acessórios**, clique com o botão direito do mouse em **prompt de comando** e clique em **Executar como administrador**.  
  
2.  No prompt de comando, digite o seguinte comando para alterar os diretórios `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`:.  
  
3.  No prompt de comando, digite `dwconfig.exe`.  
  
Depois que o **Configuration Manager** for iniciado, você verá todas as funcionalidades disponíveis listadas no painel esquerdo. O restante desta seção discute como executar cada ação disponível na ferramenta.  
  
Para fechar e sair **Configuration Manager**, clique em **sair** no canto inferior direito de qualquer tela.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>Consulte Também  
[Monitore o dispositivo usando o console de administração &#40;o sistema de plataforma de análise&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
