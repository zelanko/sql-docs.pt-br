---
title: "Editor de Transforma&#231;&#227;o Convers&#227;o de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataconversiontransformation.f1"
helpviewer_keywords: 
  - "Editor de Transformação Conversão de Dados"
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Editor de Transforma&#231;&#227;o Convers&#227;o de Dados
  Use a caixa de diálogo **Editor de Transformação Conversão de Dados** para selecionar as colunas a converter, selecionar o tipo de dados ao qual converter a coluna e definir atributos de conversão.  
  
> [!NOTE]  
>  A propriedade **FastParse** das colunas de saída da transformação Conversão de Dados não está disponível no **Editor de Transformação Conversão de Dados**, mas pode ser definida por meio do **Editor Avançado**. Para obter mais informações sobre essa propriedade, consulte a seção Transformação Conversão de Dados em [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Para saber mais sobre a transformação Conversão de Dados, consulte [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
## Opções  
 **Colunas de Entrada Disponíveis**  
 Selecione as colunas a converter, utilizando as caixas de seleção. as seleções adicionam colunas de entrada à tabela abaixo.  
  
 **Coluna de Entrada**  
 Selecione colunas a converter na lista de colunas de entrada disponíveis. Suas seleções serão refletidas nas caixas de seleção marcadas acima.  
  
 **Alias de Saída**  
 Digite um alias para cada coluna nova. O padrão é **Copiar de** seguido do nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Tipo de Dados**  
 Selecione na lista um tipo de dados disponível. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Comprimento**  
 Defina o tamanho de coluna para dados de cadeia de caracteres.  
  
 **Precisão**  
 Defina a precisão para dados numéricos.  
  
 **Escala**  
 Defina a escala para dados numéricos.  
  
 **Página de código**  
 Selecione a página de código apropriada para colunas de tipo DT_STR.  
  
 **Configurar saída de erro**  
 Especifique como tratar erros de nível de linha usando a caixa de diálogo [Configurar Saída de Erro](../Topic/Configure%20Error%20Output.md).  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Converter dados em um tipo de dados diferente por meio da transformação Conversão de Dados](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  