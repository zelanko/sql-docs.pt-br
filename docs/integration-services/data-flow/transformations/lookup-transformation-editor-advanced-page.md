---
title: "Editor da Transforma&#231;&#227;o Pesquisa (p&#225;gina Avan&#231;ado) | Microsoft Docs"
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
  - "sql13.dts.designer.lookuptransformation.advanced.f1"
helpviewer_keywords: 
  - "Editor da Transformação Pesquisa"
ms.assetid: f3395c65-0320-47f9-8d83-daaa082d8713
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# Editor da Transforma&#231;&#227;o Pesquisa (p&#225;gina Avan&#231;ado)
  Use a página **Avançado** da caixa de diálogo **Editor da Transformação Pesquisa** para configurar o cache parcial e para modificar a instrução SQL da transformação Pesquisa.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## Opções  
 **Tamanho de cache (32 bits)**  
 Ajuste o tamanho de cache (em megabytes) para computadores de 32 bits. O valor padrão é 5 megabytes.  
  
 **Tamanho de cache (64 bits)**  
 Ajuste o tamanho de cache (em megabytes) para computadores de 64 bits. O valor padrão é 5 megabytes.  
  
 **Ativar cache para linhas com entradas sem-correspondência**  
 Linhas de cache com entradas sem-correspondência no conjunto de dados de referência.  
  
 **Alocação de cache**  
 Especifique o percentual de cache a ser alocado para as linhas com entradas sem-correspondência no conjunto de dados de referência.  
  
 **Modificar instrução SQL**  
 Modifique a instrução SQL usada para gerar o conjunto de dados de referência.  
  
> [!NOTE]  
>  A instrução SQL opcional especificada nesta página substituirá o nome da tabela especificado na página **Conexão** do **Editor da Transformação Pesquisa**. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;Página Conexão&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md).  
  
 **Definir Parâmetros**  
 Mapeie colunas de entrada para parâmetros usando a caixa de diálogo **Definir Parâmetros da Consulta**.  
  
## Recursos externos  
 Entrada de blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## Consulte também  
 [Editor de Transformação Pesquisa &#40;Página Geral&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-general-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Conexão&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)   
 [Editor de Transformação Pesquisa &#40;Guia Colunas&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Saída de Erro&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)   
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformação Pesquisa Difusa](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  