---
title: "Editor da Transforma&#231;&#227;o Pesquisa (p&#225;gina Sa&#237;da de Erro) | Microsoft Docs"
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
  - "sql13.dts.designer.lookuptransformation.erroroutput.f1"
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Editor da Transforma&#231;&#227;o Pesquisa (p&#225;gina Sa&#237;da de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor da Transformação Pesquisa** para especificar as opções de tratamento de erros.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## Opções  
 **Entrada/Saída**  
 Visualize o nome da entrada.  
  
 **Coluna**  
 Não usado.  
  
 **Erro**  
 Especifique que tipo de erro pode ocorrer ao lidar com linhas com entradas sem correspondência no conjunto de dados de referência:  
  
-   Ignorar falha e direcionar linhas para uma saída.  
  
-   Redirecionar linhas para uma saída de erro.  
  
-   Falha no componente.  
  
 Esta opção não estará disponível ao selecionar **Redirecionar linhas para uma saída sem-correspondência** na lista **Especificar como lidar com linhas com entradas sem-correspondência** . Essa lista está na página **Geral** da caixa de diálogo **Editor da Transformação Pesquisa** .  
  
 **Tópicos Relacionados:** [Tratamento de erros em dados](../../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorrer um truncamento de dados:  
  
-   Ignorar falha.  
  
-   Redirecionar linha.  
  
-   Falha no componente.  
  
 **Description**  
 Visualize a descrição da operação.  
  
 **Definir células selecionadas com esse valor**  
 Especifique o que deve acontecer com todas as células selecionadas quando ocorrer um erro ou truncamento:  
  
-   Ignorar falha.  
  
-   Redirecionar linha.  
  
-   Falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  