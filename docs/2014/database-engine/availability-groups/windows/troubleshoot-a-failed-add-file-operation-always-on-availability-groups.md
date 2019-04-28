---
title: Solucionar problemas de uma operação de adição de arquivos com falha (grupos de disponibilidade AlwaysOn) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary databases [SQL Server], Availability Groups
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 31ceaebf-864b-4dd0-9112-0d047b0316ad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6940e9e40a09e5bd0c7afc591b34c17129350d74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813436"
---
# <a name="troubleshoot-a-failed-add-file-operation-alwayson-availability-groups"></a>Solução de problemas de uma operação de adicionar arquivos com falha (grupos de disponibilidade de AlwaysOn)
  Em algumas implantações de grupos de disponibilidade AlwaysOn, os caminhos de arquivos diferem entre o sistema que hospeda a réplica primária e os sistemas que hospedam uma réplica secundária. Se o caminho do arquivo de uma operação de adicionar arquivos não existir em uma réplica secundária, a operação de adicionar arquivos terá sucesso no banco de dados primário. Mas a operação de adicionar arquivos fará o banco de dados secundário ser suspenso. Isto, por sua vez, faz a réplica secundária entrar no estado NOT SYNCHRONIZING.  
  
> [!NOTE]  
>  É recomendável que, se possível, o caminho do arquivo (incluindo a letra da unidade) de um determinado banco de dados secundário seja idêntico ao caminho do banco de dados primário correspondente.  
  
## <a name="problem-resolution"></a>Resolução do problema  
 Para resolver esse problema, o proprietário do banco de dados deve concluir as seguintes etapas:  
  
1.  Remover o banco de dados secundário do grupo de disponibilidade. Para obter mais informações, veja [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md).  
  
2.  No banco de dados secundário existente, restaure um backup completo do grupo de arquivos que contém o arquivo adicionado no banco de dados secundário, usando WITH NORECOVERY e WITH MOVE (especificando o caminho de arquivo na instância de servidor que hospeda a réplica secundária). Para obter mais informações, consulte [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md).  
  
3.  Faça backup do log de transações que contém a operação adicionar arquivo no banco de dados primário e restaure manualmente o backup do log no banco de dados secundário usando WITH NORECOVERY e WITH MOVE.  
  
4.  Prepare o banco de dados secundário para reingressar no grupo de disponibilidade, restaurando, WITH NO RECOVERY, todos os backups de log pendentes a partir do banco de dados primário.  
  
5.  Reunindo o banco de dados secundário ao grupo de disponibilidade. Para obter mais informações, veja [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)   
 [Solução de problemas de usuários órfãos &#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;excluído](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
