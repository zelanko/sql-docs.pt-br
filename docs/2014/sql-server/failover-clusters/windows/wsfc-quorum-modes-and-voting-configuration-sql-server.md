---
title: Configuração de modos de quorum WSFC e votação (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: ca0d59ef-25f0-4047-9130-e2282d058283
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7febab9f8ecf6cae4df08f110a16c0bdc512a948
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62711431"
---
# <a name="wsfc-quorum-modes-and-voting-configuration-sql-server"></a>Configuração de modos de quorum WSFC e votação (SQL Server)
  Tanto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] quanto as instâncias de cluster de failover (FCI) AlwaysOn utilizam o Windows Server Failover Clustering (WSFC) como tecnologia de plataforma.  O WSFC usa uma abordagem baseada em quorum para monitorar integridade de cluster geral e maximizar a tolerância a falhas no nível do nó. Um entendimento fundamental dos modos de quorum do WSFC e a configuração de votação de nó são muito importantes para o design, a operação e a resolução de problemas da sua solução de alta disponibilidade e recuperação de desastre AlwaysOn.  
  
 **Neste tópico:**  
  
-   [Detecção de integridade de cluster por quorum](#ClusterHealthDetectionbyQuorum)  
  
-   [Modos de quorum](#QuorumModes)  
  
-   [Nós de votação e não votação](#VotingandNonVotingNodes)  
  
-   [Ajustes indicados para votação de quorum](#RecommendedAdjustmentstoQuorumVoting)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="cluster-health-detection-by-quorum"></a><a name="ClusterHealthDetectionbyQuorum"></a>Detecção de integridade de cluster por quorum  
 Cada nó em um cluster do WSFC participa da comunicação de pulsação periódica para compartilhar o status de integridade do nó com os outros nós. Nós sem resposta são considerados como em estado com falha.  
  
 Um conjunto de nós de *quorum* é uma maioria dos nós de votação e testemunhas no cluster WSFC. A integridade geral e o status de um cluster WSFC são determinados por um *voto de quorum*periódico.  A presença de um quorum significa que o cluster está íntegro e é capaz de fornecer tolerância a falhas no nível de nó.  
  
 A ausência de um quorum indica que o cluster não está íntegro.  A integridade do cluster WSFC geral deve ser mantida para assegurar que os nós secundários de integridade estejam disponíveis para nós primários para failover.  Se o voto de quorum falhar, o cluster WSFC será definido offline por precaução.  Isso também fará com que todas as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] registradas com o cluster sejam interrompidas.  
  
> [!IMPORTANT]  
>  Se um cluster WSFC for definido offline devido a uma falha de quorum, a intervenção manual será necessária para colocá-lo online novamente.  
>   
>  Para obter mais informações, veja: [Recuperação de desastres do WSFC por meio de quorum forçado &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)periódico.  
  
##  <a name="quorum-modes"></a><a name="QuorumModes"></a>Modos de quorum  
 Um *modo de quorum* é configurado no nível do cluster WSFC que dita a metodologia usada para votação de quorum.  O utilitário Gerenciador de Cluster de Failover recomendará um modo de quorum com base no número de nós no cluster.  
  
 Os seguintes modos de quorum podem ser usados para determinar o que constitui um quorum de votos:  
  
-   **Maioria de Nós.** Mais da metade dos nós de votação no cluster precisam votar afirmativamente para o cluster ser íntegro.  
  
-   **Maioria de compartilhamentos de nós e arquivos.** Semelhante ao modo de quorum Maioria de Nó, exceto pelo fato de um compartilhamento de arquivo remoto também ser configurado como uma testemunha de votação e a conectividade de qualquer nó com esse compartilhamento também ser contada como um voto afirmativo.  Mais da metade dos votos possíveis deve ser afirmativa para que o cluster seja íntegro.  
  
     Como uma prática recomendada, o compartilhamento de arquivo de testemunha não deve residir em nenhum nó no cluster e deve estar visível para todos os nós no cluster.  
  
-   **Maioria de nós e discos.** Semelhante ao modo de quorum Maioria de Nó, exceto pelo fato de um recurso de cluster de disco compartilhamento também ser designado como uma testemunha de votação e a conectividade de qualquer nó com esse disco compartilhado também ser contada como um voto afirmativo.  Mais da metade dos votos possíveis deve ser afirmativa para que o cluster seja íntegro.  
  
-   **Somente Disco.** Um recurso de cluster de disco compartilhamento é designado como uma testemunha e a conectividade por qualquer nó com esse disco compartilhado é contada como um voto afirmativo.  
  
> [!TIP]  
>  Ao usar uma configuração de armazenamento assimétrico para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], em geral, você deve usar o modo de quorum Maioria de Nós quando há um número ímpar de nós de votação ou o modo de quorum Maioria de Compartilhamentos de Nós e Arquivos quando há um número par de nós de votação.  
  
##  <a name="voting-and-non-voting-nodes"></a><a name="VotingandNonVotingNodes"></a>Nós de votação e não votantes  
 Por padrão, cada nó no cluster WSFC é incluso como membro do quorum de cluster; cada nó tem um único voto na determinação da integridade de cluster geral e cada nó tentará continuamente estabelecer um quorum.  A discussão de quorum até esse ponto qualificou cuidadosamente o conjunto de nós do cluster WSFC que votam na integridade do cluster como *nós de votação*.  
  
 Nenhum nó individual em um cluster WSFC pode determinar definitivamente se o cluster como um todo é íntegro ou não íntegro.  A qualquer momento, da perspectiva de cada nó, alguns dos outros nós podem aparecer offline ou talvez pareça que estão em processo de failover ou não respondentes devido a uma falha de comunicação de rede.  Uma função chave do voto de quorum é determinar se o estado aparente de cada nó no cluster WSFC é de fato o estado real desses nós.  
  
 Para todos os modelos de quorum, exceto 'Somente Disco', a efetividade de um voto de quorum depende das comunicações confiáveis entre todos os nós de votação no cluster. As comunicações de rede entre os nós na mesma sub-rede física devem ser consideradas confiáveis; o voto de quorum deve ser confiável.  
  
 No entanto, se um nó em outra sub-rede for visto como não respondente em um voto de quorum, mas na verdade estiver online e, de outra forma, íntegro, isso ocorre muito provavelmente devido a uma falha de comunicação de rede entre sub-redes.  Dependendo da topologia de cluster, do modo de quorum e da configuração da política de failover, essa falha de comunicação de rede pode criar efetivamente mais de um conjunto (ou subconjunto) de nós de votação.  
  
 Quando mais de um subconjunto de nós de votação consegue estabelecer um quorum próprio, ele é conhecido como *cenário de separação*.  Nesse cenário, os nós nos quorums separados podem se comportar de modo diferente e conflitante.  
  
> [!NOTE]  
>  O cenário de separação somente é possível quando um administrador de sistema executa manualmente uma operação de quorum forçado ou em circunstâncias muito raras, um failover forçado; subdividindo explicitamente o conjunto de nós de quorum.  
  
 Para simplificar sua configuração de quorum e aumentar o tempo de inativo, convém ajustar a configuração de *NodeWeight* de cada nó para que o voto do nó não seja contado para o quorum.  
  
> [!IMPORTANT]  
>  Para usar configurações de NodeWeight, é necessário aplicar o seguinte hotfix para todos os servidores no cluster WSFC:  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): há um hotfix disponível para permitir que você configure um nó de cluster que não tenha votos de quorum em [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e em [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
##  <a name="recommended-adjustments-to-quorum-voting"></a><a name="RecommendedAdjustmentstoQuorumVoting"></a>Ajustes recomendados para votação de quorum  
 Ao habilitar ou desabilitar o voto de um nó WSFC específico, siga estas diretrizes:  
  
-   **Nenhum voto, por padrão.** Assuma que cada nó não deve votar sem justificativa explícita.  
  
-   **Inclua todas as réplicas primárias.** Cada nó WSFC que hospeda uma réplica primária do grupo de disponibilidade ou é o proprietário preferencial de uma FCI deve ter um voto.  
  
-   **Inclua possíveis proprietários de failover automático.** Cada nó que pode hospedar uma réplica primária, como resultado de um failover de grupo de disponibilidade automático ou failover de FCI, deve ter um voto. Se houver apenas um grupo de disponibilidade no cluster WSFC e as réplicas de disponibilidade forem hospedadas apenas por instâncias autônomas, essa regra incluirá somente a réplica secundária que é o destino do failover automático.  
  
-   **Exclua nós de site secundários.** Em geral, não dê votos para nós WSFC que residem em um site de recuperação de desastre secundário.  Você não deseja que os nós no site secundário colaborem para uma decisão de colocar o cluster offline quando não houver nada errado com o site primário.  
  
-   **Números de votos ímpares.** Se necessário, adicione um compartilhamento de arquivo testemunha, um nó testemunha ou um disco testemunha ao cluster e ajuste o modo de quorum para prevenir possíveis empates no voto de quorum.  
  
-   **Reavalie as atribuições de voto após o failover.** Você não deseja o failover em uma configuração de cluster sem suporte para um quorum íntegro.  
  
> [!IMPORTANT]
>  Quando a configuração de voto de quorum do WSFC for validada, o Assistente para Grupo de Disponibilidade AlwaysOn exibirá um aviso se um das condições a seguir for verdadeira:  
> 
>  -   O nó do cluster que hospeda a réplica primária não tem um voto  
> -   Uma réplica secundária é configurada para failover automático e seu nó de cluster não tem um voto.  
> -   O[KB2494036](https://support.microsoft.com/kb/2494036) não está instalado em todos os nós de cluster que hospedam réplicas de disponibilidade. Esse patch é necessário para adicionar ou remover votos para nós de cluster em implantações multissite. No entanto, em implantações de site único, ele geralmente não é necessário, e você pode ignorar o aviso sem nenhum problema.  
> 
> [!TIP]
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] expõe várias DMVs (exibições de gerenciamento dinâmico) do sistema que podem ajudá-lo a gerenciar configurações relacionadas à configuração do cluster WSFC e à votação de quorum do nó.  
> 
>  Para obter mais informações, veja:  [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql), [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql), [sys.dm_os_cluster_nodes](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql), [sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Exibir configurações de NodeWeight de quorum do cluster](view-cluster-quorum-nodeweight-settings.md)  
  
-   [Definir configurações de NodeWeight de quorum do cluster](configure-cluster-quorum-nodeweight-settings.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Verificação da configuração do voto de quorum nos assistentes de Grupo de Disponibilidade AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/archive/2012/03/13/quorum-vote-configuration-check-in-alwayson-availability-group-wizards-andy-jing.aspx)  
  
-   [Tecnologias do Windows Server: clusters de failover](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [Guia passo a passo do cluster de failover: configurando o quorum em um cluster de failover](https://technet.microsoft.com/library/cc770620\(WS.10\).aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Recuperação de desastre do WSFC por meio de quorum forçado &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)   
 [WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
