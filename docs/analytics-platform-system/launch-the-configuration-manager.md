---
title: "Inicie o Gerenciador de configuração (Analytics Platform System)"
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
ms.assetid: b914ba9a-e4ec-4750-934a-c447fc8909e3
caps.latest.revision: "22"
ms.openlocfilehash: 2ead82cd226a585d261eac2779cacb72cd5edbb6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="launch-the-configuration-manager"></a>Inicie o Gerenciador de configuração
Este tópico fornece instruções para iniciar o **do Configuration Manager** para o dispositivo Analytics Platform System.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
O Analytics Platform System**do Configuration Manager** só pode ser executado pelo administrador de domínio do dispositivo. Para executar essa ferramenta, a senha é necessária para o administrador de domínio do dispositivo. Para criar outros administradores APS, consulte [criar um administrador de domínio APS &#40; APS &#41; ](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>Inicie a ferramenta Configuration Manager  
Para executar o Gerenciador de configuração, use a área de trabalho remota para conectar-se ao nó de controle do PDW (***PDW_region*-CTL01**) nó e fazer logon como *appliance_domain* **\Administrator**. Ao iniciar o **do Configuration Manager** de programa, use o **executar como administrador** opção para garantir que suas credenciais de administrador são usadas.  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Monitorar o dispositivo usando o Console de administração &#40; Analytics Platform System &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
