---
title: Definir armazenamento de partição (Analysis Services - Multidimensional) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- low latency MOLAP
- standard storage [Analysis Services]
- hybrid OLAP
- automatic MOLAP
- relational OLAP
- multidimensional OLAP
- scheduled MOLAP [Analysis Services]
- partitions [Analysis Services], storage
- HOLAP
- MOLAP
- real time ROLAP
- real time HOLAP
- ROLAP
- medium latency MOLAP
ms.assetid: e525e708-f719-4905-a4cc-20f6a9a3edcd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d86734023080c9b7fc62cff636d4f1952d00d0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072985"
---
# <a name="set-partition-storage-analysis-services---multidimensional"></a>Definir armazenamento de partição (Analysis Services – Multidimensional)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece várias configurações de armazenamento padrão para modos de armazenamento e opções de cache. São configurações usadas normalmente para notificação de atualizações, latência e recriação de dados.  
  
 Você pode especificar o armazenamento da partição na guia Partições do cubo no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], ou na página de propriedades da partição no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="guidelines-for-choosing-a-storage-mode"></a>Diretrizes para escolher um modo de armazenamento  
 Para um grupo de medidas grande, é uma prática comum configurar o armazenamento de modo diferente para partições diferentes. Considere as seguintes diretrizes:  
  
-   Use o ROLAP em tempo real para os dados atuais que estão sendo atualizados continuamente.  
  
-   Use o cache pró-ativo com latência baixa ou média para partições baseadas em fontes de dados que estão sendo atualizadas com menos frequência.  
  
-   Use o MOLAP automático para fontes de dados das quais os usuários exigem alto desempenho, mas podem suportar alguma latência dos dados.  
  
-   Use o MOLAP agendado para fontes de dados acessadas continuamente pelos usuários, mas atualizadas apenas periodicamente.  
  
-   Use o armazenamento MOLAP sem cache pró-ativo para as partições alteradas com pouca frequência ou que não são alteradas, para as partições cujos dados mais recentes não precisam ser procurados pelos usuários e se os dados não precisarem ficar disponíveis continuamente para os usuários durante qualquer atualização e processamento necessários.  
  
 Essas são diretrizes gerais. Uma análise cuidadosa e testes podem ser necessários para desenvolver o melhor esquema de armazenamento possível para seus dados. Você também pode configurar manualmente definições de armazenamento para uma partição se nenhuma configuração padrão satisfizer suas necessidades.  
  
## <a name="storage-settings-descriptions"></a>Descrição das configurações de armazenamento  
  
