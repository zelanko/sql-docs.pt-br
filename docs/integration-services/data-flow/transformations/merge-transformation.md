---
title: Transformação Mesclar | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.mergetrans.f1
- sql13.dts.designer.mergetransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a444abac97c69755e234e39a9c6e3ae623af8d89
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919572"
---
# <a name="merge-transformation"></a>Transformação Mesclar

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  A Transformação Mesclagem combina dois conjuntos de dados classificados em um único conjunto de dados. As linhas de cada conjunto de dados estão inseridas na saída com base em valores de suas colunas-chave.  
  
 Incluindo a Transformação Mesclar em um fluxo de dados, você poderá executar as seguintes tarefas:  
  
-   Mesclar dados de duas fontes de dados, tais como tabelas e arquivos.  
  
-   Criar conjuntos de dados complexos aninhando transformações de Mesclar.  
  
-   Volte a mesclar as filas depois de corrigir erros nos dados.  
  
 A Transformação Mesclar é semelhante às transformações do Union All. Use a transformação do Union All em vez da Transformação Mesclar nas situações seguintes:  
  
-   As entradas de transformação não estão ordenadas.  
  
-   A saída combinada não precisa ser classificada.  
  
-   A transformação tem mais de duas entradas.  
  
## <a name="input-requirements"></a>Requisitos de entrada  
 A Transformação Mesclar requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 A Transformação Mesclar também requer que as colunas mescladas em suas entradas tenham metadados coincidentes. Por exemplo, você não pode mesclar uma coluna que tenha um tipo de dados numéricos com uma coluna que tenha um tipo de dados de caracteres. Se os dados tiverem um tipo de dados de cadeia de caracteres, o comprimento da coluna na segunda entrada deve ser menor, ou igual, ao comprimento da coluna na primeira entrada com a qual é intercalado.  
  
 No Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , a interface do usuário para a transformação Mesclar mapeia automaticamente as colunas que contém os mesmos metadados. É possível então mapear manualmente outras colunas que tenham tipos de dados compatíveis.  
  
 Esta transformação tem duas entradas e uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-merge-transformation"></a>Configuração da Transformação Mesclar  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas programaticamente, clique em um dos tópicos a seguir:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter detalhes sobre como definir propriedades, consulte os tópicos a seguir:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-transformation-editor"></a>Editor de Transformação Mesclagem
  Use o **Editor de Transformação Mesclagem** para especificar colunas de dois conjuntos de dados classificados a serem mescladas.  
  
> [!IMPORTANT]  
>  A Transformação Mesclar requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="options"></a>Opções  
 **Nome da Coluna de Saída**  
 Especifique o nome da coluna de saída.  
  
 **Mesclar Entrada 1**  
 Selecione a coluna a mesclar como Mesclar Entrada 1.  
  
 **Mesclar Entrada 2**  
 Selecione a coluna a mesclar como Mesclar Entrada 2.  
  
## <a name="see-also"></a>Consulte Também  
 [Transformação Junção de Mesclagem](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Transformação Unir Tudo](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
