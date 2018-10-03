---
title: Informações da publicação – avisos – publicação de instantâneo – SQL Server 2005+ | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.warningsandagents.snapshot.f1
ms.assetid: 7aa2eb52-b6b7-4dd3-8483-8ef00d9f0435
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 263f1b3a76a30c1ab220234b32dd55af1ab6cfac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674704"
---
# <a name="publication-information-warnings-snapshot-publication-sql-server-2005-and-later"></a>Informações da Publicação, Avisos (publicação de instantâneo, SQL Server 2005 e versões posteriores)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A guia **Avisos** está disponível para Distribuidores que estão executando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. A guia **Avisos** permite executar as seguintes tarefas para a publicação selecionada:  
  
-   Habilitar avisos.  
  
-   Especificar limites associados a avisos.  
  
-   Definir alertas associados a avisos.  
  
## <a name="warnings-thresholds-and-alerts"></a>Avisos, limites e alertas  
 Por padrão, o Replication Monitor exibe avisos para assinaturas não inicializadas: um status **Assinatura não inicializada** é exibido como um aviso na coluna **Status** de páginas que incluem informações de assinatura. Para publicações de instantâneo, você também pode especificar que a expiração iminente da assinatura resulte em um aviso, com a definição da opção **Avisar se uma assinatura for expirar dentro do limite**. Se o limite especificado for alcançado ou ultrapassado, o status da assinatura será exibido como **Expirando em breve/Expirado** (a menos que um problema com prioridade mais alta precise ser exibido).  
  
 Além de exibir de um aviso no Replication Monitor, atingir um limite também pode disparar um alerta. Os alertas são definidos clicando em **Configurar Alertas** e fornecendo informações na caixa de diálogo **Configurar Alertas de Replicação** .  
  
## <a name="options"></a>Opções  
 **Ativado**  
 Selecione para habilitar um aviso e especificar um limite.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para uma publicação &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
