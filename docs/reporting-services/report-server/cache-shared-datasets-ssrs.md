---
title: Conjunto de dados compartilhados em cache | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 4acb1bbe-1c04-4979-b893-dc1b1c5039b6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9436fd4963c5c9af86f3ea4ede200952fb6deb59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77082550"
---
# <a name="cache-shared-datasets-ssrs"></a>Conjuntos de dados compartilhado em cache (SSRS)
  Os resultados de consultas de um conjunto de dados compartilhado podem ser copiados para um cache para fornecer dados consistentes para vários relatórios e melhorar o tempo de resposta da consulta do conjunto de dados. Como relatórios, você pode configurar um conjunto de dados compartilhado para ser armazenado em cache no primeiro uso ou especificando uma agenda.  
  
 Um conjunto de dados compartilhado pode ser incluído em vários relatórios ou como parte de definições de componente. Armazenando em cache o conjunto de dados compartilhado, você fornece um conjunto de dados consistente para todos os relatórios que o usam e também reduz o número de vezes que a consulta de conjunto de dados é executada em relação à fonte de dados externa.  
  
 A lista a seguir fornece exemplos de quando armazenar em cache um conjunto de dados compartilhado:  
  
-   A consulta leva uma quantidade significativa de tempo para ser executada.  
  
-   A consulta usa parâmetros, mas na maior parte do tempo, o número de combinações de parâmetros é pequeno. Cada combinação cria resultados da consulta armazenados em cache.  
  
-   A consulta é executada em horas previsíveis do dia, semana ou mês.  
  
-   A consulta é executada como o resultado de uma referência de conjunto de dados compartilhado em um relatório que é entregue por email, onde é provável que um grande número de pessoas clique no link em um curto período de tempo.  
  
 A lista a seguir fornece exemplos de quando não armazenar em cache um conjunto de dados compartilhado:  
  
-   Os resultados da consulta devem sempre incluir os dados mais recentes.  
  
-   A consulta é executada rapidamente.  
  
-   A consulta é executada com pouca frequência.  
  
-   A consulta usa parâmetros, o número de combinações de parâmetros é grande e nenhuma combinação é mais provável que a outra.  
  
-   A fonte de dados na qual o conjunto de dados compartilhado é baseado tem Prompt ou credenciais do Windows Integrado.  
  
-   O filtro ou a consulta do conjunto de dados compartilhado contém uma expressão com uma referência à coleção global Usuário.  
  
 Se um usuário escolher valores de parâmetros de relatório diferentes dos valores padrão especificados para o conjunto de resultados armazenado em cache, a consulta do conjunto de dados será executada ativamente e os resultados armazenados em cache não serão usados para essa consulta.  
  
## <a name="caching-shared-datasets"></a>Armazenando em cache conjuntos de dados compartilhados  
 Para habilitar o armazenamento em cache de um conjunto de dados compartilhado, você deve selecionar a opção de cache no conjunto de dados compartilhado. Depois que o armazenamento em cache é habilitado, os resultados da consulta de um conjunto de dados compartilhado são copiados no cache no primeiro uso. Se o conjunto de dados compartilhado tiver parâmetros, cada combinação de parâmetros criará uma nova entrada no cache.  
  
 Enquanto os resultados da consulta para uma combinação de parâmetros específica estão no cache, cada relatório iniciado para processamento e que inclui uma referência ao conjunto de dados compartilhado com esses valores de parâmetros usará os dados armazenados em cache.  
  
 Você pode especificar por quanto tempo os dados devem ser mantidos no cache antes de expirarem. Para saber mais, confira [Trabalhando com conjuntos de dados compartilhados](../../reporting-services/work-with-shared-datasets-web-portal.md).  
  
## <a name="preloading-the-cache"></a>Pré-carregando o cache  
 Você pode pré-carregar o cache criando um plano de atualização de cache. Com um plano de atualização, você pode especificar com que frequência atualizar o cache usando uma agenda específica de item ou uma agenda compartilhada. Para evitar várias entradas no cache para o mesmo item, a agenda especificada deve permitir tempo de processamento suficiente para o processamento da consulta na fonte de dados externa. Por exemplo, se a consulta levar 20 minutos para ser executada, a agenda de atualização deverá ser maior que 20 minutos. Para obter mais informações, consulte [Schedules](../../reporting-services/subscriptions/schedules.md).  
  
 Para criar um plano de atualização de cache para um conjunto de dados compartilhado, as seguintes condições são aplicadas.  
  
-   O conjunto de dados compartilhado deve estar habilitado para armazenamento em cache.  
  
-   A fonte de dados compartilhada da qual o conjunto de dados compartilhado depende não pode usar Prompt ou credenciais do Windows Integrado.  
  
-   Se o conjunto de dados compartilhado tiver parâmetros, você deverá especificar valores padrão estáticos para cada parâmetro que não esteja marcado como somente leitura. Parâmetros somente leitura sempre usarão o valor padrão. Para armazenar em cache um conjunto de dados compartilhado para várias combinações de parâmetros, você deve criar um plano de atualização de cache separado para cada combinação. Parâmetros não podem conter referências a outros conjuntos de dados.  
  
-   Cada plano de atualização do cache está associado a apenas um conjunto de dados compartilhado ou relatório.  
  
-   Você deve ter as permissões ReadPolicy e UpdatePolicy no conjunto de dados compartilhado.  
  
 Os planos de atualização do cache se aplicam a conjuntos de dados compartilhados e relatórios. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
## <a name="conditions-that-cause-cache-expiration"></a>Condições que provocam a expiração do cache  
 As condições a seguir podem fazer com que um cache de conjunto de dados compartilhado se torne inválido.  
  
-   Uma condição de agenda expira. O tempo limite do cache é esgotado ou o tempo de expiração ocorre.  
  
-   Uma agenda compartilhada é excluída.  
  
-   Alterações em uma agenda compartilhada. Agendas compartilhadas podem ser pausadas, o que também afeta quando um cache expira.  
  
-   A definição de consulta do conjunto de dados compartilhado é alterada.  
  
-   As credenciais da fonte de dados compartilhada da qual o conjunto de dados compartilhado depende são alteradas.  
  
-   As opções de cache do conjunto de dados compartilhado são alteradas.  
  
-   Os valores padrão dos parâmetros somente leitura do conjunto de dados compartilhado são alterados.  
  
-   Os filtros que fazem parte da definição do conjunto de dados compartilhado são alterados.  
  
-   O conjunto de dados compartilhado é excluído do servidor de relatório. Quando um conjunto de dados compartilhado é excluído, as cópias armazenadas em cache associadas e os planos de atualização de cache também são excluídos.  
  
 As atualizações nos planos de atualização do cache de conjuntos de dados compartilhados não afetam os relatórios que já estão sendo processados. A atualização de um plano de atualização do cache afeta apenas inicializações futuras de relatórios que fazem referência ao conjunto de dados compartilhado.  
  
## <a name="see-also"></a>Confira também
  
 [Gerenciar conjuntos de dados compartilhados](../../reporting-services/report-data/manage-shared-datasets.md)  
  