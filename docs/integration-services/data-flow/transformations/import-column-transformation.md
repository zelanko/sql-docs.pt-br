---
title: Importar Transformação de Coluna | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 58534c37ab2ee5d857bcf9ce823b3aa336c1f477
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291364"
---
# <a name="import-column-transformation"></a>Transformação Importar Coluna

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A transformação Importar Coluna lê dados em arquivos e adiciona esses dados à colunas em um fluxo de dados. Usando essa transformação, um pacote pode adicionar texto e imagens armazenados em arquivos separados a um fluxo de dados. Por exemplo, um fluxo de dados que carrega dados em uma tabela que armazena informações de produto pode incluir a transformação Importar Coluna para importar revisões de clientes de cada produto a partir de arquivos e adicionar as revisões ao fluxo de dados.  
  
 É possível configurar a transformação Importar Coluna com os seguintes procedimentos:  
  
-   Especificando as colunas às quais a transformação adiciona dados.  
  
-   Especificando se a transformação espera uma marca de ordem de byte (BOM).  
  
    > [!NOTE]  
    >  Uma BOM só será esperada se os dados tiverem o tipo de dados de DT_NTEXT.  
  
 Uma coluna na entrada de transformação contém os nomes de arquivos que mantêm os dados. Cada linha do conjunto de dados pode especificar um arquivo diferente. Quando a transformação Importar Coluna processa uma linha, ela lê o nome de arquivo, abre o arquivo correspondente no sistema de arquivos, e carrega o conteúdo do arquivo em uma coluna de saída. O tipo de dados da coluna de saída deve ser DT_TEXT, DT_NTEXT ou DT_IMAGE. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Essa transformação tem uma entrada, uma saída e uma saída de erro.  
  
## <a name="configuration-of-the-import-column-transformation"></a>Configuração da transformação Importar Coluna  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades deste componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Transformação Exportar Colunas](../../../integration-services/data-flow/transformations/export-column-transformation.md)   
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
