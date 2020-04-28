---
title: Restaurar banco de dados mestre
description: Restaure o banco de dados mestre no sistema de plataforma de análise (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6d122881f5283da86f66494ee2f049756d151551
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400449"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>Restaurar o banco de dados mestre no sistema de plataforma de análise (APS)
A página **restaurar mestre** do SQL Server PDW Configuration Manager permite que você restaure o banco de dados mestre de um backup.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
> [!IMPORTANT]  
> Para executar a restauração, SQL Server PDW deve excluir o banco de dados mestre atual, que contém informações de segurança do usuário e o catálogo de banco de dados. É recomendável fazer um backup do banco de dados mestre atual antes de executar a restauração.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar o banco de dados mestre  
  
1.  Inicie o Configuration Manager. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;&#41;do sistema de plataforma de análise ](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo da Configuration Manager, clique em **restaurar mestre**.  
  
3.  Selecione o backup mestre a ser restaurado.  
  
4.  Clique em **Aplicar**.  
  
5.  Para executar a restauração, SQL Server PDW desligará todos os serviços do dispositivo e desconectará todos os usuários. Após a conclusão da restauração, SQL Server PDW reiniciará os serviços do dispositivo.  
  
![Mestre de restauração PDW do dispositivo DWConfig](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
