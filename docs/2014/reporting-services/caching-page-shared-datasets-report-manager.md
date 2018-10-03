---
title: Página cache, Shared Datasets (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eac372e9-d2a1-48a8-bbe5-09d101df16ea
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8d19f339b8cb8955ab33f73ea164f8bbfb2e7fce
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205166"
---
# <a name="caching-page-shared-datasets-report-manager"></a>Página Cache, Conjuntos de Dados Compartilhados (Gerenciador de Relatórios)
  Use a página de propriedades Cache para definir as opções de cache para um conjunto de dados compartilhado.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para esse local na interface do usuário.  
  
### <a name="to-open-the-caching-properties-page-for-a-shared-dataset"></a>Para abrir a página de propriedades Cache de um conjunto de dados compartilhado  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cujo conjunto de dados compartilhado você deseja configurar.  
  
2.  Aponte para o conjunto de dados compartilhado e clique na seta para baixo.  
  
3.  Na lista suspensa, clique em **Gerenciar**. A página de propriedades Geral do relatório é aberta.  
  
4.  Clique na guia **Cache** .  
  
## <a name="options"></a>Opções  
 **Conjunto de dados compartilhado em cache**  
 Coloca uma cópia temporária dos dados em um cache quando um usuário abre pela primeira vez um relatório que usa esse conjunto de dados compartilhado. Os usuários subsequentes que executarem o relatório dentro do período de cache receberão a cópia dos dados armazenada em cache. O cache normalmente melhora o desempenho porque os dados são retornados do cache, em vez de haver uma nova execução da consulta de conjunto de dados.  
  
 **Expire o cache após um número de minutos**  
 Especifique o número de minutos para salvar a cópia dos dados armazenada em cache. Assim que uma cópia temporária expirar, os dados não serão mais retornados do cache. Na próxima vez que um usuário abrir um relatório que use esse conjunto de dados compartilhado, a consulta de conjunto de dados será executada e o servidor de relatório colocará novamente uma cópia dos dados atualizados no cache.  
  
 **Expire o cache na seguinte agenda**  
 Agende a hora em que os dados armazenados em cache não serão mais válidos e serão removidos do cache. A agenda pode ser uma agenda compartilhada ou uma que seja específica somente para o conjunto de dados compartilhado atual.  
  
 **Agenda específica do conjunto de dados**  
 Especifique uma agenda que seja usada somente por este conjunto de dados.  
  
 **Agenda compartilhada**  
 Especifique uma agenda que seja compartilhada entre relatórios, assinaturas e outros conjuntos de dados compartilhados.  
  
 **Aplicar**  
 Salve as alterações.  
  
## <a name="see-also"></a>Consulte também  
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Ajuda de F1 do Gerenciador de relatórios](../../2014/reporting-services/report-manager-f1-help.md)   
 [Armazenar conjuntos de dados compartilhados em cache &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)   
 [Agendas](subscriptions/schedules.md)  
  
  
