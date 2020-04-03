---
title: Perfil de dados e notificações no DQS
ms.date: 04/01/2020
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a778bb5b-8e35-4a7b-b04a-ae2b46dec21b
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 1e5c51996ba85b9645650f453a0e4ed18478ccf7
ms.sourcegitcommit: 52925f1928205af15dcaaf765346901e438ccc25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2020
ms.locfileid: "80607829"
---
# <a name="data-profiling-and-notifications-in-dqs"></a>Perfil de dados e notificações no DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  A criação do perfil de dados no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) é o processo de analisar os dados em uma fonte de dados existente e exibir estatísticas sobre os dados nas atividades do DQS. Isso fornece a você medições automatizadas da qualidade dos dados. A criação de perfil do DQS está integrada ao gerenciamento de conhecimento do DQS e aos projetos de qualidade de dados. é dinâmico e ajustável. A criação de perfil tem dois objetivos principais: primeiro, orientá-lo durante os processos de qualidade de dados e dar suporte às suas decisões e, segundo, avaliar a efetividade dos processos. A criação de perfil do DQS tem os seguintes benefícios:  
  
-   A criação de perfil fornece informações sobre a qualidade da sua fonte de dados e o ajuda a identificar problemas de qualidade de dados.  
  
-   A criação de perfil avalia a eficácia dos processos de qualidade de dados, orientando você na descoberta da base de dados de conhecimento, limpeza de dados, política de correspondência e trabalho de correspondência.  
  
-   A criação de perfil apresenta as informações mais relevantes no momento mais relevante.  
  
-   O processo de criação de perfil gera notificações que enfatizam estatísticas ou eventos importantes que podem merecer ação. Em muitos casos, as notificações do DQS indicarão uma condição e recomendarão a ação que você deve adotar para resolver essa condição.  
  
 A criação de perfil permite que você use o Data Quality Services não só para a descoberta da base de dados de conhecimento, limpeza e correspondência, como também como uma ferramenta de análise. Talvez você queira criar uma base de dados de conhecimento para análise e executar a descoberta da base de dados de conhecimento usando essa base para determinar, com base nas estatísticas de criação de perfil, se a base de dados de conhecimento atende suas necessidades de descoberta, limpeza e correspondência.  
  
##  <a name="how-profiling-works"></a><a name="How"></a>Como funciona o perfil  
 O perfil não mede a qualidade da base de conhecimento. Ela mede a qualidade dos dados de origem. O perfil fornece estatísticas que indicam o efeito da operação específica que você está fazendo no gerenciamento do conhecimento ou em um projeto de qualidade de dados sobre seus dados de origem. O perfil está sempre no contexto da atividade específica que você está fazendo. Você pode clicar na guia de criação de perfil em uma tela para exibir dados de criação de perfil sem deixar o estágio da atividade que você está fazendo. A tabela de criação de perfil é preenchida em tempo real à medida que o processo é realizado, permitindo que você avalie as tarefas de qualidade de dados enquanto as está fazendo. É possível determinar se os dados de origem ficam melhores após a limpeza ou desduplicação e o quanto melhoram.  
  
 Todos os números de perfil referem-se ao número de aparições de um valor, e em muitos casos referem-se ao percentual do total, com exceção das métricas de exclusividade. As métricas de exclusividade se referem ao número absoluto de valores, independentemente do número de vezes em que esses valores aparecem.  
  
 A criação de perfil faz parte da solução voltada para conhecimentos do DQS. Ela fornece informações sobre uma base de dados de conhecimento, correspondência ou processo de limpeza de dados com base no mapeamento entre os campos da fonte de dados e os domínios da base de dados de conhecimento. Você só faz o perfil após o mapeamento ser concluído; nenhum perfil é feito durante a fase de mapeamento de qualquer atividade. A criação de perfil sempre está associada a uma atividade. O processo de criação de perfil é feito sobre os dados que são mapeados para domínios, não sobre os dados nos domínios. Está integrado nas seguintes etapas das atividades:  
  
-   As etapas **Descobrir** e **Gerenciar valores de domínio** da atividade Descoberta da base de dados de conhecimento  
  
-   As etapas **Limpar** e **Gerenciar e exibir resultados** da atividade Limpeza  
  
-   As etapas **Política de correspondência** e **Resultados correspondentes** da atividade Política de correspondência  
  
-   As etapas **Correspondência** e **Exportar** da atividade Correspondência  
  
 O DQS não fornece estatísticas de criação de perfil para a atividade de Gerenciamento de Domínios.  
  
##  <a name="profiling-data-by-activity"></a><a name="Activity"></a>Perfilando dados por atividade  
 A criação de perfil do DQS usa dimensões de qualidade de dados padrão para representar a qualidade dos dados: integridade (a extensão até a qual os dados estão presentes), precisão (a extensão até a qual os dados podem ser utilizados para seu uso pretendido) e exclusividade (a extensão até a qual valores diferentes representam entidades diferentes). Por padrão, valores NUUTOs e vazios são considerados ausentes, ou diminuir o percentual de completitude; no entanto, você também pode definir outros valores como nulo equivalente, nesse caso eles também serão considerados ausentes.  
  
 A criação de perfil fornece as estatísticas de que você precisa para avaliar seus processos, mas é necessário interpretá-las. Entenda o que a criação de perfil está informando a você examinando as estatísticas coluna por coluna.  
  
 As atividades do DQS têm conjuntos diferentes de estatísticas de criação de perfil, da seguinte forma:  
  
