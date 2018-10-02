---
title: Definir limites e avisos no Replication Monitor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- Merge Agent, thresholds and warnings
- Distribution Agent, thresholds and warnings
- thresholds [SQL Server replication]
- Replication Monitor, thresholds and warnings
- monitoring performance [SQL Server replication], thresholds and warnings
ms.assetid: 3a409c2c-b77e-4001-b81a-1dcd918618ec
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e20f280df7054596f357c4864ef95177ca3e9cf5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749577"
---
# <a name="set-thresholds-and-warnings-in-replication-monitor"></a>Definir os limites e avisos no Replication Monitor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor exibe informações de status para publicações e assinaturas. Por padrão, o Replication Monitor só exibe avisos para assinaturas não inicializadas, mas você pode habilitar os avisos para outras condições. Recomendamos habilitar os avisos para a sua topologia, para que esteja informado sobre o status e o desempenho de maneira oportuna.  
  
 Ao habilitar um aviso, você especifica um limite. Quando o limite é atingido ou excedido, um aviso é exibido (a menos que um problema com prioridade superior deva ser exibido). Além de exibir de um aviso no Replication Monitor, atingir um limite também pode disparar um alerta. Você pode habilitar avisos para as seguintes condições:  
  
-   Expiração iminente de assinatura  
  
     Isso se aplica a todos os tipos de replicação. Se o limite especificado for atingido ou excedido, o status da assinatura será exibido como **Expirando em breve/Expirado**.  
  
-   Exceder a latência especificada (o período decorrido entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante).  
  
     Isso se aplica à replicação transacional. Se o limite especificado for atingido ou excedido, o status da assinatura será exibido como **Desempenho crítico**.  
  
-   Excedendo o tempo de sincronização especificado.  
  
     Isso se aplica à replicação de mesclagem. Se o limite especificado for atingido ou excedido, o status será exibido como **Mesclagem de execução longa**. Você pode especificar limites diferentes para conexões discadas e Rede local (LAN).  
  
-   Falha no processamento do número especificado de linhas em um determinado período.  
  
     Isso se aplica à replicação de mesclagem. Se o limite especificado for atingido ou excedido, o status será exibido como **Desempenho crítico**. Você pode especificar limites diferentes para conexões discadas e LAN.  
  
 Para obter mais informações sobre os avisos **Desempenho crítico** e **Mesclagem de execução longa**, consulte [Monitorar o desempenho com o Replication Monitor](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Neste tópico**  
  
-   [Definir limites e avisos para uma publicação transacional](#Transactional)  
  
-   [Definir limites e avisos para uma publicação de mesclagem](#Merge)  
  
-   [Definir limites e avisos para uma publicação de instantâneo](#Snapshot)  
  
##  <a name="Transactional"></a> Para definir limites e avisos para uma publicação transacional  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique na guia **Avisos** . Para exibir mais informações sobre as opções nessa guia, clique em **Ajuda** na barra de menus.  
  
3.  Habilite um aviso selecionando a caixa de seleção apropriada: **Avise se uma assinatura for expirar dentro do limite** ou **Avise se a latência exceder o limite**.  
  
4.  Defina um limite para os avisos na coluna **Limite** . Por exemplo, ao selecionar **Avise se a latência exceder o limite** na etapa 3, é possível selecionar uma latência de **60 segundos** na coluna **Limite** .  
  
5.  Clique em **Salvar Alterações**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Para configurar um alerta para um limite  
  
1.  Clique em **Configurar Alertas**.  
  
2.  Na caixa de diálogo **Configurar Alertas de Replicação** , selecione um alerta e então clique em **Configurar**.  
  
     Essa caixa de diálogo exibe os alertas para todos os tipos de publicação, inclusive alertas que não estão relacionados com o monitoramento de limites. Para obter mais informações, consulte [Usar alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
3.  Defina opções na caixa de diálogo **Propriedades do alerta \<AlertName>**:  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique em **Fechar**.  
  
##  <a name="Merge"></a> Definir limites e avisos para uma publicação de mesclagem  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique na guia **Avisos** . Para exibir mais informações sobre as opções nessa guia, clique em **Ajuda** na barra de menu.  
  
3.  Habilite um aviso selecionando a caixa de seleção apropriada:  
  
    -   **Avise se uma assinatura for expirar dentro do limite**  
  
    -   **Avisar se o tamanho de mesclagem da conexão discada exceder o limite**  
  
    -   **Avisar se o tamanho de mesclagem das conexões da LAN exceder o limite**  
  
    -   **Avisar se as filas mescladas por segundo para conexões de LAN forem menores que o limite**  
  
    -   **Avisar se as filas mescladas por segundo para conexões discadas forem menores que o limite**  
  
4.  Defina limites para os avisos na coluna **Limite** . Por exemplo, caso tenha selecionado **Avisar se o tamanho de mesclagem para conexões discadas exceder o limite** na etapa 3, você poderá selecionar um intervalo de **10 minutos** na coluna **Limite** .  
  
5.  Clique em **Salvar Alterações**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Para configurar um alerta para um limite  
  
1.  Clique em **Configurar Alertas**.  
  
2.  Na caixa de diálogo **Configurar Alertas de Replicação** , selecione um alerta e então clique em **Configurar**.  
  
     Essa caixa de diálogo exibe os alertas para todos os tipos de publicação, inclusive alertas que não estão relacionados com o monitoramento de limites.  
  
3.  Defina opções na caixa de diálogo **Propriedades do alerta \<AlertName>**:  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique em **Fechar**.  
  
##  <a name="Snapshot"></a> Definir limites e avisos para uma publicação de instantâneo  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique na guia **Avisos** . Para exibir mais informações sobre as opções nessa guia, clique em **Ajuda** no menu superior.  
  
3.  Ative uma aviso selecionando a caixa de seleção **Avisar se uma assinatura for expirar dentro do limite**.  
  
4.  Defina um limite para o aviso na coluna **Limite** . Por exemplo, você pode selecionar um valor de **70%** na coluna **Limite** .  
  
5.  Clique em **Salvar Alterações**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Para configurar um alerta para um limite  
  
1.  Clique em **Configurar Alertas**.  
  
2.  Na caixa de diálogo **Configurar Alertas de Replicação** , selecione um alerta e então clique em **Configurar**.  
  
     Essa caixa de diálogo exibe os alertas para todos os tipos de publicação, inclusive alertas que não estão relacionados com o monitoramento de limites. Para obter mais informações, consulte [Usar alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
3.  Defina opções na caixa de diálogo **Propriedades do alerta \<AlertName>**:  
  
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.  
  
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.  
  
    -   Na página **Opções** , personalize o texto da resposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique em **Fechar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
