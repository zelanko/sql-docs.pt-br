---
title: "Editor da Transforma&#231;&#227;o Pesquisa (p&#225;gina Geral) | Microsoft Docs"
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
  - "sql13.dts.designer.lookuptransformation.general.f1"
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Editor da Transforma&#231;&#227;o Pesquisa (p&#225;gina Geral)
  Use a página **Geral** da caixa de diálogo Editor da Transformação Pesquisa para selecionar o modo de cache, selecionar o tipo de conexão e especificar como lidar com as linhas com entradas sem-correspondência.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## Opções  
 **Cache cheio**  
 Gere e carregue o conjunto de dados de referência no cache antes de executar a transformação Pesquisa.  
  
 **Cache parcial**  
 Gere o conjunto de dados de referência durante a execução da transformação Pesquisa. Carregue as linhas com entradas com correspondência no conjunto de dados de referência e as linhas com entradas sem-correspondência no conjunto de dados no cache.  
  
 **Não cache**  
 Gere o conjunto de dados de referência durante a execução da transformação Pesquisa. Nenhum dado é carregado no cache.  
  
 **Gerenciador de conexões do cache**  
 Configure a transformação Pesquisa para usar um Gerenciador de conexão de cache. Esta opção estará disponível somente se a opção Cache cheio for selecionada.  
  
 **gerenciador de conexões OLE DB**  
 Configure a transformação Pesquisa para usar um Gerenciador de conexões OLE DB.  
  
 **Especificar como lidar com linhas com entradas sem-correspondência**  
 Selecione uma opção para lidar com as linhas que não correspondem a pelo menos uma entrada no conjunto de dados de referência.  
  
 Ao selecionar **Redirecionar linhas para uma saída sem-correspondência**, as linhas serão redirecionadas a uma saída sem-correspondência e serão tratadas como erros. A opção **Erro** na página **Saída de Erro** da caixa de diálogo **Editor da Transformação Pesquisa** não estará disponível.  
  
 Ao selecionar uma opção na caixa de listas **Especificar como lidar com linhas com entradas sem-correspondência** , as linhas serão tratadas como erros. A opção **Erro** na página **Saída de Erro** estará disponível.  
  
## Recursos externos  
 Entrada de blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## Consulte também  
 [Gerenciador de conexões de cache](../../../integration-services/data-flow/transformations/cache-connection-manager.md)   
 [Editor de Transformação Pesquisa &#40;Página Conexão&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)   
 [Editor de Transformação Pesquisa &#40;Guia Colunas&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Avançado&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Saída de Erro&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)  
  
  