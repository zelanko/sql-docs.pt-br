---
title: Linha do tempo de backup | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.POINTINTIMERESTORE.F1
- sql12.swb.backuptimeline.f1
helpviewer_keywords:
- Backup Timeline
ms.assetid: ae3565f2-ddb2-4469-a992-7531d4f9ebb8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 92cffa7c280aac559433a8fc7ad5a3223c9f6de2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060906"
---
# <a name="backup-timeline"></a>Linha do tempo de backup
  Use a caixa de diálogo **Linha do Tempo de Backup** para localizar e especificar backups para restaurar um banco de dados em um ponto específico. Acesse a caixa de diálogo **Linha do Tempo de Backup** clicando em **Linha do Tempo** no painel **Restaurar Banco de dados (Página Geral)** . Esta caixa de diálogo permite exibir uma linha do tempo das operações de restauração executadas no banco de dados.  
  
 O orientador de recuperação de banco de dados garante que apenas os backups necessários para restaurar até o ponto especificado sejam selecionados. Esses backups selecionados compõem o plano de restauração recomendado para a operação de restauração. Você deve usar apenas os backups selecionados. Para obter informações sobre o Orientador de Recuperação de Banco de Dados, confira [Visão geral da restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Restaurar banco de dados &#40;página Geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
