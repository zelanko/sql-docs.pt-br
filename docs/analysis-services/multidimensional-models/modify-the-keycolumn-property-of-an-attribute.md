---
title: "Modificar a propriedade KeyColumn de um atributo | Microsoft Docs"
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
  - "atributos de associação [Analysis Services]"
  - "atributos [Analysis Services], associação"
  - "colunas da chave [Analysis Services]"
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Modificar a propriedade KeyColumn de um atributo
  Você pode modificar a propriedade **KeyColumns** de um atributo. Por exemplo, convém especificar uma chave composta em vez de uma chave única como a chave para o atributo.  
  
### Para modificar a propriedade KeyColumn de um atributo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto no qual você quer modificar a propriedade **KeyColumns**.  
  
2.  Abra o Designer de Dimensão seguindo um destes procedimentos:  
  
    -   No **Gerenciador de Soluções**, clique com o botão direito do mouse na dimensão na pasta **Dimensões** e, em seguida, clique em **Abrir** ou **Designer de Exibição**.  
  
         — ou —  
  
    -   No Designer de Cubo, na guia **Estrutura do Cubo**, expanda a dimensão do cubo no painel **Dimensões** e clique em **Editar \<dimensão>**.  
  
3.  Na guia **Estrutura da Dimensão**, no painel **Atributos**, clique no atributo cuja propriedade **KeyColumns** você quer modificar.  
  
4.  Na janela **Propriedades**, clique o valor da propriedade **KeyColumns**.  
  
5.  Clique no botão Procurar **(...)** que aparece na célula de valor da caixa de propriedade.  
  
     A caixa de diálogo **Colunas de Chave** é aberta.  
  
6.  Para remover uma coluna de chave existente, na lista **Colunas de Chave**, selecione a coluna e, em seguida, clique no botão **\<**.  
  
7.  Para adicionar uma coluna de chave, na lista **Colunas Disponíveis**, selecione a coluna e clique no botão **>**.  
  
    > [!NOTE]  
    >  Se você definir várias colunas de chave, a ordem de disposição das colunas na lista **Colunas de Chave** vai afetar a ordem de exibição. Por exemplo, um atributo de mês tem duas colunas de chave: mês e ano. Se a coluna de ano aparecer na lista antes da coluna de mês, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fará a classificação por ano e, depois, por mês. Se a coluna de mês aparecer antes da coluna de ano, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fará a classificação por mês e, depois, por ano.  
  
8.  Para alterar a ordem das colunas de chave, selecione uma coluna e clique no botão **Acima** ou **Abaixo**.  
  
## Consulte também  
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  