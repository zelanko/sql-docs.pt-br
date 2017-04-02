---
title: "Informa&#231;&#245;es da Publica&#231;&#227;o, Avisos (publica&#231;&#227;o transacional, SQL Server 2005 e vers&#245;es posteriores) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.warningsandagents.tran.f1"
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Informa&#231;&#245;es da Publica&#231;&#227;o, Avisos (publica&#231;&#227;o transacional, SQL Server 2005 e vers&#245;es posteriores)
  A guia **Avisos** está disponível para Distribuidores que estão executando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. A guia **Avisos** permite executar as seguintes tarefas para a publicação selecionada:  
  
-   Ativar advertências a serem exibidas no Replication Monitor.  
  
-   Especificar limites associados a avisos.  
  
-   Definir alertas associados a avisos.  
  
## Avisos, limites e alertas  
 Por padrão, o Replication Monitor exibe avisos para assinaturas não inicializadas: um status **Assinatura não inicializada** é exibido como um aviso na coluna **Status** de páginas que incluem informações de assinatura. Para publicações transacionais, você pode especificar se essas condições adicionais resultarão em avisos:  
  
-   Expiração de assinatura iminente.  
  
     Isso corresponde à opção **Avisar se uma assinatura for expirar dentro do limite**. Se o limite especificado for atingido ou excedido, o status da assinatura será exibido como **expirando em breve/expirado** (a menos que um problema com uma prioridade mais alta precise ser exibido).  
  
-   Excedendo a latência especificada. É o período de tempo que decorre entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante.  
  
     Isso corresponde à opção **Avisar se a latência excede o limite**. Se o limite especificado for atingido ou excedido, o status da assinatura será exibido como **desempenho crítico** (a menos que um problema com uma prioridade mais alta precise ser exibido). O limite também é usado para fornecer uma avaliação de desempenho, que é exibida na **desempenho** coluna das páginas que incluem informações de assinatura. A classificação de desempenho é um dos seguintes valores:  
  
    -   Excelente  
  
    -   Bom  
  
    -   Razoável  
  
    -   Fraco  
  
    -   Crítico  
  
 Quando você habilita um aviso, também define um limite. Por exemplo, se você habilitar o aviso **Avisar se a latência excede o limite**, selecione o período de tempo permitido entre uma transação confirmada no Editor e a transação seja confirmada no assinante.  
  
 Além de exibir de um aviso no Replication Monitor, atingir um limite também pode disparar um alerta. Os alertas são definidos clicando em **Configurar Alertas** e fornecendo informações na caixa de diálogo **Configurar Alertas de Replicação** .  
  
## Opções  
 **Ativado**  
 Selecione para habilitar um aviso e especificar um limite.  
  
 **Aviso**  
 Uma descrição do aviso associada a um limite.  
  
 **Limite**  
 Especifique um valor para o limite.  
  
 **Configurar Alertas**  
 Selecione uma linha no **avisos** grade e clique em **Configurar alertas** para iniciar o **Configurar alertas de replicação** caixa de diálogo. A caixa de diálogo permite definir um alerta associado ao limite selecionado e ao aviso.  
  
 **Descartar Alterações**  
 Clique para descartar qualquer alteração em avisos e limites.  
  
> [!NOTE]  
>  Clicar em **Descartar alterações** não afeta os alertas definidas no **Configurar alertas de replicação** caixa de diálogo.  
  
 **Salvar alterações**  
 Clique para salvar qualquer alteração em avisos e limites.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para uma publicação e 40; Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Monitorar o desempenho com o Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Set Thresholds and Warnings in Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  