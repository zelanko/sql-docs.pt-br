---
title: "Pesquisar e substituir | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "diferenciar maiúsculas de minúsculas [SQL Server]"
  - "operações de desfazer"
  - "pesquisas [SQL Server Management Studio]"
  - "substituindo texto "
  - "localização e substituição rápidas [SQL Server Management Studio]"
  - "Editor de Consultas [SQL Server Management Studio], desfazer"
  - "Editor de Consultas [SQL Server Management Studio], pesquisando"
  - "expressões regulares [SQL Server Management Studio]"
  - "localizando texto [SQL Server Management Studio]"
  - "texto [SQL Server], operações de pesquisa e substituição"
  - "localizando [SQL Server Management Studio]"
  - "localizando texto"
  - "Editor de Consultas [SQL Server Management Studio], substituindo texto"
  - "Caixa de diálogo Localizar e Substituir"
  - "opções de curinga [SQL Server Management Studio]"
  - "coincidir palavra inteira [SQL Server]"
  - "pesquisas [SQL Server Management Studio], substituindo"
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Pesquisar e substituir
  Há vários modos diferentes de localizar e substituir texto. No menu **Editar**, **Localizar e Substituir** oferece quatro opções: **Localização Rápida**, **Substituição Rápida**, **Localizar nos Arquivos** ou **Substituir nos Arquivos**. Cada uma dessas opções abre versões da caixa de diálogo **Localizar e Substituir**. Você também pode pesquisar sem uma caixa de diálogo usando teclas de atalho de teclado de pesquisa incremental. Essas técnicas permitem que você controle o escopo de localização e substituição, e escolha o método de revisão de correspondências e substituições.  
  
 Você deve considerar os itens a seguir ao localizar e substituir texto:  
  
-   As opções definidas na caixa de diálogo **Localizar e Substituir** afetam todas as pesquisas. Essas opções incluem **Corresponder Maiúsculas e Minúsculas**, **Coincidir palavra inteira**, **Pesquisar para cima**, **Pesquisar texto oculto**, **Curingas**, **Expressões Regulares**, **Procurar em Todos os Documentos Abertos **e **Procurar no Projeto Atual**. Nem todas as opções estão disponíveis em todas as versões da caixa de diálogo **Localizar e Substituir**.  
  
-   **Desfazer** só está disponível para documentos deixados abertos após uma operação de substituição.  
  
-   **Desfazer** para uma operação **Substituir Tudo** que englobe mais de um arquivo é considerada uma ação única em massa em todos os arquivos afetados. Isto é, você não pode desfazer a alteração em alguns arquivos e mantê-la em outros.  
  
 Em geral, não é possível pesquisar itens com exibições gráficas.  
  
## Consulte também  
 [Pesquisar um documento ativo de forma incremental](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [Pesquisar documentos interativamente](../../relational-databases/scripting/search-documents-interactively.md)   
 [Pesquisar documentos usando listas de resultados](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Pesquisar texto com curingas](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Pesquisar texto com expressões regulares](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  