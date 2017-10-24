---
title: "Agregações e Designs de agregação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- aggregations [Analysis Services], about aggregations
- storage [Analysis Services], aggregations
- Storage Design Wizard
- data summary [Analysis Services]
- data storage [Analysis Services]
- storing data [Analysis Services], aggregations
- aggregations [Analysis Services]
ms.assetid: 35bd8589-39fa-4e0b-b28f-5a07d70da0a2
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8554ed91ce593803fe1043823aa0e97aa890043b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="aggregations-and-aggregation-designs"></a>Agregações e designs de agregação
  Um objeto <xref:Microsoft.AnalysisServices.AggregationDesign> define um conjunto de definições de agregação que podem ser compartilhadas por várias partições.  
  
 Um objeto <xref:Microsoft.AnalysisServices.Aggregation> representa o resumo de dados de grupo de medidas em determinada granularidade de dimensões.  
  
 Um objeto simples <xref:Microsoft.AnalysisServices.Aggregation> é composto de: informações básicas e dimensões. As informações básicas incluem o nome da agregação, o ID, as anotações e uma descrição. As dimensões coleções de objetos <xref:Microsoft.AnalysisServices.AggregationDimension> que contêm a lista de atributos de granularidade para a dimensão.  
  
 As agregações são resumos pré-calculados de dados de células folha. As agregações melhoram o tempo de resposta de consulta preparando as respostas antes das perguntas serem feitas. Por exemplo, quando uma tabela de fatos de data warehouse contém centenas de milhares de linhas, uma consulta que solicita os totais de vendas semanais de uma determinada linha de produtos, pode demorar um longo tempo para ser respondida se todas as linhas na tabela de fatos tiverem de ser verificadas e somadas na consulta para calcular a resposta. No entanto, a resposta pode ser quase imediata se os dados de resumo para responder essa consulta tiverem sido pré-calculados. Esse pré-cálculo de dados do resumo ocorre durante o processamento e é base dos tempos de resposta rápida da tecnologia OLAP.  
  
 Os cubos são o modo que a tecnologia OLAP usa para organizar dados resumidos em estruturas multidimensionais. As dimensões e suas hierarquias de atributos refletem as consultas que podem ser feitas ao cubo. As agregações são armazenadas na estrutura multidimensional em células em coordenadas especificadas pelas dimensões. Por exemplo, a pergunta "Quais foram as vendas do produto X em 1998 para a região noroeste?" envolve três dimensões (produto, tempo e geografia) e uma medida (vendas). O valor da célula no cubo em coordenadas especificadas (produto X, 1998, noroeste) é a resposta, um único valor numérico.  
  
 Outras perguntas podem retornar vários valores. Por exemplo, "De quanto eram as vendas de produtos de hardware por trimestre, por região, em 1998?" Tais consultas retornam conjuntos de células das coordenadas que atendem às condições especificadas. O número de células retornado pela consulta depende do número de itens no nível Hardware da dimensão Produto, os quatro trimestres em 1998 e o número de regiões na dimensão Geografia. Se todos os dados de resumo tiverem sido pré-calculados em agregações, o tempo de resposta da consulta dependerá apenas do tempo necessário para extrair as células específicas. Nenhum cálculo ou leitura de dados da tabela de fatos é necessário.  
  
 Apesar do pré-cálculo de todas as agregações possíveis em um cubo fornecer o tempo de resposta mais rápido possível para todas as consultas, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode facilmente calcular alguns valores de agregação de outras agregações pré-calculadas. Além disso, calcular todas as agregações possíveis requer tempo de processamento e armazenamento significativos. Portanto, há um equilíbrio entre requisitos de armazenamento e a porcentagem de possíveis agregações que são pré-calculadas. Se nenhuma agregação for pré-calculada (0%), a quantidade de tempo de processamento e espaço de armazenamento, necessários para um cubo, serão reduzidos mas o tempo de resposta da consulta será maior, pois os dados necessários para responder a cada consulta deverão ser recuperados de células folha e, em seguida, agregados na consulta. Por exemplo, retornar um único número que responda à questão feita anteriormente ("Quais são as vendas do produto X em 1998 para a região noroeste"), pode exigir a leitura de milhares de linhas de dados, extraindo o valor da coluna usada para fornecer a medida Vendas de cada linha e, então, calcular a soma. Além disso, o tempo necessário para recuperar os dados variará, dependendo do modo de armazenamento escolhido para os dados — MOLAP, HOLAP ou ROLAP.  
  
## <a name="designing-aggregations"></a>Projetando agregações  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incorpora um algoritmo sofisticado para selecionar agregações para pré-cálculo para que outras agregações podem ser rapidamente computadas a partir de valores pré-calculados. Por exemplo, se as agregações forem pré-calculadas para o nível Mês da hierarquia Tempo, o cálculo do nível Trimestre exigirá apenas o resumo de três números, os quais podem ser rapidamente computados sob demanda. Essa técnica economiza tempo de processamento e reduz os requisitos de armazenamento, com efeito mínimo sobre o tempo de resposta de consulta.  
  
 O Assistente de Design de Agregação oferece opções para você especificar as restrições de armazenamento e a porcentagem no algoritmo para atingir um equilíbrio satisfatório entre o tempo de resposta da consulta e os requisitos de armazenamento. Porém, o algoritmo do Assistente de Design de Agregação assume que todas as consultas possíveis são igualmente prováveis. O Assistente de Otimização com Base no Uso permite ajustar o projeto da agregação para um grupo de medidas, analisando as consultas enviadas por aplicativos cliente. Usando o assistente para ajustar a agregação do cubo, você pode aumentar a capacidade de resposta para consultas frequentes e diminuir a capacidade de resposta de consultas não frequentes sem afetar significativamente o armazenamento necessário para o cubo.  
  
 As agregações são projetadas usando os assistentes, mas não são calculadas até que a partição para a qual as agregações são projetadas seja processada. Depois que a agregação tiver sido criada, se a estrutura do cubo mudar alguma vez ou se forem adicionados ou alterados dados nas tabelas de origem do cubo, geralmente será necessário examinar as agregações do cubo e processá-lo novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Modos de armazenamento de partição e processamento](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  

