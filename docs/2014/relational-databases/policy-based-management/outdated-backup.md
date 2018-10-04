---
title: Backup desatualizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ab9ff4990c3e2ce3444f241522d928f5c97003b9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203226"
---
# <a name="outdated-backup"></a>Backup desatualizado
  Esta regra verifica se um banco de dados possui backups recentes. Programar backups regulares é importante para proteger os bancos de dados contra perda de dados de muitas falhas diferentes. A frequência apropriada para fazer backup de dados depende do modelo de recuperação do banco de dados, dos requisitos do negócio sobre uma possível perda de dados e da frequência em que o banco de dados é atualizado. Em um banco de dados atualizado frequentemente, a exposição à perda de trabalho aumenta rapidamente entre backups.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Recomendamos que você execute backups com frequência para proteger os bancos de dados contra perda de dados.  
  
 O modelo de recuperação simples e modelo de recuperação completa exigem backups de dados. Para qualquer modelo de recuperação, é possível complementar os backups completos com backups diferenciais para reduzir com eficiência o risco de perda de dados.  
  
 Para um banco de dados que usa o modelo de recuperação completa, recomendamos que faça backups de log frequentes. Para um banco de dados de produção que contém dados muito importantes, os backups de log normalmente são feitos em intervalos de um a quinze minutos.  
  
> [!NOTE]  
>  O método recomendado para agendar backups é um plano de manutenção de banco de dados.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [Modelos de recuperação &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)  
  
 [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [Planos de manutenção](../maintenance-plans/maintenance-plans.md)  
  
 [Backups de log de transações &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
