---
title: Restaurar banco de dados mestre-APS (sistema de plataforma de análise) | Microsoft Docs
description: Restaure o banco de dados mestre no sistema de plataforma de análise (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 624e1199fb953945ae6476a1f935dded48508bab
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176140"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>Restaurar o banco de dados mestre no sistema de plataforma de análise (APS)
A página **restaurar mestre** do SQL Server PDW Configuration Manager permite que você restaure o banco de dados mestre de um backup.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
> [!IMPORTANT]  
> Para executar a restauração, SQL Server PDW deve excluir o banco de dados mestre atual, que contém informações de segurança do usuário e o catálogo de banco de dados. É recomendável fazer um backup do banco de dados mestre atual antes de executar a restauração.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar o banco de dados mestre  
  
1.  Inicie o Configuration Manager. Para obter mais informações, consulte [iniciar o &#40;Configuration Manager Analytics Platform&#41;System](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo da Configuration Manager, clique em **restaurar mestre**.  
  
3.  Selecione o backup mestre a ser restaurado.  
  
4.  Clique em **Aplicar**.  
  
5.  Para executar a restauração, SQL Server PDW desligará todos os serviços do dispositivo e desconectará todos os usuários. Após a conclusão da restauração, SQL Server PDW reiniciará os serviços do dispositivo.  
  
![Mestre de restauração do PDW do dispositivo DWConfig](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
