---
title: Inicie o Gerenciador de configuração - Analytics Platform System | Microsoft Docs
description: Instruções para iniciar a ferramenta Gerenciador de configuração para o dispositivo Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d2e7a726386aa64d04f87f30cd22328900b1e5cd
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>Inicie o Gerenciador de configuração no sistema de plataforma de análise
Este tópico fornece instruções para iniciar o **do Configuration Manager** para o dispositivo Analytics Platform System.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
O Analytics Platform System**do Configuration Manager** só pode ser executado pelo administrador de domínio do dispositivo. Para executar essa ferramenta, a senha é necessária para o administrador de domínio do dispositivo. Para criar outros administradores APS, consulte [criar um administrador de domínio APS &#40;APS&#41;](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>Inicie a ferramenta Configuration Manager  
Para executar o Gerenciador de configuração, use a área de trabalho remota para conectar-se ao nó de controle do PDW (***PDW_region *-CTL01**) nó e fazer logon como * appliance_domain ***\administrator**. Ao iniciar o **do Configuration Manager** de programa, use o **executar como administrador** opção para garantir que suas credenciais de administrador são usadas.  
  
#### <a name="to-launch-from-a-browser-window"></a>Para iniciar a partir de uma janela do navegador  
  
1.  Abra um navegador e navegue até o diretório `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
2.  Clique com botão direito `dwconfig.exe` e, em seguida, clique em **executar como administrador**.  
  
#### <a name="to-launch-from-a-command-prompt"></a>Para iniciar a partir de um prompt de comando  
  
1.  Na área de trabalho, abra o **iniciar** menu, clique em **programas**, clique em **Acessórios**, clique com botão direito **Prompt de comando** e, em seguida, clique em  **Executar como administrador**.  
  
2.  No prompt de comando, digite o seguinte comando para alterar os diretórios: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`.  
  
3.  No prompt de comando, digite `dwconfig.exe`.  
  
Após o **do Configuration Manager** é iniciado, você verá todas as funcionalidades disponíveis listadas no painel esquerdo. O restante desta seção descreve como realizar cada ação disponível na ferramenta.  
  
Para fechar e encerrar **do Configuration Manager**, clique em **sair** no canto inferior direito da tela de qualquer.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>Consulte também  
[Monitorar o dispositivo usando o Console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
