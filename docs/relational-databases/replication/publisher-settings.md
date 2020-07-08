---
title: "'Configurações do Editor' (SSMS) | Microsoft Docs"
descripton: Describes the 'Publisher Settings' dialog box found in Replication Monitor within SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publishersettings.f1
helpviewer_keywords:
- Publisher Settings dialog box
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: a6232fc78b4c9b1d68a9cc96e6fed69138e5075f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85678484"
---
# <a name="sql-server-replication-publisher-settings-dialog-box"></a>Caixa de diálogo 'Configurações do Editor' de Replicação do SQL Server
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  A caixa de diálogo **Configurações do Publicador** permite alterar configurações para Publicadores adicionados ao painel esquerdo no Replication Monitor.  
  
## <a name="options"></a>Opções  
 **Conexão do Publicador**  
 Clique para iniciar a caixa de diálogo **Conectar ao Servidor** que permite que você visualize e altere as credenciais e propriedades de conexão que o Replication Monitor usa para se conectar a um Publicador.  
  
 **Conexão do Distribuidor**  
 Exibido somente se o Publicador usar um Distribuidor remoto. Clique para iniciar a caixa de diálogo **Conectar ao Servidor** que permite que você visualize e altere as credenciais e propriedades de conexão que o Replication Monitor usa para se conectar a um Distribuidor remoto.  
  
 **Conectar automaticamente quando o Replication Monitor for iniciado**  
 Selecione para permitir que o Replication Monitor faça conexão automática com o Distribuidor e recupere informações de status para o Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa caixa de seleção estiver desmarcada, você terá de fazer a conexão manualmente após iniciar o Replication Monitor: clique com o botão direito no Publicador no painel esquerdo do Replication Monitor, e clique em **Conectar**.  
  
 **Atualizar automaticamente o status deste Publicador e de suas publicações**  
 Selecione para permitir que o Replication Monitor atualize automaticamente o status do Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa opção for selecionada, o Replication Monitor pesquisará no Distribuidor informações de status sobre o Publicador e suas publicações. O intervalo da sondagem é definido pela opção **Taxa de Atualização** . Para obter mais informações sobre a atualização no Replication Monitor, consulte [Cache, atualização e desempenho do Replication Monitor](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Taxa de atualização**  
 Insira um valor (em segundos) para especificar a frequência de sondagem do Replication Monitor no Distribuidor, por status. Valores mais baixos resultam em sondagens mais frequentes, que podem afetar o desempenho no Distribuidor se você estiver monitorando um grande número de Publicadores. É recomendado que você teste seu sistema para determinar um valor apropriado. A configuração da **Taxa de Atualização** será também usada se você selecionar **Atualização Automática** em qualquer uma das janelas de detalhes no Replication Monitor.  
  
 **Mostrar este Publicador no grupo a seguir**  
 Selecione um grupo de Publicadores na lista. O Publicador é exibido nesse grupo no painel esquerdo. Grupos fornecem uma forma de organizar Publicadores e não causam nenhum efeito em funções de replicação.  
  
 **Novo grupo**  
 Clique para criar um novo grupo de Publicadores. Um grupo de Publicadores é um modo conveniente de organizar Publicadores no Replication Monitor. Grupos não afetam a replicação de dados ou a relação entre servidores em uma topologia de replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
