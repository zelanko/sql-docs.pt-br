---
title: Alterar a partição DirectQuery (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9df1e66-dd23-41b4-95eb-af110d10eda4
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5c777c0ce70d06b979fbc26ac8f50df1bdbd858d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116031"
---
# <a name="change-the-directquery-partition-ssas-tabular"></a>Alterar a partição DirectQuery (SSAS tabular)
  Como apenas uma partição em uma tabela pode ser designada como a partição DirectQuery, por padrão, o Analysis Services usa a primeira partição criada na tabela. Durante a criação do projeto de modelo, você pode alterar a partição DirectQuery usando a caixa de diálogo Gerenciador de Partições no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para modelos implantados, você pode alterar a partição DirectQuery usando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>Alterar a partição DirectQuery para um projeto de modelo de tabela  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no designer de modelos, clique na tabela (guia) que contém a tabela particionada.  
  
2.  Clique no menu **Tabela** e clique em **Partições**.  
  
3.  No **Gerenciador de Partições**, a partição que é a partição atual Direct Query é indicada pelo prefixo **(DirectQuery)** no nome da partição.  
  
     Selecione outra partição na lista **Partições** e clique em **Definir como DirectQuery**. O botão **Definir como DirectQuery** não é habilitado quando a partição DirectQuery atual é selecionada e não fica visível quando o modelo não está habilitado no modo Direct Query.  
  
4.  Se necessário, altere as opções de processamento e clique em **OK**.  
  
### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>Alterar a partição DirectQuery para um modelo de tabela implantado  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], abra o banco de dados modelo no Pesquisador de Objetos.  
  
2.  Expanda o nó **Tabelas** , clique com o botão direito do mouse na tabela particionada e selecione **Partições**.  
  
     A partição que é designada para uso com o modo DirectQuery tem o prefixo (DirectQuery) no nome da partição.  
  
3.  Para alterar para uma partição diferente, clique no ícone da barra de ferramentas **Direct Query** para abrir a caixa de diálogo **Definir Partição DirectQuery** . O ícone da barra de ferramentas DirectQuery não está disponível em modelos não habilitados para Direct Query.  
  
4.  Escolha outra partição na lista suspensa **Nome da Partição** e altere opções de processamento na partição, caso seja necessário.  
  
## <a name="see-also"></a>Consulte também  
 [Partições &#40;Tabular do SSAS&#41;](tabular-models/partitions-ssas-tabular.md)  
  
  