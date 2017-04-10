---
title: "Editor de Origem ADO NET (P&#225;gina Sa&#237;da de Erro) | Microsoft Docs"
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
  - "sql13.dts.designer.adonetsource.erroroutput.f1"
ms.assetid: 4dd9d129-a95c-4d3a-bbbf-e84a39089950
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Editor de Origem ADO NET (P&#225;gina Sa&#237;da de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem ADO NET** para selecionar as opções de manipulação de erros e definir as propriedades nas colunas de saída de erros.  
  
 Para obter mais informações sobre a origem ADO NET, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir a página Saída de Erro**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha a origem ADO NET.  
  
2.  Na guia **Fluxo de Dados**, clique duas vezes na origem ADO NET.  
  
3.  No **Editor de Origem ADO NET**, clique em **Saída de Erro**.  
  
## Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) que você selecionou na página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ADO NET**.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos Relacionados:** [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Description**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## Consulte também  
 [Editor de Origem ADO NET &#40;página Gerenciador de Conexões&#41;](../../integration-services/data-flow/ado-net-source-editor-connection-manager-page.md)   
 [Editor de Origem ADO NET &#40;Página Colunas&#41;](../../integration-services/data-flow/ado-net-source-editor-columns-page.md)   
 [Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)  
  
  