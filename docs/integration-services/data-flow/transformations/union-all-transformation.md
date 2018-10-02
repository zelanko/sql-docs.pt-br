---
title: Transformação Unir Tudo | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.unionalltrans.f1
- sql13.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4fb378c8ec2021e856c654f57844de1d36a67746
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710134"
---
# <a name="union-all-transformation"></a>transformação Unir Tudo
  A transformação Union All combina várias entradas em apenas uma saída. Por exemplo, as saídas provenientes de cinco origens de Arquivo Simples diferentes podem ser aplicadas à transformação Unir Tudo e combinadas em apenas uma saída.  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 As entradas da transformação são adicionadas à saída da transformação uma após a outra, sem reordenação das linhas. Se o pacote requerer uma saída ordenada, você deve usar a transformação Merge em vez da Union All.  
  
 A primeira entrada que você conectar à transformação Union All será a entrada da qual a transformação criará a saída. As colunas nas entradas que você conectar subsequentemente à transformação serão mapeadas para as colunas, na saída da transformação.  
  
 Para mesclar as entradas, você deve mapear as colunas nas entradas para as colunas na saída. Uma coluna com pelo menos uma entrada deve ser mapeada para cada coluna de saída. O mapeamento entre duas colunas requer que seus metadados tenham correspondência. Por exemplo, as colunas mapeadas devem ter o mesmo tipo de dados.  
  
 Se as colunas mapeadas contiverem dados de cadeia de caracteres e a coluna de saída for mais curta que a de entrada, a coluna da saída será aumentada automaticamente para comportar a coluna de entrada. As colunas de entrada que não forem mapeadas para as de saída serão definidas com valores nulos nas colunas de saída.  
  
 Essa transformação tem várias entradas e apenas uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-union-all-transformation"></a>Configuração da transformação Unir Tudo  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas programaticamente, consulte [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="union-all-transformation-editor"></a>Editor de Transformação Union All
  Use a caixa de diálogo **Editor de Transformação Union All** para mesclar vários conjuntos de linhas de entrada em um único conjunto de linhas de saída. Incluindo a transformação Union All em um fluxo de dados, é possível mesclar dados de vários fluxos de dados, criar conjuntos de dados complexos aninhando transformações Union All e mesclar as linhas novamente após corrigir erros nos dados.  
  
### <a name="options"></a>Opções  
 **Nome da Coluna de Saída**  
 Digite um alias para cada coluna. O padrão é o nome da coluna de entrada da primeira entrada (referência); contudo, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Union All Entrada 1**  
 Selecione a partir da lista de colunas de entrada disponíveis na primeira entrada (referência). Os metadados das colunas mapeadas devem ser correspondentes.  
  
 **Union All Entrada n**  
 Selecione a partir da lista de colunas de entrada disponíveis na segunda entrada e adicionais. Os metadados das colunas mapeadas devem ser correspondentes.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Mesclar dados por meio da transformação Unir Tudo](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  
