---
title: Transformação Exportar Colunas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exportcolumntrans.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2914c6a23a326f4d312c2784eaad2b84fdad0b0e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430643"
---
# <a name="export-column-transformation"></a>Transformação Exportar Colunas
  A transformação Exportar Coluna lê dados em um fluxo de dados e os insere em um arquivo. Por exemplo, se o fluxo de dados contiver informações de produtos, como uma imagem de cada produto, você poderá usar a transformação Exportar Coluna para salvar essas imagens em arquivos.  
  
## <a name="append-and-truncate-options"></a>Opções de anexar e truncar  
 A tabela seguinte descreve como as definições das opções anexar e truncar afetam os resultados.  
  
|Acrescentar|Truncate|O arquivo existe|Resultados|  
|------------|--------------|-----------------|-------------|  
|Falso|Falso|Não|A transformação cria um novo arquivo e grava os dados nele.|  
|True|Falso|Não|A transformação cria um novo arquivo e grava os dados nele.|  
|Falso|True|Não|A transformação cria um novo arquivo e grava os dados nele.|  
|True|True|Não|A transformação falha na validação do tempo de design. Ela não é válida para definir ambas as propriedades como `true`.|  
|Falso|Falso|Sim|Ocorre um erro em tempo de execução. O arquivo existe, mas a transformação não pode ser gravada nele.|  
|Falso|True|Sim|A transformação exclui e recria o arquivo e grava os dados nele.|  
|True|Falso|Sim|A transformação abre o arquivo e grava os dados no final do arquivo.|  
|True|True|Sim|A transformação falha na validação do tempo de design. Ela não é válida para definir ambas as propriedades como `true`.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>Configuração da transformação Exportar Coluna  
 Pode-se configurar a transformação Exportar Coluna com os seguintes procedimentos:  
  
-   Especifique as colunas de dados e as colunas que contêm o caminho dos arquivos onde os dados são gravados.  
  
-   Especificar se a operação de inserção de dados anexa ou trunca arquivos existentes.  
  
-   Especificar se uma BOM (marca de ordem de byte) é gravada no arquivo.  
  
    > [!NOTE]  
    >  Uma BOM só é gravada quando os dados não são anexados a um arquivo existente e eles são do tipo DT_NTEXT.  
  
 A transformação usa pares de colunas de entrada; uma coluna contém um nome de arquivo e a outra contém os dados. Cada linha no conjunto de dados pode especificar um arquivo diferente. Como a transformação processa uma linha, os dados são inseridos no arquivo especificado. No tempo de execução, a transformação cria os arquivos caso eles ainda não existam e, posteriormente, grava os dados nos arquivos. Os dados a serem gravados devem ser do tipo DT_TEXT, DT_NTEXT ou DT_IMAGE. Para obter mais informações, consulte [Integration Services Data Types](../integration-services-data-types.md).  
  
 Essa transformação tem uma entrada, uma saída e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Coluna de Exportação**, consulte [Editor de Transformação Colunas de Exportação &#40;Página Colunas&#41;](../../export-column-transformation-editor-columns-page.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas da transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
  
