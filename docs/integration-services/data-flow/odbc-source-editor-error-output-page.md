---
title: "Editor de Origem ODBC (p&#225;gina Sa&#237;da de Erro) | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcsource.errorhandling.f1"
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Editor de Origem ODBC (p&#225;gina Sa&#237;da de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem ODBC** para selecionar as opções para tratamento de erros.  
  
 Para obter mais informações sobre a origem ODBC, consulte [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## Lista de Tarefas  
 **Para abrir a página Saída de Erro do Editor de Origem ODBC**  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
-   Na guia **Fluxo de Dados**, clique duas vezes na fonte ODBC.  
  
-   No **Editor de Origem ODBC**, clique em **Saída de Erro**.  
  
## Opções  
  
### Entrada/Saída  
 Exibe o nome da fonte de dados.  
  
### Coluna  
 Não usado.  
  
### Erro  
 Selecione como a origem ODBC deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
### Truncation  
 Selecione como a origem ODBC deve tratar o truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
### Description  
 Não usado.  
  
### Definir este valor para células selecionadas  
 Selecione como a origem ODBC trata todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
### Aplicar  
 Aplique as opções de tratamento de erros às células selecionadas.  
  
## Opções de tratamento de erros  
 Você usa as opções a seguir para configurar como a origem ODBC trata erros e truncamentos.  
  
### Falha no Componente  
 A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Esse é o comportamento padrão.  
  
### Ignorar Falha  
 O erro ou o truncamento é ignorado.  
  
### Redirecionar fluxo  
 A linha que está causando o erro ou o truncamento é direcionada para a saída do erro da origem ODBC. Para obter mais informações, consulte [ODBC Source](../../integration-services/data-flow/odbc-source.md).  
  
## Consulte também  
 [Editor de Fonte ODBC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [Editor de Fonte ODBC &#40;Página Colunas&#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)  
  
  