-   Somente a atividade Limpeza tem estatísticas de criação de perfil quanto à precisão (em percentual por domínio). A precisão é afetada pela validade, consistência, erros de sintaxe e regras de domínio.  
  
-   Somente a atividade Limpeza tem estatísticas de criação de perfil quanto a valores corretos, corrigidos e sugeridos na origem e valores corrigidos e sugeridos pelo domínio (ambos de número de percentual).  
  
-   As atividades Limpeza e Descoberta da Base de Dados de Conhecimento têm estatísticas de criação de perfil quanto à validade (Limpeza por registro, Descoberta da Base de Dados de Conhecimento por registro e domínio). As atividades de Correspondência e Política de Correspondência não têm estatísticas para validade.  
  
-   A atividade de limpeza não tem estatísticas de perfil para exclusividade. As atividades Descoberta da Base de Dados de Conhecimento, Política de Correspondência e Correspondência têm estatísticas de criação de perfil quanto à exclusividade no número e percentual de origem e por domínio.  
  
 Para obter mais informações sobre as estatísticas específicas de criação de perfil relacionadas a uma atividade, consulte as seções de criação de perfil nos seguintes artigos:  
  
-   [Executar a descoberta da base de dados de conhecimento](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [Limpar dados usando o conhecimento &#40;interno&#41; do DQS](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Criar uma política de correspondência](../data-quality-services/create-a-matching-policy.md)  
  
-   [Executar um projeto de correspondência](../data-quality-services/run-a-matching-project.md)  
  
##  <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>Perfilamento de dados no monitoramento de atividades  
 As informações de criação de perfil para as atividades de Descoberta de Conhecimento, Política de Correspondência, Correspondência e Limpeza estão disponíveis não apenas nas páginas de atividade no cliente Qualidade de Dados, mas também disponíveis no monitoramento de atividades. O monitoramento da atividade apresenta uma visão geral das atividades atuais e passadas. Além das propriedades e processos de atividades computacionais relacionados, você pode exibir as informações de criação de perfil geradas para cada atividade em um local. Selecione uma atividade na tabela de atividades para exibir os resultados da criação de perfil em uma tabela abaixo. Também é possível exportar os resultados da criação de perfil. Para obter mais informações, consulte [DQS Administration](../data-quality-services/dqs-administration.md).  
  
##  <a name="notifications"></a><a name="Notifications"></a>Notificações  
 Além de coletar e exibir estatísticas e métricas importantes por meio da criação de perfil, o DQS gerará notificações (se habilitado) para indicar quando talvez você queira executar uma ação com base nas estatísticas de criação de perfil exibidas. O DQS utiliza notificações para enfatizar fatos importantes sobre a fonte de dados e mostrar a eficácia da atividade atual em comparação com a finalidade para a qual foi executada. As notificações fornecem dicas e recomendações que indicam uma condição e recomendam como você pode aprimorar uma atividade de descoberta da base de dados de conhecimento, limpeza de dados ou correspondência de dados.  
  
 Uma notificação do DQS é usada para gerar uma questão que pode ser interessante para você ou abordar um problema potencial. Se você age sobre a notificação depende se ela é relevante para seus propósitos. Por exemplo, vamos supor que o DQS publique uma notificação quando a limpeza de dados não produzir valores corrigidos ou valores sugeridos quando a integridade e a exatidão forem 100%. Esta notificação indicaria que a atividade talvez não precise ser executada. Se você vai optar por executar a atividade, no entanto, essa é uma decisão sua.  
  
 Uma notificação é indicada por uma dica de ferramenta com um ponto de exclamação na guia **Perfil.** As estatísticas associadas à notificação são coloridas em vermelho para indicar a justificativa estatística para a notificação.  
  
 Você pode habilitar (o padrão) ou desabilitar as notificações na guia **Configurações Gerais** da seção **Administração** da página inicial Cliente Data Quality. Quando a notificação é desativada, as dicas da ferramenta não são exibidas e as estatísticas não são coloridas em vermelho. Não há melhora significativa no desempenho desativando notificações. A criação de perfil ainda estará operacional se você desabilitar as notificações.  
  
 Para condições específicas associadas a notificações de uma atividade, consulte os seguintes artigos:  
  
-   [Executar a descoberta da base de dados de conhecimento](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [Limpar dados usando o conhecimento &#40;interno&#41; do DQS](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Criar uma política de correspondência](../data-quality-services/create-a-matching-policy.md)  
  
-   [Executar um projeto de correspondência](../data-quality-services/run-a-matching-project.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Artigo|  
|----------------------|-----------|  
|Descreve como habilitar ou desabilitar as notificações no DQS.|[Habilitar ou desabilitar notificações de criação de perfil no DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
  
  
