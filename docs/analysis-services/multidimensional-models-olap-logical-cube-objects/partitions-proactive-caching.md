---
title: Cache pró-ativo (partições) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4959473b120a3a8a0c289ff3cd8f91e89df44b86
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34020753"
---
# <a name="partitions---proactive-caching"></a>Partições - cache pró-ativo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O cache pró-ativo fornece criação automática de cache MOLAP e gerenciamento de objetos OLAP. Os cubos incorporam imediatamente as alterações feitas nos dados no banco de dados, com base em modificações recebidas do banco de dados. O objetivo do cache pró-ativo é oferecer o desempenho do MOLAP tradicional, além de manter a instantaneidade e facilidade de gerenciamento oferecida pelo ROLAP.  
  
 Um objeto simples <xref:Microsoft.AnalysisServices.ProactiveCaching> é composto de: especificação de tempo e notificação de tabela. A especificação de tempo define o período de tempo para atualizar o cache depois que uma notificação de alteração for recebida. A notificação de tabela define o esquema de notificação entre a tabela de dados e o objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
 O armazenamento OLAP multidimensional (MOLAP) fornece a melhor resposta de consulta, mas acarreta alguma latência de dados. Os usuários do armazenamento relacional em tempo real OLAP (ROLAP) pesquisam, de forma imediata, as alterações mais recentes em uma fonte de dados mas com um desempenho significativamente mais baixo do que o do armazenamento OLAP multidimensional (MOLAP), que é causado pela ausência de resumos pré-calculados de dados e porque o armazenamento relacional não é otimizado para consultas do tipo OLAP. Se você tem aplicativos nos quais os usuários precisam visualizar dados recentes e deseja também as vantagens de desempenho do armazenamento MOLAP, o SQL Server Analysis Server oferece a opção de cache pró-ativo adequado a esse cenário, particularmente, em combinação com o uso de partições. O cache pró-ativo é definido por partição e por dimensão. As opções de cache pró-ativo fornecem um equilíbrio entre o bom desempenho do armazenamento MOLAP e a instantaneidade do armazenamento ROLAP e fornece processamento de partição automático quando dados subjacentes mudam ou em um cronograma definido.  
  
## <a name="proactive-caching-configuration-options"></a>Opções de configuração de cache pró-ativo   
 O SQL Server Analysis Services fornece diversas opções de configuração de cache pró-ativo que permitem que você aumente o desempenho, diminua a latência e programe o processamento. Os recursos de cache pró-ativo simplificam o processo de gerenciar a obsolescência de dados. As configurações de cache pró-ativo determinam com qual frequência a estrutura OLAP multidimensional, também chamada de cache MOLAP, é recriada, se o armazenamento MOLAP desatualizado é consultado enquanto o cache é recriado ou a fonte de dados ROLAP subjacente, e se o cache é recriado sob um cronograma ou tem base em alterações no banco de dados.  
  
### <a name="minimizing-latency"></a>Diminuindo a latência  
 Com o cache pró-ativo configurado para reduzir a latência, as consultas do usuário a um objeto OLAP são feitas com armazenamento ROLAP ou MOLAP, dependendo se ocorreram alterações recentes em dados e de como o cache pró-ativo foi configurado. O mecanismo de consulta dirige consultas aos dados de fonte no armazenamento MOLAP até que ocorram alterações na fonte de dados. Para reduzir a latência, após ocorrerem alterações em uma fonte de dados, os objetos MOLAP armazenados em cache são descartados e a consulta alterna para o armazenamento ROLAP enquanto os objetos MOLAP são recriados no cache. Depois que os objetos MOLAP são recriados e processados, as consultas serão alternadas automaticamente para o armazenamento MOLAP. A atualização do cache pode ser extremamente rápida para uma partição pequena, uma vez que a partição pode ser tão pequena quanto o dia atual.  
  
### <a name="maximizing-performance"></a>Aumentando o desempenho  
 Para aumentar o desempenho e também reduzir a latência, o cache também pode ser usado sem descartar os objetos MOLAP atuais. As consultas aos objetos MOLAP prosseguem, enquanto os dados são lidos e processados em um novo cache. Esse método fornece melhor desempenho, mas pode resultar em consultas que retornam dados antigos enquanto o novo cache está sendo criado.  
  
## <a name="see-also"></a>Consulte também  
 [Armazenamento de dimensão](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [Definir armazenamento de partição & #40; Analysis Services - Multidimensional & #41;](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md)  
  
  
