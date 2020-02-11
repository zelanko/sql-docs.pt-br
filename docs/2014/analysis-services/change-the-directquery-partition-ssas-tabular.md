---
title: Alterar a partição DirectQuery (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9df1e66-dd23-41b4-95eb-af110d10eda4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1eb0b6349eac28bbd2abc22b9483ef74edf1bf33
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088188"
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
  
## <a name="see-also"></a>Consulte Também  
 [Partições &#40;SSAS de tabela&#41;](tabular-models/partitions-ssas-tabular.md)  
  
  
