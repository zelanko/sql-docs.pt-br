---
title: Linha do tempo de backup | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.SWB.POINTINTIMERESTORE.F1
- sql13.swb.backuptimeline.f1
helpviewer_keywords:
- Backup Timeline
ms.assetid: ae3565f2-ddb2-4469-a992-7531d4f9ebb8
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5281d07e90a8163ec02392c7f52f04d1aa949959
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="backup-timeline"></a>Linha do tempo de backup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a caixa de diálogo **Linha do Tempo de Backup** para localizar e especificar backups para restaurar um banco de dados em um ponto específico. Acesse a caixa de diálogo **Linha do Tempo de Backup** clicando em **Linha do Tempo** no painel **Restaurar Banco de dados (Página Geral)** . Esta caixa de diálogo permite exibir uma linha do tempo das operações de restauração executadas no banco de dados.  
  
 O orientador de recuperação de banco de dados garante que apenas os backups necessários para restaurar até o ponto especificado sejam selecionados. Esses backups selecionados compõem o plano de restauração recomendado para a operação de restauração. Você deve usar apenas os backups selecionados. Para obter informações sobre o Orientador de Recuperação de Banco de Dados, confira [Visão geral da restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
## <a name="restore-to"></a>Restaurar para  
 **Último backup feito** está selecionado por padrão. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] selecionará os backups apropriados para restaurar o banco de dados, e restaurará o banco de dados para o ponto do último backup. Clique em **Data e hora específicas** para definir manualmente a data e a hora (selecionando um ponto específico no tempo).  
  
 **Data e hora específicas** permite que você pare a restauração a uma data e hora especificadas por você. A linha de tempo mostra uma representação das operações de backup executadas 24 horas ma seleção de data e hora.  
  
 **Data**  
 Insira ou selecione uma data na lista suspensa.  
  
 **Time**  
 Insira ou selecione uma data para designar o ponto específico no tempo para a restauração parar.  
  
 **Intervalo na linha de tempo**  
 Exibe as opções para os tipos de intervalo que podem ser exibidos na linha do tempo.  
  
## <a name="timeline-and-legend"></a>Linha de tempo e legenda  
 Use a barra de rolagem abaixo da linha do tempo para mover o cursor para a frente e para trás ao longo da linha do tempo. Clique em um backup para mover a barra de rolagem ao término desse backup. Mova o mouse sobre um marcador para exibir uma Dica de tela que fornece informações sobre o conjunto de backup selecionado. As informações de backup são mostradas na linha do tempo pelos marcadores a seguir.  
  
 Triângulo maior  
 Representa os backups completos executados no banco de dados, denotando o ponto específico no tempo em que cada backup completo foi executado.  
  
 Triângulo menor  
 Representa os backups diferenciais executados no banco de dados, denotando o ponto específico no tempo em que cada backup diferencial foi executado.  
  
 Áreas sombreadas verdes  
 Representa a cobertura de backup do log de transações.  
  
 Linha vermelha  
 Pode ser posicionada somente ao longo da linha do tempo onde a restauração é possível. A movimentação da linha vermelha ao longo da linha do tempo ajusta a data e a hora exibidas nas caixas **Data** e **Hora** .  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurar banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
  
