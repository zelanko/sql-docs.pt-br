---
title: "Editor de Origem ODBC (p&#225;gina Colunas) | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcsource.columns.f1"
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Editor de Origem ODBC (p&#225;gina Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem ODBC** para mapear uma coluna de saída em cada coluna externa (origem).  
  
 Para obter mais informações sobre a origem ODBC, consulte [ODBC Source](../../integration-services/data-flow/odbc-source.md).  
  
## Lista de Tarefas  
 **Para abrir a página Colunas do Editor de Origem ODBC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
2.  Na guia **Fluxo de Dados**, clique duas vezes na fonte ODBC.  
  
3.  No **Editor de Origem ODBC**, clique em **Colunas**.  
  
## Opções  
  
### Colunas Externas Disponíveis  
 A lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas. Selecionar as colunas a serem usadas da origem. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 Marque essa caixa de seleção **Selecionar Tudo** para selecionar todas as colunas.  
  
### Coluna Externa  
 Uma exibição das colunas externas (origem) na ordem em que serão exibidas ao configurar os componentes que consomem os dados da origem ODBC.  
  
### Coluna de Saída  
 Insira um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome inserido é exibido no Designer SSIS.  
  
## Consulte também  
 [Editor de Fonte ODBC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [Editor de Fonte ODBC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  