---
title: Adicionar um grupo de detalhes (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ef8efba-6d48-4aeb-a3b9-a02ba5a44614
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 5aedacebef1f91a7d7f73e6d1da71bf15bfd8cf9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006299"
---
# <a name="add-a-details-group-report-builder-and-ssrs"></a>Adicionar um grupo de detalhes (Construtor de Relatórios e SSRS)
  Os dados de detalhes de um conjunto de dados de relatório são especificados como um grupo sem expressão de grupo. Adicione um grupo de detalhes a uma região de dados tablix existente quando desejar exibir os dados de detalhes para uma matriz. Adicione dados de detalhes novamente que você excluiu de uma tabela ou lista ou para adicionar grupos de detalhes adicionais. Para obter mais informações sobre grupos, consulte [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-details-group-to-a-tablix-data-region"></a>Para adicionar um grupo de detalhes a uma região de dados tablix  
  
1.  Na superfície de design, clique em qualquer lugar em uma região de dados tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas dessa região de dados selecionada.  
  
2.  No painel Agrupamento, clique com o botão direito do mouse em um grupo que seja o grupo filho mais interno. Clique em **Adicionar Grupo**e em **Grupo Filho**. A caixa de diálogo **Grupo Tablix** é aberta.  
  
3.  Em **Expressão de Grupo**, deixe a expressão em branco. Um grupo de detalhes não tem nenhuma expressão.  
  
4.  Selecione **Mostrar dados de detalhes**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Um novo grupo de detalhes é adicionado como um grupo filho ao painel Agrupamento e o identificador da linha do grupo selecionado na etapa 1 exibe o ícone do grupo de detalhes. Para obter mais informações sobre identificadores, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar ou excluir um grupo em uma região de dados &#40;SSRS e construtor de relatórios&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [Noções básicas sobre grupos &#40;SSRS e construtor de relatórios&#41;](understanding-groups-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  