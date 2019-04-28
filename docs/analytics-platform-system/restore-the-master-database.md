---
title: Restaurar o banco de dados mestre - Analytics Platform System | Microsoft Docs
description: Restaure o banco de dados mestre no Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 184184f332225e76e152c2d909cfff788b4fea91
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678440"
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>Restaurar o banco de dados mestre no Analytics Platform System
O **mestre de restauração** página do SQL Server PDW Configuration Manager permite que você restaure o banco de dados mestre de um backup.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
> [!IMPORTANT]  
> Para executar a restauração, SQL Server PDW deve excluir o atual banco de dados mestre, que contém informações de segurança do usuário e o catálogo de banco de dados. É recomendável fazer um backup de banco de dados mestre atual antes de executar a restauração.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar o banco de dados mestre  
  
1.  Inicie o Gerenciador de configuração. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do Gerenciador de configuração, clique em **mestre de restauração**.  
  
3.  Selecione o backup mestre para restaurar.  
  
4.  Clique em **Aplicar**.  
  
5.  Para executar a restauração, SQL Server PDW desligará todos os serviços do dispositivo e desconecte todos os usuários. Após a conclusão da restauração, SQL Server PDW reiniciará os serviços do dispositivo.  
  
![DWConfig Appliance PDW Restore master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
