---
title: SQL Server, objeto Dispositivo de Backup | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ec64b929da7e8e6be90f2b99b93b18adc89ce932
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329405"
---
# <a name="sql-server-backup-device-object"></a>SQL Server, objeto Backup Device
  O objeto **Backup Device** oferece contadores para monitorar dispositivos de backup do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizados para operações de backup e restauração. Monitore os dispositivos de backup quando quiser determinar a taxa de transferência ou o andamento e o desempenho de operações de backup e restauração por dispositivo. Para monitorar a taxa de transferência da operação de backup ou restauração inteira do banco de dados, use o contador **Taxa de Transferência de Backup/Restauração/s** do objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Databases** object. Para obter mais informações, consulte [SQL Server, Databases Object](sql-server-databases-object.md).  
  
 Esta tabela descreve o contador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** .  
  
|Contadores do Dispositivo de Backup do SQL Server|Description|  
|---------------------------------------|-----------------|  
|**Taxa de Transferência do Dispositivo em Bytes/s**|Taxa de transferência de operações de leitura e gravação (em bytes por segundo) de um dispositivo de backup utilizado no backup ou restauração de bancos de dados. Este contador só existe enquanto a operação de backup ou restauração está em execução.|  
  
## <a name="see-also"></a>Consulte também  
 [Dispositivos de backup &#40;SQL Server&#41;](../backup-restore/backup-devices-sql-server.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
