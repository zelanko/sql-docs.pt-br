---
title: Perfil de dados e notificações no DQS
ms.date: 03/15/2020
ms.prod: sql
ms.reviewer: jroth
ms.technology: data-quality-services
ms.topic: conceptual
author: swinarko
ms.author: sawinark
ms.openlocfilehash: e0bd9585a48ee30368d145c79f8431e922801a9c
ms.sourcegitcommit: c30a2def43c86860aeec69d3e3029f2296544b13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2020
ms.locfileid: "80243396"
---
# <a name="data-profiling-and-notifications-in-data-quality-services-dqs"></a>Criação de perfil de dados e notificações no DQS (Data Quality Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)](DQS) é um serviço de criação de perfil de dados. O DQS analisa os dados de uma fonte e exibe as estatísticas sobre os dados nas atividades do DQS.

## <a name="attributes-goals-benefits"></a>Atributos, metas, benefícios

### <a name="attributes-of-dqs"></a>Atributos do DQS

A criação de perfil do DQS tem os seguintes atributos:

- Fornece medidas automatizadas de qualidade de dados.
- É integrado ao gerenciamento de conhecimento do DQS e a projetos de qualidade de dados.
- É dinâmico e ajustável.

### <a name="goals-of-dqs"></a>Metas do DQS

A criação de perfil com o DQS tem os dois principais objetivos a seguir:

- Para orientá-lo nos processos de qualidade de dados e para dar suporte às suas decisões.
- Para avaliar a eficácia dos processos.

### <a name="benefits-of-dqs"></a>Benefícios do DQS

A criação de perfil do DQS tem os seguintes benefícios:

- Fornece informações sobre a qualidade de seus dados de origem e ajuda a identificar problemas de qualidade de dados.

- Avalia os processos de qualidade de dados e orienta seu:
  - Descoberta de conhecimento
  - Limpeza de dados
  - Política de correspondência
  - Trabalho de correspondência

- Apresenta as informações mais relevantes no momento mais relevante.

- Gera notificações que enfatizam estatísticas importantes ou eventos que podem exigir ação. As notificações do DQS geralmente indicam uma condição e recomendam a ação corretiva.

A criação de perfil do DQS fornece descoberta de conhecimento, limpeza de dados e correspondência de dados. O DQS também é uma ferramenta de análise de dados. Você pode criar uma base de dados de conhecimento para análise. Em seguida, você pode executar a descoberta de conhecimento usando a base de dados de conhecimento. A descoberta de conhecimento usa estatísticas de criação de perfil para determinar se a base de dados de conhecimento atende às suas necessidades de descoberta, limpeza e correspondência.

## <a name="how-dqs-profiling-works"></a><a name="How"></a>Como funciona a criação de perfil do DQS

A criação de perfil do DQS não mede a qualidade da base de dados de conhecimento. A criação de perfil mede a qualidade dos dados de origem. A criação de perfil fornece estatísticas que indicam o efeito dos seguintes esforços:

- Sua operação específica no gerenciamento de conhecimento.
- Um projeto de qualidade de dados em seus dados de origem.

### <a name="activity-context"></a>Contexto da atividade

A criação de perfil está sempre no contexto da atividade específica que você está executando. Você pode clicar na guia criação de perfil em uma tela para exibir dados de criação de perfil. Esse clique não o retira do estágio da atividade que você está executando. A tabela de criação de perfil é populada em tempo real conforme o processo é executado. Portanto, você pode avaliar as tarefas de qualidade de dados enquanto as executa.

É possível determinar se os dados de origem ficam melhores após a limpeza ou desduplicação e o quanto melhoram.

### <a name="profiling-is-based-on-counts"></a>A criação de perfil é baseada em contagens

Todos os números de criação de perfil referem-se à contagem de aparências de valores específicos. Em muitos casos, os números referem-se à porcentagem do total. As métricas de exclusividade são uma exceção. As métricas de exclusividade referem-se ao número absoluto de valores, independentemente da contagem de aparências desses valores.

### <a name="knowledge-driven-solution"></a>Solução controlada por conhecimento

A criação de perfil faz parte da solução voltada para conhecimentos do DQS. A criação de perfil fornece informações sobre um processo de base de conhecimento, correspondência ou limpeza de dados. As informações se baseiam no mapeamento entre os campos de fonte de dados e os domínios da base de conhecimento. A criação de perfil é executada somente após a conclusão do mapeamento. Nenhuma criação de perfil é executada durante o estágio de mapeamento de qualquer atividade.

A criação de perfil sempre está associada a uma atividade. O processo de criação de perfil é executado nos dados que são _mapeados_ para domínios, não nos dados _nos_ domínios.

A criação de perfil está integrada nas seguintes etapas de atividades:

- As etapas de **descobrir** e **gerenciar valores de domínio** da atividade de descoberta da base de dados de conhecimento.

- As etapas **limpar** e **gerenciar e exibir resultados** da atividade de limpeza.

- As etapas de **política de correspondência** e **resultados de correspondência** da atividade de política de correspondência.

- As etapas de **correspondência** e **exportação** da atividade de correspondência.

O DQS não fornece estatísticas de criação de perfil para a atividade Gerenciamento de Domínio.

## <a name="profiling-data-by-activity"></a><a name="Activity"></a>Criação de perfil de dados por atividade

A criação de perfil do DQS usa as seguintes dimensões de qualidade de dados padrão para representar a qualidade dos dados:

