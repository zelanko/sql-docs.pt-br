---
title: "Transformação junção de mesclagem | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.mergejointrans.f1
- sql13.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 7c3382fb6a61c1362fe10d67a422c0d316a5d663
ms.contentlocale: pt-br
ms.lasthandoff: 08/19/2017

---
# <a name="merge-join-transformation"></a>Transformação Junção de Mesclagem
  A transformação Junção de Mesclagem fornece uma saída que é gerada unindo-se dois conjuntos de dados ordenados que usam uma junção FULL, LEFT ou INNER. Por exemplo, você pode usar uma associação de LEFT para unir uma tabela que inclui informações de produtos com uma tabela que lista o país/região no qual um produto foi fabricado. O resultado é uma tabela que lista todos os produtos e seu país/região de origem.  
  
 Você pode configurar a transformação Junção de Mesclagem das seguintes formas:  
  
-   Especificando se a associação é de FULL, LEFT ou de INNER.  
  
-   Especificando as colunas que a associação utiliza.  
  
-   Especificando se a transformação manipula valores nulos como iguais a outros nulos.  
  
    > [!NOTE]  
    >  Se os valores nulos não forem tratados como valores iguais, a transformação considera valores nulos como faz o Mecanismo de Banco de Dados do SQL Server.  
  
 Esta transformação tem duas entradas e uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="input-requirements"></a>Requisitos de entrada  
 A Transformação Junção de Mesclagem requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## <a name="join-requirements"></a>Requisições de junção  
 A transformação Junção de Mesclagem requer que as colunas unidas tenham metadados compatíveis. Por exemplo, você não pode unir uma coluna que tenha um tipo de dados numérico com uma coluna que tenha um tipo de dados de caracteres. Se os dados tiverem um tipo de dados de cadeia de caracteres, o comprimento da coluna na segunda entrada deve ser menor, ou igual, ao comprimento da coluna na primeira entrada com a qual é intercalado.  
  
## <a name="buffer-throttling"></a>Limitação de buffer  
 Não é mais preciso configurar o valor da propriedade **MaxBuffersPerInput** , pois a Microsoft fez alterações que reduzem o risco de a transformação Junção de Mesclagem consumir memória excessiva. Esse problema algumas vezes ocorria quando as várias entradas da Junção de Mesclagem geravam dados a taxas irregulares.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter mais informações sobre como definir as propriedades dessa transformação, clique em um dos tópicos a seguir:  
  
-   [Estender um conjunto de dados por meio da transformação Junção de Mesclagem](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para transformações de junção de mesclagem e de mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-join-transformation-editor"></a>Editor de Transformação Mesclagem
  Use a caixa de diálogo **Editor de Transformação Mesclar Junção** para especificar o tipo de junção, as colunas de junção e as colunas de saída para mesclar duas entradas combinadas por uma junção.  
  
> [!IMPORTANT]  
>  A Transformação Junção de Mesclagem requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="options"></a>Opções  
 **Tipo de junção**  
 Especifique se você quer usar uma junção interna, externa esquerda ou completa.  
  
 **Trocar Entradas**  
 Troque a ordem entre entradas usando o botão **Trocar Entradas** . Essa seleção pode ser útil com a opção de Junção externa esquerda.  
  
 **Entrada**  
 Para cada coluna que você desejar na saída mesclada, selecione primeiro na lista de entradas disponíveis.  
  
 São exibidas entradas em duas tabelas separadas. Selecione colunas a serem incluídas na saída. Arraste colunas para criar uma junção entre as tabelas. Para excluir uma junção, selecione-a e pressione a tecla DELETE.  
  
 **Coluna de Entrada**  
 Selecione uma coluna a incluir na saída mesclada da lista de colunas disponíveis na entrada selecionada.  
  
 **Alias de Saída**  
 Digite um alias para cada coluna de saída. O padrão é o nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
## <a name="see-also"></a>Consulte também  
 [Transformação de mesclagem](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

