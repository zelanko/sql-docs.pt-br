---
title: "Editor da Transforma&#231;&#227;o Pesquisa (p&#225;gina Conex&#227;o) | Microsoft Docs"
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
  - "sql13.dts.designer.lookuptransformation.referencetable.f1"
helpviewer_keywords: 
  - "Editor da Transformação Pesquisa"
ms.assetid: e90d6b69-5a26-43c5-8433-5c3c9588e08c
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Editor da Transforma&#231;&#227;o Pesquisa (p&#225;gina Conex&#227;o)
  Use a página **Conexão** da caixa de diálogo **Editor da Transformação Pesquisa** para selecionar um gerenciador de conexões. Se você selecionar um gerenciador de conexões OLE DB, também poderá selecionar uma consulta, tabela ou exibição para gerar o conjunto de dados de referência.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## Opções  
 As opções a seguir estarão disponíveis quando você selecionar **Cache cheio** e **Gerenciador de conexões de cache** na página Geral da caixa de diálogo **Editor da Transformação Pesquisa**.  
  
 **Gerenciador de conexões do cache**  
 Selecione um gerenciador de conexões de cache existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Editor de Gerenciador de Conexões de Cache**.  
  
 As opções a seguir estarão disponíveis quando você selecionar **Cache cheio**, **Cache parcial** ou **Sem cache** e **Gerenciador de conexões OLE DB** na página Geral da caixa de diálogo **Editor da Transformação Pesquisa**.  
  
 **gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB**.  
  
 **Use uma tabela ou exibição**  
 Selecione uma tabela ou exibição existente na lista ou crie uma nova tabela clicando em **Nova**.  
  
> [!NOTE]  
>  Se você especificar uma instrução SQL na página **Avançado** do **Editor da Transformação Pesquisa**, essa instrução SQL vai sobrescrever e substituir o nome da tabela selecionada aqui. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;Página Avançado&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md).  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela**.  
  
 **Usar resultados de uma consulta SQL**  
 Escolha esta opção para navegar até uma consulta preexistente, criar uma nova consulta, verificar a sintaxe da consulta e visualizar os resultados da consulta.  
  
 **Construir consulta**  
 Crie a instrução Transact-SQL a ser executada usando o **Construtor de Consultas**, uma ferramenta gráfica que é usada para criar consultas navegando pelos dados.  
  
 **Procurar**  
 Use esta opção para navegar até uma consulta preexistente salva como um arquivo.  
  
 **Analisar Consulta**  
 Verifique a sintaxe da consulta.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta**. Esta opção exibe até 200 linhas.  
  
## Recursos externos  
 Entrada de blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## Consulte também  
 [Editor de Transformação Pesquisa &#40;Página Geral&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-general-page.md)   
 [Editor de Transformação Pesquisa &#40;Guia Colunas&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Avançado&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Saída de Erro&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)   
 [Transformação Pesquisa Difusa](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  