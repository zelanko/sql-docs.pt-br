---
title: Informações da publicação, avisos (publicação de mesclagem, SQL Server 2005 e versões posterior) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.warningsandagents.merge.f1
ms.assetid: 9bef3565-5f13-42ac-8723-ebe55b0c11e6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f849394a4a77091f92ee66857b4d5263875fdea3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63021682"
---
# <a name="publication-information-warnings-merge-publication-sql-server-2005-and-later"></a>Informações da Publicação, Avisos (publicação de mesclagem, SQL Server 2005 e versões posteriores)
  A guia **Avisos** está disponível para Distribuidores que estão executando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. A guia **Avisos** permite executar as seguintes tarefas para a publicação selecionada:  
  
-   Habilitar avisos.  
  
-   Especificar limites associados a avisos.  
  
-   Definir alertas associados a avisos.  
  
## <a name="warnings-thresholds-and-alerts"></a>Avisos, limites e alertas  
 Por padrão, o Replication Monitor exibe avisos para assinaturas não inicializadas: um status **Assinatura não inicializada** é exibido como um aviso na coluna **Status** de páginas que incluem informações de assinatura. Para publicações de mesclagem, você pode especificar se essas condições adicionais resultarão em avisos:  
  
-   Expiração de assinatura iminente.  
  
     Isso corresponde à opção **Avisar se uma assinatura for expirar dentro do limite**. Se o limite especificado for alcançado ou ultrapassado, o status da assinatura será exibido como **Expirando em breve/Expirado** (a menos que um problema com prioridade mais alta precise ser exibido).  
  
-   Excedendo o tempo de sincronização especificado.  
  
     Isso corresponde às opções **Avisar se o tamanho de mesclagem da conexão discada exceder o limite** e **Avisar se o tamanho de mesclagem das conexões da LAN exceder o limite**. Esses dois limites podem ser definidos, mas só um é usado durante uma determinada sincronização. O Merge Agent aplica o limite apropriado com base no tipo de conexão.  
  
     Se o limite especificado for alcançado ou ultrapassado, o status da assinatura será exibido como **Mesclagem de execução longa** (a menos que um problema com prioridade mais alta precise ser exibido).  
  
-   Falha no processamento do número especificado de linhas em um determinado período.  
  
     Corresponde às opções **Avisar se as filas mescladas por segundo para conexões discadas forem menores que o limite** e **Avisar se o tamanho de mesclagem das conexões da LAN exceder o limite**. Esses dois limites podem ser definidos, mas só um é usado durante uma determinada sincronização. O Merge Agent aplica o limite apropriado com base no tipo de conexão.  
  
     Se o limite especificado for alcançado ou ultrapassado, o status da assinatura será exibido como **Desempenho crítico** (a menos que um problema com prioridade mais alta precise ser exibido).  
  
 Quando você habilita um aviso, também define um limite. Por exemplo, se você habilitar o aviso **Avisar se o tamanho de mesclagem das conexões da LAN exceder o limite**, defina o período de tempo máximo permitido para uma sincronização de mesclagem.  
  
 Além de exibir de um aviso no Replication Monitor, atingir um limite também pode disparar um alerta. Os alertas são definidos clicando em **Configurar Alertas** e fornecendo informações na caixa de diálogo **Configurar Alertas de Replicação** .  
  
## <a name="options"></a>Opções  
 **Ativado**  
 Selecione para habilitar um aviso e especificar um limite.  
  
 **Alerta**  
 Selecione para habilitar a configurações de alerta para um determinado aviso de replicação.  
  
 **Aviso**  
 Uma descrição do aviso associada a um limite.  
  
 **Limite**  
 Especifique um valor para o limite.  
  
 **Configurar Alertas**  
 Selecione uma linha na grade **Avisos** e clique em **Configurar Alertas** para iniciar a caixa de diálogo **Configurar Alertas de Replicação** . A caixa de diálogo permite definir um alerta associado ao limite selecionado e ao aviso.  
  
 **Descartar Alterações**  
 Clique para descartar qualquer alteração em avisos e limites.  
  
> [!NOTE]  
>  Clicar em **Descartar Alterações** não afeta alertas definidos na caixa de diálogo **Configurar Alertas de Replicação** .  
  
 **Salvar alterações**  
 Clique para salvar qualquer alteração em avisos e limites.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitorar o desempenho com o Replication Monitor](monitor/monitor-performance-with-replication-monitor.md)   
 [Monitorando a Replicação](monitoring-replication.md)   
 [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
