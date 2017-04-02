---
title: "Criar conjuntos nomeados | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "cálculos [Analysis Services], conjuntos nomeados"
  - "conjuntos nomeados [Analysis Services]"
  - "membros [Analysis Services], conjuntos nomeados"
ms.assetid: 03cf97a4-1a18-45f3-acb0-35123bd619be
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 31
---
# Criar conjuntos nomeados
  Um conjunto nomeado é um conjunto de membros ou uma expressão de conjunto que é criado(a) para ser reutilizado(a), por exemplo, em consultas multidimensionais. É possível criar conjuntos nomeados combinando dados de cubo, operadores aritméticos, números e funções. Por exemplo, você pode criar um conjunto nomeado chamado Dez Maiores Fábricas que contém os dez membros da dimensão Fábricas com os valores mais altos para a medida Produção. Os usuários finais podem usar o conjunto Dez Maiores Fábricas em consultas. Por exemplo, um usuário final pode colocar o conjunto Dez Maiores Fábricas em um eixo e a dimensão Medidas, incluindo Produção, em outro. Para obter mais informações, consulte [Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md), e [Criando conjuntos nomeados em MDX &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md).  
  
 Para criar um conjunto nomeado, use o comando **Novo Conjunto Nomeado** da guia **Cálculos** do Designer de Cubo. Esse comando pode ser chamado pelo menu **Cubo** na barra de ferramentas da guia **Cálculos**. Ele exibe um formulário para você especificar as seguintes opções para o conjunto nomeado:  
  
 **Nome**  
 Selecione o nome do conjunto nomeado. Ele aparecerá para os usuários finais quando eles procurarem o cubo.  
  
 **Expressão**  
 Especifique a expressão que produz o conjunto nomeado. Pode ser escrita em MDX. A expressão pode conter uma das seguintes opções:  
  
-   Expressões de dados que representam componentes de cubo, como dimensões, níveis, medidas, etc.  
  
-   Operadores aritméticos.  
  
-   Números.  
  
-   Funções.  
  
 É possível copiar ou arrastar os componentes do cubo da guia **Metadados** no painel **Ferramentas de Cálculo** para a caixa **Expressão** do painel **Editor de Formulário de Conjunto de Nomeado**. É possível copiar ou arrastar as funções da guia **Funções** no painel **Ferramentas de Cálculo** para a caixa **Expressão** do painel **Editor de Formulário de Conjunto de Nomeado**.  
  
> [!IMPORTANT]  
>  Se você criar a expressão de conjunto nomeando explicitamente seus membros, coloque a lista de membros entre chaves ({}).  
  
## Consulte também  
 [Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  