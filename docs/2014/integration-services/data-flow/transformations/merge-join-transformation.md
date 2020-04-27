---
title: Transformação Junção de Mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointrans.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0ef70f4f9d28fc23c0ac0a168447cc1b8867cd27
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62900162"
---
# <a name="merge-join-transformation"></a>Merge Join Transformation
  A transformação Junção de Mesclagem fornece uma saída que é gerada unindo-se dois conjuntos de dados ordenados que usam uma junção FULL, LEFT ou INNER. Por exemplo, você pode usar uma associação de LEFT para unir uma tabela que inclui informações de produtos com uma tabela que lista o país/região no qual um produto foi fabricado. O resultado é uma tabela que lista todos os produtos e seu país/região de origem.  
  
 Você pode configurar a transformação Junção de Mesclagem das seguintes formas:  
  
-   Especificando se a associação é de FULL, LEFT ou de INNER.  
  
-   Especificando as colunas que a associação utiliza.  
  
-   Especificando se a transformação manipula valores nulos como iguais a outros nulos.  
  
    > [!NOTE]  
    >  Se os valores nulos não forem tratados como valores iguais, a transformação considera valores nulos como faz o Mecanismo de Banco de Dados do SQL Server.  
  
 Esta transformação tem duas entradas e uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="input-requirements"></a>Requisitos de entrada  
 A Transformação Junção de Mesclagem requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## <a name="join-requirements"></a>Requisições de junção  
 A transformação Junção de Mesclagem requer que as colunas unidas tenham metadados compatíveis. Por exemplo, você não pode unir uma coluna que tenha um tipo de dados numérico com uma coluna que tenha um tipo de dados de caracteres. Se os dados tiverem um tipo de dados de cadeia de caracteres, o comprimento da coluna na segunda entrada deve ser menor, ou igual, ao comprimento da coluna na primeira entrada com a qual é intercalado.  
  
## <a name="buffer-throttling"></a>Limitação de buffer  
 Não é mais preciso configurar o valor da propriedade `MaxBuffersPerInput`, pois a Microsoft fez alterações que reduzem o risco de a transformação Junção de Mesclagem consumir memória excessiva. Esse problema algumas vezes ocorria quando as várias entradas da Junção de Mesclagem geravam dados a taxas irregulares.  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter mais informações sobre como definir as propriedades dessa transformação, clique em um dos tópicos a seguir:  
  
-   [Estender um conjunto de dados por meio da transformação Junção de Mesclagem](merge-join-transformation.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de transformação junção de mesclagem](../../merge-join-transformation-editor.md)   
 [Transformação Mesclar](merge-transformation.md)   
 [Transformação Union All](union-all-transformation.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  
