---
title: Adicionar, mover ou excluir uma tabela, matriz ou lista (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4b97c470-cde0-4bb1-a46e-5f5f5553feaa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb60f8152ad49b68723367cfb4f9f3941511954e
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59938922"
---
# <a name="add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs"></a>Adicionar, mover ou excluir uma tabela, matriz ou lista (Construtor de Relatórios e SSRS)
  Uma região de dados exibe dados a partir de um conjunto de dados de relatório. As regiões de dados incluem tabela, matriz, gráfico e medidor. Para aninhar uma região de dados dentro de outra, adicione cada uma separadamente e arraste a região de dados filho para a região de dados pai.  
  
 A maneira mais simples de adicionar uma região de dados de tabela ou matriz a seu relatório é executar o Assistente de Nova Tabela ou Nova Matriz. Esses assistentes o orientarão pelo processo de escolher uma conexão com uma fonte de dados, organizar campos e escolher o layout e o estilo.  
  
> [!NOTE]  
>  O assistente só está disponível no Construtor de Relatórios.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-table-or-matrix-to-a-report-by-using-the-new-table-or-new-matrix-wizard"></a>Para adicionar uma tabela ou matriz a um relatório usando o Assistente de Nova Tabela ou Nova Matriz  
  
1.  Na guia **Inserir** , clique em **Tabela** ou **Matriz**e clique em **Assistente de Tabela** ou **Assistente de Matriz**.  
  
2.  Siga as etapas a **NewTable** ou **nova matriz** assistente.  
  
3.  Na guia **Página Inicial** , clique em **Executar** para visualizar o relatório renderizado.  
  
4.  Na guia **Executar** , clique em **Design** para continuar trabalhando no relatório.  
  
### <a name="to-add-a-data-region"></a>Para adicionar uma região de dados  
  
1.  Na **Faixa de Opções**, no grupo **Regiões de Dados** , clique na região de dados que será adicionada.  
  
2.  Clique na superfície de design e a arraste para criar uma caixa com o tamanho desejado da região de dados.  
  
3.  Arraste um campo do conjunto de dados do relatório do painel de dados do relatório para a célula da região de dados. A região de dados agora está associada aos dados de um conjunto de dados do relatório.  
  
### <a name="to-select-a-data-region"></a>Para selecionar uma região de dados  
  
-   Para uma região de dados de tablix, clique com o botão direito na alça de canto. Em uma região de dados de gráfico ou medidor, clique na região de dados.  
  
     Uma alça de seleção e oito alças de redimensionamento são exibidas.  
  
     Para regiões de dados aninhadas, clique com o botão direito do mouse na região de dados aninhada, clique em **Selecionar**e, em seguida, selecione o item de relatório desejado. Para verificar qual item de relatório está selecionado, use o painel Propriedades. O nome do item selecionado na superfície de design aparece na barra de ferramentas do painel Propriedades.  
  
### <a name="to-move-a-data-region"></a>Para mover uma região de dados  
  
-   Para mover uma região de dados, clique na alça de seleção da região de dados e arraste-a. Use linhas ajustadas para alinhá-las aos itens de relatório existentes.  
  
     Se a régua não estiver visível, clique na guia Exibir e selecione a opção **Régua** .  
  
     Como alternativa, use as teclas de seta para mover a região de dados selecionada na superfície de design.  
  
### <a name="to-delete-a-data-region"></a>Para excluir uma região de dados  
  
-   Selecione a região de dados, clique nela com o botão direito do mouse e, em seguida, clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
