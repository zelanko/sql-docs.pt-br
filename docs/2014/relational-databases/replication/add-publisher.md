---
title: Caixa de diálogo ' Adicionar publicador '
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.addpublisher.f1
helpviewer_keywords:
- Add Publisher dialog box
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9f0401c06d79e7664ad4a06a2a92adcb52edfccb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068785"
---
# <a name="sql-server-replication-add-publisher-dialog-box"></a>Caixa de diálogo Replicação do SQL Server ' Adicionar publicador ' 
  A caixa de diálogo **Adicionar Publicador** permite a adição de um ou mais publicadores no painel esquerdo do Replication Monitor. Depois de adicionar um Publicador, selecioná-lo no painel esquerdo mostrará informações sobre o Publicador no painel à direita.  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Clique para selecionar um tipo de Publicador a ser adicionado que inicia a caixa de diálogo **Conectar ao Servidor** . As opções são:  
  
-   **Adicionar SQL Server Publicador...**  
  
     Conectar-se ao Editor usando a caixa de diálogo **Conectar ao Servidor** .  
  
-   **Adicionar Publicador Oracle...**  
  
     Conecte-se ao Distribuidor da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com Editor Oracle usando a caixa de diálogo **Conectar ao Servidor**.  
  
-   **Especifique um distribuidor e adicione seus Publicadores...**  
  
     Conecte-se ao Distribuidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associado a um ou mais Publicadores usando a caixa de diálogo **Conectar ao Servidor** .  
  
 Depois de se conectar com êxito ao Publicador ou ao Distribuidor, o nome de cada publicador e seu distribuidor serão exibidos na grade, na parte superior da caixa de diálogo.  
  
> [!NOTE]  
>  O Distribuidor e o Publicador geralmente são executados na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas o Distribuidor pode ser executado em outra instância (essa configuração é referenciada como Distribuidor remoto).  
  
 **Remover**  
 Selecione um Publicador na grade, na parte superior da caixa de diálogo, e clique em **Remover** para remover o Publicador da lista de Publicadores a serem selecionados.  
  
> [!NOTE]  
>  Esse botão não pode ser usado para remover um Publicador já exibido no Replication Monitor. Para remover um Publicador já exibido, clique no Publicador no painel esquerdo do Replication Monitor, e clique em **Remover**.  
  
 **Conectar automaticamente quando o Replication Monitor for iniciado**  
 Selecione para permitir que o Replication Monitor faça conexão automática com o Distribuidor e recupere informações de status para o Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa caixa de seleção estiver desmarcada, você terá de fazer a conexão manualmente após iniciar o Replication Monitor: clique com o botão direito no Publicador no painel esquerdo do Replication Monitor, e clique em **Conectar**.  
  
 **Atualizar automaticamente o status deste Publicador e de suas publicações**  
 Selecione para permitir que o Replication Monitor atualize automaticamente o status do Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa opção for selecionada, o Replication Monitor pesquisará no Distribuidor informações de status sobre o Publicador e suas publicações. O intervalo da sondagem é definido pela opção **Taxa de Atualização** . Para obter mais informações sobre a atualização no Replication Monitor, consulte [Cache, atualização e desempenho do Replication Monitor](monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Taxa de atualização**  
 Insira um valor (em segundos) para especificar a frequência de sondagem do Replication Monitor no Distribuidor, por status. Valores mais baixos resultam em sondagens mais frequentes, que podem afetar o desempenho no Distribuidor se você estiver monitorando um grande número de Publicadores. É recomendado que você teste seu sistema para determinar um valor apropriado. A configuração da **Taxa de Atualização** será também usada se você selecionar **Atualização Automática** em qualquer uma das janelas de detalhes no Replication Monitor.  
  
 **Mostrar este Publicador no grupo a seguir**  
 Selecione um grupo de Publicadores na lista. O Publicador é exibido nesse grupo no painel esquerdo. Grupos fornecem uma forma de organizar Publicadores e não causam nenhum efeito em funções de replicação. Se nenhum grupo estiver definido ou você quer criar um novo, clique em **Novo Grupo**.  
  
 **Novo grupo**  
 Clique para criar um novo grupo de Publicadores. Um grupo de Publicadores é um modo conveniente de organizar Publicadores no Replication Monitor. Grupos não afetam a replicação de dados ou a relação entre servidores em uma topologia de replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Monitorando a Replicação](monitoring-replication.md)  
  
  
