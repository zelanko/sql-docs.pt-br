---
title: "Transforma&#231;&#227;o Convers&#227;o de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataconversiontrans.f1"
helpviewer_keywords: 
  - "convertendo tipos de dados [Integration Services]"
  - "transformação Conversão de Dados"
  - "tipos de dados [Integration Services], convertendo"
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
caps.latest.revision: 53
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 53
---
# Transforma&#231;&#227;o Convers&#227;o de Dados
  A transformação Conversão de Dados converte os dados de uma coluna de entrada em um tipo diferente de dados e os copia em uma nova coluna de saída. Por exemplo, um pacote pode extrair dados de várias fontes e usar essa transformação para converter colunas em tipos de dados exigidos pelo armazenamento dos dados de destino. Você pode aplicar várias conversões em uma única coluna de entrada.  
  
 Usando essa transformação, um pacote pode executar os seguintes tipos de conversão de dados:  
  
-   Alterar o tipo de dados. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
    > [!NOTE]  
    >  Se você estiver convertendo dados em um tipo de dados de data ou data/hora, a data na coluna de saída estará no formato ISO, embora a preferência de localidade possa especificar um formato diferente.  
  
-   Defina o comprimento da coluna dos dados da cadeia de caracteres e a precisão e a escala em dados numéricos. Para obter mais informações, consulte [Precisão, escala e comprimento &#40;Transact-SQL&#41;](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
-   Especifique uma página de código. Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
    > [!NOTE]  
    >  Ao copiar entre colunas com um tipo de dados de cadeia de caracteres, as duas colunas devem usar a mesma página de código.  
  
 Se o comprimento de uma coluna de saída de dados de cadeia de caracteres for menor do que o comprimento de sua coluna de entrada correspondente, os dados de saída serão truncados. Para obter mais informações, consulte [Tratamento de erros em dados](../../../integration-services/data-flow/error-handling-in-data.md).  
  
 Essa transformação tem uma entrada, uma saída e uma saída de erro.  
  
## Tarefas relacionadas  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente. Para obter informações sobre como usar a transformação Conversão de Dados no Designer SSIS, consulte [Converter dados em um tipo de dados diferente por meio da transformação Conversão de Dados](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md) e [Editor de Transformação Conversão de Dados](../../../integration-services/data-flow/transformations/data-conversion-transformation-editor.md). Para obter informações sobre como definir as propriedades dessa transformação programaticamente, consulte [Propriedades comuns](../Topic/Common%20Properties.md) e [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## Conteúdo relacionado  
 Entrada de blog, [Comparação de desempenho entre as técnicas de conversão de tipo de dados no SSIS 2008](http://go.microsoft.com/fwlink/?LinkId=220823), em blogs.msdn.com.  
  
## Consulte também  
 [Análise rápida](../Topic/Fast%20Parse.md)   
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  