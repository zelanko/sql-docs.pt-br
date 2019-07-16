---
title: Inicie o Gerenciador de configuração - Analytics Platform System | Microsoft Docs
description: Instruções para iniciar a ferramenta Configuration Manager para o dispositivo do Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7aef9ada4a93605460cf2759dbe9deeddfc9e0d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960722"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>Inicie o Gerenciador de configurações no Analytics Platform System
Este tópico fornece instruções para iniciar o **Configuration Manager** para o dispositivo do Analytics Platform System.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Pré-requisitos  
O Analytics Platform System**Configuration Manager** só pode ser executado pelo administrador de domínio do dispositivo. Para executar essa ferramenta, você precisa da senha para o administrador de domínio do dispositivo. Para criar outros administradores APS, consulte [criar um administrador de domínio de APS &#40;pontos de acesso&#41;](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>Inicie a ferramenta Configuration Manager  
Para executar o Gerenciador de configuração, usar a área de trabalho remota para conectar-se ao nó de controle do PDW ( **_PDW_region_-CTL01**) nós e logon como _appliance_domain_ **\Administrator**. Ao iniciar o **Configuration Manager** de programa, use o **executar como administrador** opção para garantir que suas credenciais de administrador são usadas.  
  
#### <a name="to-launch-from-a-browser-window"></a>Ao iniciar a partir de uma janela do navegador  
  
1.  Abra um navegador e navegue até o diretório `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
2.  Clique com botão direito `dwconfig.exe` e, em seguida, clique em **executar como administrador**.  
  
#### <a name="to-launch-from-a-command-prompt"></a>Para iniciar o prompt de comando  
  
1.  Na área de trabalho, abra o **inicie** menu, clique em **programas**, clique em **Acessórios**, clique com botão direito **Prompt de comando** e, em seguida, clique em  **Executar como administrador**.  
  
2.  No prompt de comando, digite o seguinte comando para alterar os diretórios: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`.  
  
3.  No prompt de comando, digite `dwconfig.exe`.  
  
Após o **Configuration Manager** é iniciado, você verá todas as funcionalidades disponíveis listadas no painel esquerdo. O restante desta seção descreve como realizar cada ação disponível na ferramenta.  
  
Para fechar e sair **Configuration Manager**, clique em **sair** no canto inferior direito de qualquer tela.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>Consulte também  
[Monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