- Integridade – a extensão até a qual os dados estão presentes.
- Exatidão – a extensão até a qual os dados podem ser usados para seu uso pretendido.
- Exclusividade – a extensão até a qual valores diferentes representam entidades diferentes.

Por padrão, valores nulos e vazios são considerados ausentes ou reduzem a porcentagem de integridade. No entanto, você pode definir outros valores como NULL-equivalente. Esses valores também são considerados ausentes.

A criação de perfil fornece as estatísticas de que você precisa para avaliar seus processos, mas é necessário interpretá-las. Entenda o que a criação de perfil está informando a você examinando as estatísticas coluna por coluna.

### <a name="differing-sets-of-profiling-statistics"></a>Diferentes conjuntos de estatísticas de criação de perfil

As atividades do DQS têm conjuntos diferentes de estatísticas de criação de perfil, da seguinte forma:

- Somente a atividade Limpeza tem estatísticas de criação de perfil quanto à precisão (em percentual por domínio). A precisão é afetada pela validade, consistência, erros de sintaxe e regras de domínio.

- Somente a atividade Limpeza tem estatísticas de criação de perfil quanto a valores corretos, corrigidos e sugeridos na origem e valores corrigidos e sugeridos pelo domínio (ambos de número de percentual).

- As atividades Limpeza e Descoberta da Base de Dados de Conhecimento têm estatísticas de criação de perfil quanto à validade (Limpeza por registro, Descoberta da Base de Dados de Conhecimento por registro e domínio). As atividades Política de Correspondência e Correspondência não têm estatísticas de validade.

- As estatísticas de criação de perfil são fornecidas para exclusividade, para a origem e por domínio. Esta instrução aplica-se às seguintes atividades:
  - Descoberta da base de dados de conhecimento.
  - Política de correspondência.
  - Combine.
  - Mas _não_ para a atividade de limpeza.

O DQS oferece estatísticas de criação de perfil específicas relacionadas a uma atividade. Para obter detalhes, consulte as seções de **criação de perfil** nos seguintes tópicos:

- [Executar a descoberta da base de dados de conhecimento](../data-quality-services/perform-knowledge-discovery.md)

- [Limpar dados usando o conhecimento de&#41; interno do DQS &#40;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [Criar uma política de correspondência](../data-quality-services/create-a-matching-policy.md)

- [Executar um projeto de correspondência](../data-quality-services/run-a-matching-project.md)

## <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>Criação de perfil de dados no monitoramento de atividades

As informações de criação de perfil estão disponíveis não apenas nas páginas de atividade do cliente Data Quality, mas também no monitoramento de atividades. As informações referem-se à descoberta de conhecimento, política de correspondência, correspondência e atividades de limpeza. As informações estão disponíveis nas páginas de atividade do cliente Data Quality e no monitoramento de atividades.

Você pode exibir todos os seguintes itens em um único local:

- Propriedades
- Processos computacionais relacionados de atividades
- Informações de criação de perfil geradas para cada atividade

Você seleciona uma atividade na tabela de atividades para exibir os resultados da criação de perfil na segunda tabela. Também é possível exportar os resultados da criação de perfil.

Para obter mais informações, consulte [DQS Administration](../data-quality-services/dqs-administration.md).

## <a name="notifications"></a><a name="Notifications"></a>Notificações

O DQS gera notificações para indicar quando você pode desejar executar uma ação com base nas estatísticas de perfil. O DQS usa notificações para fatos importantes sobre a fonte de dados. Esses fatos mostram a eficácia da atividade atual em relação à finalidade para a qual ela foi executada. As notificações fornecem dicas e recomendações que indicam uma condição. As notificações também podem recomendar como você pode melhorar uma descoberta de conhecimento, limpeza de dados ou atividade de correspondência de dados.

O DQS envia uma notificação quando detecta um problema que pode ser importante para você. Como uma situação de exemplo, quando a integridade e a exatidão são de 100%, a atividade de limpeza de dados pode não produzir valores corrigidos ou sugeridos. O DQS pode postar uma notificação para essa situação. Essa notificação indicaria que a atividade pode não ser necessária. A possibilidade de executar a atividade continua sendo sua decisão.

Uma notificação é indicada por uma dica de ferramenta com um ponto de exclamação, na guia **criação de perfil** . as estatísticas associadas à notificação são coloridas em vermelho para indicar a justificativa estatística da notificação.

### <a name="disable-notifications"></a>Desabilitar notificações

As notificações são habilitadas por padrão. Mas você pode desabilitar as notificações usando o home page de Data Quality Client. Na seção **Administração** , use a guia **configurações gerais** .

Quando as notificações são desabilitadas, as dicas de ferramenta não são exibidas e as estatísticas não são coloridas em vermelho. A criação de perfil permanece operacional enquanto as notificações são desabilitadas. Não há melhoria no desempenho ao desabilitar notificações.

Para condições específicas associadas às notificações de uma atividade, consulte o seguinte:

- [Executar a descoberta da base de dados de conhecimento](../data-quality-services/perform-knowledge-discovery.md)

- [Limpar dados usando o conhecimento de&#41; interno do DQS &#40;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [Criar uma política de correspondência](../data-quality-services/create-a-matching-policy.md)

- [Executar um projeto de correspondência](../data-quality-services/run-a-matching-project.md)

## <a name="related-tasks"></a>Related Tasks

| Descrição da tarefa | Tópico |
| :--------------- | :---- |
| Descreve como habilitar ou desabilitar as notificações no DQS. | [Habilitar ou desabilitar notificações de criação de perfil no DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md) |
|||
