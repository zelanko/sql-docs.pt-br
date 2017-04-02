---
title: "Transforma&#231;&#227;o Importar Coluna | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.importcolumntrans.f1"
helpviewer_keywords: 
  - "Transformação Importar Coluna [Integration Services]"
  - "colunas [Integration Services], importando"
  - "importando dados, pacotes do SSIS"
  - "inserindo dados"
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Transforma&#231;&#227;o Importar Coluna
  A transformação Importar Coluna lê dados em arquivos e adiciona esses dados à colunas em um fluxo de dados. Usando essa transformação, um pacote pode adicionar texto e imagens armazenados em arquivos separados a um fluxo de dados. Por exemplo, um fluxo de dados que carrega dados em uma tabela que armazena informações de produto pode incluir a transformação Importar Coluna para importar revisões de clientes de cada produto a partir de arquivos e adicionar as revisões ao fluxo de dados.  
  
 É possível configurar a transformação Importar Coluna com os seguintes procedimentos:  
  
-   Especificando as colunas às quais a transformação adiciona dados.  
  
-   Especificando se a transformação espera uma marca de ordem de byte (BOM).  
  
    > [!NOTE]  
    >  Uma BOM só será esperada se os dados tiverem o tipo de dados de DT_NTEXT.  
  
 Uma coluna na entrada de transformação contém os nomes de arquivos que mantêm os dados. Cada linha do conjunto de dados pode especificar um arquivo diferente. Quando a transformação Importar Coluna processa uma linha, ela lê o nome de arquivo, abre o arquivo correspondente no sistema de arquivos, e carrega o conteúdo do arquivo em uma coluna de saída. O tipo de dados da coluna de saída deve ser DT_TEXT, DT_NTEXT ou DT_IMAGE. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Essa transformação tem uma entrada, uma saída e uma saída de erro.  
  
## Configuração da transformação Importar Coluna  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Tarefas relacionadas  
 Para obter informações sobre como definir as propriedades deste componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Consulte também  
 [Transformação Exportar Colunas](../../../integration-services/data-flow/transformations/export-column-transformation.md)   
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  