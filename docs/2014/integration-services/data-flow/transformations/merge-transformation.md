---
title: Transformação Mesclar | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergetrans.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 322caa6b9be17e860afaa1e3526a3590df049820
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790948"
---
# <a name="merge-transformation"></a>Transformação Mesclar
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
 A Transformação Mesclar requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 A Transformação Mesclar também requer que as colunas mescladas em suas entradas tenham metadados coincidentes. Por exemplo, você não pode mesclar uma coluna que tenha um tipo de dados numéricos com uma coluna que tenha um tipo de dados de caracteres. Se os dados tiverem um tipo de dados de cadeia de caracteres, o comprimento da coluna na segunda entrada deve ser menor, ou igual, ao comprimento da coluna na primeira entrada com a qual é intercalado.  
  
 No Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , a interface do usuário para a transformação Mesclar mapeia automaticamente as colunas que contém os mesmos metadados. É possível então mapear manualmente outras colunas que tenham tipos de dados compatíveis.  
  
 Esta transformação tem duas entradas e uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-merge-transformation"></a>Configuração da Transformação Mesclar  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Mesclar** , consulte [Editor de Transformação Mesclar](../../merge-transformation-editor.md).  
  
 Para obter mais informações sobre as propriedades que podem ser definidas programaticamente, clique em um dos tópicos a seguir:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas da transformação](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter detalhes sobre como definir propriedades, consulte os tópicos a seguir:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>Consulte também  
 [Transformação Junção de Mesclagem](merge-join-transformation.md)   
 [Transformação Unir Tudo](union-all-transformation.md)   
 [Fluxo de Dados](../data-flow.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  
