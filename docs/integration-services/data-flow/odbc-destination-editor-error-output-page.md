---
title: "Editor de Destinos ADO NET (p&#225;gina Sa&#237;da de Erro) | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcdest.errorhandling.f1"
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Editor de Destinos ADO NET (p&#225;gina Sa&#237;da de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Destino ODBC** para selecionar as opções para tratamento de erros.  
  
 Para obter mais informações sobre o destino ODBC, consulte [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).  
  
 **Para abrir a página Saída de Erro do Editor de Destino ODBC**  
  
## Lista de Tarefas  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem o destino ODBC.  
  
-   Na guia **Fluxo de Dados**, clique duas vezes no destino ODBC.  
  
-   No **Editor de Destino ODBC**, clique em **Saída de Erro**.  
  
## Opções  
  
### Entrada/Saída  
 Exibe o nome da fonte de dados.  
  
### Coluna  
 Não usado.  
  
### Erro  
 Selecione como o destino ODBC deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
### Truncation  
 Selecione como o destino ODBC deve tratar truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
### Description  
 Exiba uma descrição do erro.  
  
### Definir este valor para células selecionadas  
 Selecione como o destino ODBC trata todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
### Aplicar  
 Aplique as opções de tratamento de erros às células selecionadas.  
  
## Opções de tratamento de erros  
 Você usa as opções a seguir para configurar como o destino ODBC trata erros e truncamentos.  
  
### Falha no Componente  
 A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Esse é o comportamento padrão.  
  
### Ignorar Falha  
 O erro ou o truncamento é ignorado.  
  
### Redirecionar fluxo  
 A linha que está causando o erro ou o truncamento é direcionada para a saída do erro do destino ODBC. Para obter mais informações, consulte Destino ODBC.  
  
## Consulte também  
 [Editor do Destino ODBC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [Editor de Destinos ODBC &#40;Página Mapeamentos&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
  