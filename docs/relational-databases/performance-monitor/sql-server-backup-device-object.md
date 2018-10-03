---
title: SQL Server, objeto Dispositivo de Backup | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b622b17b19d3fedf192eecc1d976330c685752c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602744"
---
# <a name="sql-server-backup-device-object"></a>SQL Server, objeto Backup Device
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O objeto **Backup Device** oferece contadores para monitorar dispositivos de backup do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizados para operações de backup e restauração. Monitore os dispositivos de backup quando quiser determinar a taxa de transferência ou o andamento e o desempenho de operações de backup e restauração por dispositivo. Para monitorar a taxa de transferência da operação de backup ou restauração inteira do banco de dados, use o contador **Taxa de Transferência de Backup/Restauração/s** do objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Databases** object. Para obter mais informações, consulte [SQL Server, Databases Object](../../relational-databases/performance-monitor/sql-server-databases-object.md).  
  
 Esta tabela descreve o contador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** .  
  
|Contadores do Dispositivo de Backup do SQL Server|Descrição|  
|---------------------------------------|-----------------|  
|**Taxa de Transferência do Dispositivo em Bytes/s**|Taxa de transferência de operações de leitura e gravação (em bytes por segundo) de um dispositivo de backup utilizado no backup ou restauração de bancos de dados. Este contador só existe enquanto a operação de backup ou restauração está em execução.|  
  
## <a name="see-also"></a>Consulte Também  
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