|Configuração de armazenamento padrão|Descrição|  
|------------------------------|-----------------|  
|ROLAP em tempo real|O OLAP é em tempo real. Os dados de detalhe e as agregações são armazenados em formato relacional. O servidor escuta as notificações quando os dados são alterados e todas as consultas refletem o estado atual dos dados (latência zero).<br /><br /> Essa configuração normalmente seria usada para uma fonte de dados com atualizações muito frequentes e contínuas, quando os dados mais recentes sempre são solicitados pelos usuários. Dependendo dos tipos de consulta gerados pelos aplicativos cliente, esse método fornece os tempos de resposta mais lentos.|  
|HOLAP em tempo real|O OLAP é em tempo real. Os dados de detalhe são armazenados em um formato relacional, enquanto as agregações são armazenadas em um formato multidimensional. O servidor escuta as notificações quando os dados são alterados e atualiza as agregações OLAP multidimensionais (MOLAP) conforme necessário. Nenhum cache MOLAP é criado. Sempre que a fonte de dados é atualizada, o servidor passa para o OLAP relacional (ROLAP) em tempo real até que as agregações sejam atualizadas. Todas as consultas refletem o estado atual dos dados (latência zero).<br /><br /> Essa configuração normalmente seria usada para uma fonte de dados com atualizações frequentes e contínuas (mas não tão frequentes quanto o ROLAP em tempo real) e os usuários sempre solicitam os dados mais recentes. Esse método normalmente fornece um melhor desempenho geral do que o armazenamento ROLAP. Os usuários podem obter o desempenho MOLAP a partir dessa configuração se a fonte de dados permanecer silenciosa por um período longo o suficiente.|  
|MOLAP de baixa latência|Os dados de detalhe e as agregações são armazenados em formato multidimensional. O servidor escuta as notificações das alterações de dados e passa para o ROLAP em tempo real, enquanto os objetos MOLAP são reprocessados em um cache. Um intervalo de silêncio de pelo menos 10 segundos é obrigatório antes de atualizar o cache. Há um intervalo de substituição de 10 minutos se o intervalo de silêncio não for atingido. O processamento acontece automaticamente à medida que os dados são alterados com uma latência de destino de 30 minutos depois da primeira alteração.<br /><br /> Essa configuração normalmente seria usada para uma fonte de dados com atualizações frequentes, quando o desempenho da consulta é um pouco mais importante do que sempre fornecer os dados mais atuais. Essa configuração processa automaticamente objetos MOLAP sempre que exigidos depois do intervalo de latência. O desempenho fica mais lento enquanto os objetos MOLAP estão sendo reprocessados.|  
|MOLAP de latência média|Os dados de detalhe e as agregações são armazenados em formato multidimensional. O servidor escuta as notificações das alterações de dados e passa para o ROLAP em tempo real, enquanto os objetos MOLAP são reprocessados em cache. Um intervalo de silêncio de pelo menos 10 segundos é obrigatório antes de atualizar o cache. Há um intervalo de substituição de 10 minutos se o intervalo de silêncio não for atingido. O processamento acontece automaticamente à medida que os dados são alterados com uma latência de destino de quatro horas.<br /><br /> Essa configuração normalmente é usada para uma fonte de dados com atualizações frequentes (ou menos frequentes), quando o desempenho da consulta é mais importante do que sempre fornecer os dados mais atuais. Essa configuração processa automaticamente objetos MOLAP sempre que exigidos depois do intervalo de latência. O desempenho fica mais lento enquanto os objetos MOLAP estão sendo reprocessados.|  
|MOLAP automático|Os dados de detalhe e as agregações são armazenados em formato multidimensional. O servidor escuta as notificações, mas mantém o cache MOLAP atual enquanto cria um novo. O servidor nunca passa para o OLAP em tempo real e as consultas podem ficar obsoletas enquanto o novo cache é criado.<br /><br /> Um intervalo de silêncio de pelo menos 10 segundos é obrigatório antes de criar o novo cache MOLAP. Há um intervalo de substituição de 10 minutos se o intervalo de silêncio não for atingido. O processamento acontece automaticamente à medida que os dados são alterados com uma latência de destino de duas horas.<br /><br /> Essa configuração normalmente é usada para uma fonte de dados quando o desempenho da consulta é de importância fundamental. Essa configuração processa automaticamente objetos MOLAP sempre que exigidos depois do intervalo de latência. As consultas não retornam os dados mais recentes enquanto o novo cache está sendo criado e processado.|  
|MOLAP agendado|Os dados de detalhe e as agregações são armazenados em um formato multidimensional. O servidor não recebe notificações quando os dados são alterados. O processamento acontece automaticamente a cada 24 horas.<br /><br /> Essa configuração normalmente é usada para uma fonte de dados quando apenas as atualizações diárias são obrigatórias. As consultas sempre são feitas nos dados do cache MOLAP, que não é descartado até um novo cache ser criado e seus objetos serem processados.|  
|MOLAP|O cache pró-ativo não é habilitado. Os dados de detalhe e as agregações são armazenados em formato multidimensional. O servidor não recebe notificações quando os dados são alterados. O processamento deve ser programado ou executado manualmente.<br /><br /> Essa configuração normalmente é usada para uma fonte de dados na qual as atualizações periódicas são desnecessárias para os aplicativos cliente, mas para a qual o alto desempenho é fundamental.<br /><br /> O armazenamento MOLAP sem cache pró-ativo fornece o melhor desempenho possível caso os aplicativos não precisem dos dados mais recentes. É necessário um tempo de inatividade para processar os objetos atualizados, embora esse tempo possa ser minimizado com a atualização e o processamento de cubos em um servidor de preparação e com o uso da sincronização de banco de dados para copiar os objetos MOLAP atualizados e processados no servidor de produção.|  
  
## <a name="custom-storage-options"></a>Opções de armazenamento personalizadas  
 Em vez de usar um das configurações de armazenamento padrão, é possível configurar manualmente o armazenamento e o cache pró-ativo. Antes de criar configurações personalizadas, clique primeiro na opção **Configuração padrão** e mova o controle deslizante até a configuração padrão que mais se aproxima da configuração que deseja usar. Em seguida, para criar uma configuração personalizada, clique na opção **Configurações personalizadas** e em **Opções**.  
  
-   É possível especificar se as alterações feitas na fonte de dados devem disparar atualizações no cache. Para permitir um nível tolerável de alterações, especifique um intervalo mínimo de silêncio após as atualizações na fonte de dados. Também é possível especificar um novo intervalo de silêncio que atualizará o cache após um período especificado se o intervalo entre as alterações na fonte de dados nunca atingir o mínimo.  
  
-   Você pode especificar se deseja descartar o cache desatualizado durante as atualizações. Se essa opção for selecionada, quando a latência especificada for ultrapassada, o servidor mudará para o OLAP relacional (ROLAP) em tempo real enquanto atualiza o cache. Se essa opção não for escolhida, o servidor continuará consultando o cache do OLAP multidimensional (MOLAP) obsoleto enquanto cria o novo cache.  
  
     É possível especificar o intervalo de latência que deve acontecer entre as alterações e o descarte de um cache desatualizado. Esse intervalo representa o período do tempo que os usuários podem continuar procurando dados no cache desatualizado antes de ser descartado. Se as alterações ocorrerem e o cache ainda estiver sendo atualizado ou processado no final desse intervalo, as consultas serão redirecionadas para o ROLAP.  
  
-   Se desejar atualizar periodicamente os objetos MOLAP armazenados em cache independentemente das alterações na fonte de dados, programe atualizações forçadas do cache. Os benefícios do OLAP em tempo real variam de acordo com o tamanho do banco de dados e o período de latência atribuído pela frequência de alterações dos dados de origem. Os usuários devem enviar consultas para o cache com a maior frequência possível, não para o ROLAP.  
  
 Se a caixa de seleção **Aplicar configurações a dimensões** for marcada, as mesmas configurações de armazenamento serão aplicadas nas dimensões relacionadas ao grupo de medidas. Os valores de dimensão são, inicialmente, iguais aos valores de partição.  
  
## <a name="see-also"></a>Consulte também  
 [Partições em modelos multidimensionais](partitions-in-multidimensional-models.md)  
  
  
