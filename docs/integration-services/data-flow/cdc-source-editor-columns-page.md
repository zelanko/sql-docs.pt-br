---
title: "Editor de Origem CDC (p&#225;gina Colunas) | Microsoft Docs"
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
  - "sql13.ssis.designer.cdcsource.columns.f1"
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Editor de Origem CDC (p&#225;gina Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem CDC** para mapear uma coluna de saída em cada coluna externa (origem).  
  
 Para obter mais informações sobre a origem CDC, consulte [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## Lista de Tarefas  
 **Para abrir a página Colunas do Editor de Origem CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a origem CDC.  
  
2.  Na guia **Fluxo de Dados**, clique duas vezes na origem CDC.  
  
3.  No **Editor de Origem CDC**, clique em **Colunas**.  
  
## Opções  
 **Colunas Externas Disponíveis**  
 A lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas. Selecione as colunas a serem usadas na origem. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 **Coluna Externa**  
 Uma exibição das colunas externas (origem) na ordem em que serão exibidas ao configurar os componentes que consomem os dados da origem CDC. Para alterar essa ordem, primeiro limpe as colunas selecionadas na lista **Colunas Externas Disponíveis** e depois selecione colunas externas na lista em uma ordem diferente. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 **Coluna de Saída**  
 Insira um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome inserido é exibido no Designer SSIS.  
  
## Consulte também  
 [Editor de Origem CDC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [Editor de Origem CDC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  