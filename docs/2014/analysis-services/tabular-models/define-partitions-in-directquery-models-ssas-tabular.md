---
title: Partições e modo DirectQuery (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f445b32e0c580cde10f38a22b3d26270d927c5a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757318"
---
# <a name="partitions-and-directquery-mode-ssas-tabular"></a>Partições e modo DirectQuery (SSAS tabular)
  Esta seção explica como as partições são usadas em modelos DirectQuery. Para obter mais informações gerais sobre partições em modelos de tabela, consulte [Partições &#40;SSAS de Tabela&#41;](partitions-ssas-tabular.md).  
  
 Para obter instruções sobre como alterar a partição que é usada, ou exibir informações sobre a partição, consulte [alterar a partição DirectQuery &#40;SSAS de tabela&#41;](../change-the-directquery-partition-ssas-tabular.md).  
  
## <a name="using-partitions-in-directquery-mode"></a>Usando partições no modo DirectQuery  
 Para cada tabela, você deve especificar uma única partição para usar como a fonte de dados DirectQuery.  Se houver várias partições, quando você alternar o modelo para habilitar o modo DirectQuery, por padrão a primeira partição que foi criada na tabela será sinalizada como a partição DirectQuery. Você pode alterar isso posteriormente usando o Gerenciador de Partições no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Por que permitir apenas uma partição única no modo DirectQuery?  
  
 Em modelos de tabela (como em modelos OLAP), as partições de uma tabela são definidas através de consultas SQL. O desenvolvedor que cria a definição de partição é responsável por assegurar que não haja sobreposição de partições. O Analysis Services não verifica se os registros pertencem em uma ou várias partições.  
  
 As partições em um modelo de tabela armazenado em cache se comportam da mesma forma. Se você estiver usando um modelo na memória, enquanto o cache estiver sendo acessado, fórmulas DAX serão avaliadas para cada partição e os resultados serão combinados. Porém, quando um modelo de tabela usa o modo DirectQuery, é impossível avaliar várias partições, combinar os resultados e converter isso em uma instrução SQL a ser enviada ao repositório de dados relacional. Essa ação pode causar a perda inaceitável de desempenho e imprecisões em potencial, já que os resultados são agregados.  
  
 Portanto, para consultas respondidas no modo DirectQuery, o servidor usa uma única partição que foi marcada como a partição primária para acesso do DirectQuery, chamada de *partição DirectQuery*.  A consulta SQL especificada na definição dessa partição define o conjunto completo de dados que podem ser usados para responder a consultas no modo DirectQuery.  
  
 Se você não definir a partição explicitamente, o mecanismo simplesmente emitirá uma consulta SQL à fonte de dados relacional inteira, executará qualquer operação baseada em conjunto ditada pela fórmula DAX e retornará os resultados da consulta.  
  
 Se você tiver várias partições em uma tabela, e selecionar uma partição como a partição DirectQuery, por padrão, todas as outras partições serão marcadas como apenas de uso na memória.  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>Partições em modelos armazenados em cache e em modelos DirectQuery  
 Quando você configura uma partição DirectQuery, deve especificar opções de processamento para a partição.  
  
 Há duas opções de processamento para a partição DirectQuery. Para definir essa propriedade, use o **Gerenciador de Partições** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e selecione a propriedade **Opção de Processamento** . A tabela a seguir lista os valores desta propriedade e descreve os efeitos de cada valor quando combinados com a propriedade DirectQueryUsage na cadeia de conexão:  
  
|**DirectQueryUsage** propriedade|Propriedade**Opção de Processamento** |Observações|  
|-----------------------------------|------------------------------------|-----------|  
|DirectQuery|Nunca processar esta partição|Quando o modelo só estiver usando o DirectQuery, o processamento nunca será necessário.<br /><br /> Em modelos híbridos, você pode configurar a partição DirectQuery para nunca ser processada. Por exemplo, se você estiver operando em um conjunto de dados muito grande e não desejar adicionar os resultados completos ao cache, poderá especificar que a partição DirectQuery inclua a união de resultados para todas as outras partições na tabela e que nunca processe a união. As consultas destinadas à fonte relacional não serão afetadas e as consultas em dados armazenados em cache combinarão dados das outras partições|  
|InMemory com DirectQuery|Permitir que a partição seja processada|Se o modelo estiver usando o modo híbrido, você deve usar a mesma partição para consultas na memória e consultas na fonte de dados DirectQuery.|  
  
## <a name="see-also"></a>Consulte também  
 [Partições &#40;SSAS de Tabela&#41;](partitions-ssas-tabular.md)  
  
  
