---
title: "Adicionar intelig&#234;ncia de dimens&#227;o a uma dimens&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
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
  - "melhorias de Business Intelligence [Analysis Services], inteligência de dimensão"
  - "dimensões [Analysis Services], melhorias de Business Intelligence"
  - "inteligência de dimensão [Analysis Services]"
  - "propriedade Type"
ms.assetid: b64fa386-eac2-4286-a320-0631a1887aac
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Adicionar intelig&#234;ncia de dimens&#227;o a uma dimens&#227;o
  Adicione o aprimoramento de inteligência de dimensão a um cubo ou uma dimensão para especificar um tipo de negócios padrão para uma dimensão. Esse aprimoramento também especifica os tipos correspondentes para atributos de dimensão. Aplicativos cliente podem usar essas especificações de tipo ao analisar dados.  
  
 Para adicionar inteligência de dimensão, use o Assistente de Business Intelligence e selecione a opção **Definir inteligência de dimensão** na página **Escolher Aprimoramento**. Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar a inteligência de dimensão e identificar os atributos para a dimensão selecionada.  
  
## Selecionando uma dimensão  
 Na primeira página **Definir Opções de Inteligência de Dimensão** do assistente, especifique a dimensão à qual você deseja aplicar a inteligência de dimensão. O aprimoramento de inteligência de dimensão adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
> [!NOTE]  
>  Se você selecionar **Conta** como dimensão, especificará a inteligência de conta para a dimensão. Para obter mais informações, consulte [Adicionar inteligência de conta a uma dimensão](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
## Especificando atributos de dimensão  
 Na página **Definir Inteligência de Dimensão**, na lista **Tipo de Dimensão**, a seleção feita define a propriedade **Tipo** da dimensão. A configuração da propriedade **Tipo** fornece informações aos servidores e aplicativos cliente sobre os conteúdos de uma dimensão. Algumas configurações fornecem apenas orientação para aplicativos cliente; essas configurações são opcionais. Outras configurações, como para Contas ou Tempo, determinam comportamentos específicos e podem ser necessárias para implementar determinados aprimoramentos de business intelligence. Por exemplo, o SQL Server Management Studio usa o tipo de dimensão para identificar uma dimensão Moeda e definir as regras para conversão de moeda apropriadas. A configuração padrão de **Tipo de Dimensão** é **Regular**, o que não faz nenhuma suposição sobre o conteúdo da dimensão.  
  
 Depois de selecionar o tipo de dimensão, em **Atributos da dimensão**, na coluna **Incluir**, marque a caixa de seleção ao lado de cada tipo de atributo padrão para o qual existe um atributo correspondente na dimensão. Por fim, na coluna **Atributo de Dimensão**, expanda a lista suspensa e selecione o atributo da dimensão correspondente ao tipo de atributo selecionado. Selecionar o atributo na lista configura a propriedade **Tipo** dos atributos.  
  
 Por exemplo, convém adicionar inteligência de dimensão a uma dimensão Contas. Em **Tipo de Dimensão**, selecione **Contas**. Em seguida, se a dimensão tiver os atributos **Tipo de Conta** e **Descrição da Conta**, na coluna **Incluir**, marque as caixas de seleção dos tipos de conta **Nome da Conta** e **Tipo de Conta**. Na coluna **Atributo de Dimensão**, associe esses tipos de conta aos atributos **Descrição da Conta** e **Tipo de Conta**, respectivamente, na dimensão.  
  
## Consulte também  
 [Definir cálculos de inteligência de tempo com o Assistente de Business Intelligence](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)  
  
  