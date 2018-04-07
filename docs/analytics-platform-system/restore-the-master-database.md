---
title: Restaurar o banco de dados mestre (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7870021a-0d89-422e-b8ea-1cc95b45c139
caps.latest.revision: 11
ms.openlocfilehash: 0f1acb692198873897d5dc26e2074beab4517e44
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="restore-the-master-database"></a>Restaurar o banco de dados mestre
O **mestre de restauração** página do SQL Server PDW Configuration Manager permite que você restaure o banco de dados mestre de um backup.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
> [!IMPORTANT]  
> Para executar a restauração, SQL Server PDW deve excluir o atual banco de dados mestre, que contém informações de segurança do usuário e o catálogo de banco de dados. É recomendável fazer um backup de banco de dados mestre atual antes de executar a restauração.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar o banco de dados mestre  
  
1.  Inicie o Gerenciador de configuração. Para obter mais informações, consulte [iniciar o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do Gerenciador de configuração, clique em **mestre de restauração**.  
  
3.  Selecione o backup mestre para restaurar.  
  
4.  Clique em **Aplicar**.  
  
5.  Para executar a restauração, SQL Server PDW será desligar todos os serviços do dispositivo e desconecte todos os usuários. Após a conclusão da restauração, o SQL Server PDW irá reiniciar os serviços do dispositivo.  
  
![DWConfig Appliance PDW Restore master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
