---
title: "Editor de Destino SQL (p&#225;gina Avan&#231;ado) | Microsoft Docs"
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
  - "sql13.dts.designer.sqlserverdestadapter.advanced.f1"
helpviewer_keywords: 
  - "Editor de Destino SQL"
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Editor de Destino SQL (p&#225;gina Avan&#231;ado)
  Use a página **Avançado** da caixa de diálogo **Editor de Destino SQL** para especificar opções avançadas de inserção em massa.  
  
 Para obter mais informações sobre destino do SQL Server, consulte [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md).  
  
## Opções  
 **Manter identidade**  
 Especifique se a tarefa deve inserir valores em colunas de identidade. O valor padrão dessa propriedade é **False**.  
  
 **Manter nulos**  
 Especifique se a tarefa deve manter valores nulos. O valor padrão dessa propriedade é **False**.  
  
 **Bloqueio de tabela**  
 Especifique se a tabela deve ser bloqueada no carregamento de dados. O valor padrão dessa propriedade é **True**.  
  
 **Verificar restrições**  
 Especifique se a tarefa deve verificar restrições. O valor padrão dessa propriedade é **True**.  
  
 **Acionadores**  
 Especifique se a inserção em massa deve ativar gatilhos em tabelas. O valor padrão dessa propriedade é **False**.  
  
 **Primeira Linha**  
 Especifique a primeira linha a inserir. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades**, no **Editor Avançado** e no modelo de objeto.  
  
 **Última Linha**  
 Especifique a última linha a inserir. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades**, no **Editor Avançado** e no modelo de objeto.  
  
 **Número máximo de erros**  
 Especifique o número máximo de erros permitido antes que a inserção em massa cesse. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades**, no **Editor Avançado** e no modelo de objeto.  
  
 **Tempo Limite**  
 Especifique o tempo limite, em segundos, a ser aguardado antes de interrupção da inserção em massa.  
  
 **Ordenar colunas**  
 Digite os nomes das colunas de classificação. Cada coluna pode ser classificada em ordem crescente ou decrescente. Ao usar várias colunas de classificação, delimite a lista com vírgulas.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destinos SQL &#40;página Gerenciador de Conexões&#41;](../../integration-services/data-flow/sql-destination-editor-connection-manager-page.md)   
 [Editor de Destinos SQL &#40;página Mapeamentos&#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)   
 [Carregar dados em massa por meio do destino do SQL Server](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  