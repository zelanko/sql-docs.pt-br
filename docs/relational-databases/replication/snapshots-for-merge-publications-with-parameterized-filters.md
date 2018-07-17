---
title: Instantâneos para publicações de mesclagem com filtros com parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
- merge replication [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9bccb510d97b54a201db8ecebc9ce870a523ad72
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37360018"
---
# <a name="snapshots-for-merge-publications-with-parameterized-filters"></a>Instantâneos para publicações de mesclagem com filtros com parâmetros
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando são usados filtros de linha com parâmetros em publicações de mesclagem, a replicação inicializa cada assinatura com um instantâneo de duas partes. Em primeiro lugar, um instantâneo do esquema é criado contendo todos os objetos exigidos pela replicação e o esquema dos objetos publicados, mas não os dados. Em seguida, cada assinatura é inicializada com um instantâneo que inclui os objetos e o esquema do instantâneo do esquema e os dados que pertencem à partição de assinatura. Se mais de uma assinatura receber uma dada partição (ou seja, receber o mesmo esquema e dados), o instantâneo para aquela partição é criado apenas uma vez; várias assinaturas são inicializadas do mesmo instantâneo. Para obter mais informações sobre filtros de linha com parâmetros, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 É possível criar instantâneos para publicações com filtros com parâmetros usando-se uma das três maneiras:  
  
-   Gere previamente instantâneos para cada partição. Usar essa opção lhe permite controlar quando os instantâneos são gerados.  
  
     É possível também optar para que os instantâneos sejam atualizados em uma agenda. Novos Assinantes que assinem uma partição para a qual um instantâneo foi criado receberão um instantâneo atualizado.  
  
-   Permita que os Assinantes solicitem geração e aplicação de instantâneos na primeira vez que eles sincronizarem. O uso dessa opção permite que novos Assinantes sincronizem sem a exigência de intervenção de um administrador ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar sendo executado no Publicador para permitir que o instantâneo seja gerado).  
  
    > [!NOTE]  
    >  Se a filtragem para um ou mais artigos da publicação gerar partições não sobrepostas, exclusivas de cada assinatura, os metadados serão limpos sempre que o Agente de Mesclagem for executado. Isso significa que o instantâneo particionado irá expirar mais rapidamente. Ao usar essa opção, considere permitir que os Assinantes possam iniciar a geração e a entrega do instantâneo. Para obter mais informações sobre opções de filtragem, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Gere manualmente um instantâneo para cada Assinante com o Agente de Instantâneo. O Assinante deve então fornecer o local do instantâneo para o Agente de Mesclagem, para que possa recuperar e aplicar o instantâneo correto.  
  
    > [!NOTE]  
    >  Essa opção tem suporte para compatibilidade com versões anteriores e não permite compartilhamento de instantâneo de FTP.  
  
 A abordagem mais flexível é usar uma combinação de opções de instantâneo gerado previamente e solicitado por Assinante: instantâneos são gerados previamente e atualizados com base em uma agenda (em geral durante momento que não é de pico), mas um Assinante pode gerar seu próprio instantâneo se uma assinatura que exige uma nova partição for criada.  
  
 Considere [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], que têm uma mão-de-obra móvel que entrega inventário para lojas individuais. Cada vendedor recebe uma assinatura com base em seu logon que recupera os dados para as lojas que eles atendem. O administrador opta por gerar instantâneos previamente e atualizá-los todos os domingos. Ocasionalmente, um novo usuário é adicionado ao sistema e precisa de dados para uma partição que não tem um instantâneo disponível. O administrador também opta por permitir instantâneos inicializados pelo Assinante a fim de evitar a situação em que um Assinante não possa fazer assinatura para a publicação por que o instantâneo ainda não está disponível. Quando o novo Assinante faz a conexão pela primeira vez, o instantâneo é gerado para a partição especificada e aplicado no Assinante ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar sendo executado no Publicador para permitir que o instantâneo seja gerado).  
  
 Para criar um instantâneo para uma publicação com filtros com parâmetros, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="security-settings-for-the-snapshot-agent"></a>Configurações de segurança para o Agente de Instantâneo  
 O Agente de Instantâneo cria instantâneos para cada partição. Para instantâneos gerados previamente e instantâneos solicitados por um Assinante, o agente é executado e faz conexões sob as credenciais que foram especificadas quando o trabalho do snapshot agent para a publicação foi criado (o trabalho é criado pelo Assistente para Nova Publicação ou **sp_addpublication_snapshot**). Para alterar as credenciais, use **sp_changedynamicsnapshot_job**. Para obter mais informações, consulte [sp_changedynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
