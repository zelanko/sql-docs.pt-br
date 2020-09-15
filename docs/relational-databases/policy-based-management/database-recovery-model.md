---
title: Modelo de Recuperação de Banco de Dados
description: Saiba como habilitar uma política para verificar o modelo de recuperação de backup para bancos de dados de usuários a fim de reduzir a perda de dados.
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 048fa8d28e32ad73aa9e2a85e217f268fa865a3c
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284883"
---
# <a name="database-recovery-model"></a>Modelo de recuperação de banco de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Para as edições SQL Server Enterprise e Standard, esta regra verifica os bancos de dados de usuários que não são somente leitura cuja recuperação está definida como simples. Para bancos de dados de produção, recomendamos o uso do modelo de recuperação completa em vez do modelo de recuperação simples. O modo de recuperação completa habilita a recuperação pontual. Isto ajuda reduzir perda de dados no caso da recuperação de um desastre.
  
## <a name="best-practices-recommendations"></a>Recomendações de melhores práticas  
 Bancos de dados de produção devem sempre estar no modo de recuperação completa e é necessário executar backups frequentes dos logs de transações para ajudar a garantir a recuperação com perdas mínimas de dados.
  
## <a name="see-also"></a>Veja também 
  
 [Visão geral da restauração e recuperação](../backup-restore/restore-and-recovery-overview-sql-server.md)   
  
 [Restaurações completas de banco de dados (modelo de recuperação completa)](../backup-restore/complete-database-restores-full-recovery-model.md)  

 [Backups de log de transações](../backup-restore/transaction-log-backups-sql-server.md)   
  
