---
title: "Gerar Script SQL (objetos de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.generatesqlscript.f1"
helpviewer_keywords: 
  - "Caixa de diálogo Gerar Script SQL"
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Gerar Script SQL (objetos de replica&#231;&#227;o)
  Um script de replicação contém os procedimentos armazenados do sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] necessários para implementar os componentes de replicação com scripts, como uma publicação ou assinatura. Todos os componentes de replicação em uma topologia devem ser incluídos no script como parte de um plano de recuperação de desastre  e os scripts também podem ser usados para automatizar tarefas repetitivas. A replicação oferece duas caixas de diálogo para scripts de objetos de replicação:  
  
-   **Gerar Script SQL**, que está disponível no menu de contexto a **replicação** pasta e todas as subpastas em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Essa caixa de diálogo permite script todos os objetos de replicação em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Gerar Script SQL \< ObjectName>**, que está disponível no menu de contexto para publicações e assinaturas. Essa caixa de diálogo permite script de objetos individuais.  
  
 Essas caixas de diálogo fazem scripts de objetos em uma instância única do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; elas não conectam com outras instâncias para script de objetos relacionados.  
  
## Opções Generate SQL Script   
 **Propriedades do Distribuidor**  
 Selecione para script de procedimentos armazenados para: habilitar ou desabilitar o Distribuidor; adicionar ou descartar Publicadores associados com o Distribuidor e criar ou descartar o banco de dados de distribuição.  
  
 **Publicações nestas fontes de dados**  
 Selecione para script de procedimentos armazenados para: habilitar ou desabilitar publicação e criar ou descartar publicações, artigos, assinaturas push e trabalhos de replicação.  
  
 **Publicações nestas fontes de dados**  
 Selecione para escrever um script de procedimentos armazenados para criar ou descartar assinaturas pull e trabalhos de replicação.  
  
 **Para criar ou habilitar os componentes** e **para remover ou desabilitar os componentes**  
 Especifique se o script deve incluir comandos para criação ou remoção de um objeto de replicação. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você use a caixa de diálogo para criar um conjunto de scripts para habilitar e desabilitar componentes.  
  
 **Trabalhos de replicação**  
 Selecione para script de trabalhos de replicação além de chamadas de procedimento armazenado. Essa opção só está disponível ao efetuar script de um Distribuidor.  
  
 Procedimentos armazenados de replicação criam os trabalhos necessários quando são executados, portanto, não é necessário selecionar essa opção. No entanto, pode ser útil ter um registro dos trabalhos criados, caso seja necessário recriar um trabalho individual.  
  
## Gerar Script SQL \< ObjectName> Opções  
 **Para criar ou habilitar os componentes** e **para remover ou desabilitar os componentes**  
 Especifique se o script deve incluir comandos para criação ou remoção de um objeto de replicação. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você use a caixa de diálogo, criando um conjunto de scripts para habilitar e desabilitar componentes.  
  
 **Trabalhos de replicação**  
 Essa opção está disponível somente a partir de **Gerar Script SQL** caixa de diálogo.  
  
## Consulte também  
 [Replicação de script](../../relational-databases/replication/scripting-replication.md)  
  
  