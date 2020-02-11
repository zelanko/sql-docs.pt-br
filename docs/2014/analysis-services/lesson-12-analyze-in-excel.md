---
title: 'Lição 13: analisar no Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a1564a2b190703e011624162ad4bc25fd5de794
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079187"
---
# <a name="lesson-13-analyze-in-excel"></a>Lição 13: Analisar no Excel
  Nesta lição, você usará o recurso Analisar no Excel no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para abrir o Microsoft Excel, criar automaticamente uma conexão de fonte de dados com o workspace modelo e adicionar automaticamente uma Tabela Dinâmica à planilha. O recurso Analisar no Excel destina-se a fornecer uma maneira rápida e fácil de testar a eficácia do design de modelo antes de implantar seu modelo. Você não executará nenhuma análise de dados nesta lição. O objetivo desta lição é familiarizar você, o autor do modelo, com as ferramentas que você pode usar para testar seu design de modelo. Diferente do uso do recurso Analisar no Excel, que se destina a autores do modelo, os usuários finais usarão aplicativos de relatórios cliente como o Excel ou o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] para conectar e procurar dados modelo implantados.  
  
 Para concluir esta lição, o Excel deve ser instalado no mesmo computador como [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Para obter mais informações, consulte [Analisar no Excel &#40;SSAS Tabular&#41;](tabular-models/analyze-in-excel-ssas-tabular.md).  
  
 Tempo estimado para conclusão desta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 11: Criar partições](lesson-10-create-partitions.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Procurar usando as perspectivas Padrão e Vendas pela Internet  
 Nestas primeiras tarefas, você procurará seu modelo usando a perspectiva padrão, que inclui todos os objetos do modelo, e também a perspectiva Vendas pela Internet que você criou na Lição 8: Criar perspectivas. A perspectiva de vendas pela Internet exclui o objeto de tabela Customer.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para navegar usando a perspectiva Padrão  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel**, clique em **OK**.  
  
     O Excel abrirá uma nova pasta de trabalho. Uma conexão de fonte de dados é criado usando a conta de usuário atual e a perspectiva Padrão é usada para definir campos visíveis. Uma Tabela Dinâmica é adicionada automaticamente à planilha.  
  
3.  No Excel, na **lista de campos da tabela dinâmica**, observe que as medidas de **vendas da Internet** e de **Data** aparecem, bem como as tabelas **cliente**, **Data**, **geografia**, **produto**, **categoria de produto**, **subcategoria de produto**e **vendas pela Internet** com todas as suas respectivas colunas aparecem.  
  
4.  Feche o Excel sem salvar a pasta de trabalho.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para navegar usando a perspectiva de Vendas pela Internet  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel**, deixe **Usuário Atual do Windows** selecionado, em seguida, na caixa de listagem suspensa **Perspectiva**, selecione **Vendas pela Internet** e clique em **OK**. O Excel é aberto.  
  
3.  No Excel, na **Lista de Campos da Tabela Dinâmica**, observe que a tabela Customer é excluída da lista de campos.  
  
## <a name="browse-using-roles"></a>Procurar usando funções  
 Funções são parte integrante de qualquer modelo tabular. Sem pelo menos uma função à qual os usuários são adicionados como membros, os usuários não poderão acessar e analisar dados usando seu modelo. O recurso Analisar no Excel fornece uma maneira de testar as funções definidas por você.  
  
#### <a name="to-browse-by-using-the-internet-sales-manager-user-role"></a>Para navegar usando a função de usuário Gerente de Vendas pela Internet  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , em **Especificar o nome de usuário ou a função a ser usada para se conectar ao modelo**, selecione **Função**e, na caixa de listagem suspensa, selecione **Gerente de Vendas pela Internet**e clique em **OK**.  
  
     O Excel abrirá uma nova pasta de trabalho. Uma Tabela Dinâmica é criada automaticamente. A lista de campos de tabela dinâmica inclui todos os campos de dados disponíveis no novo modelo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 14: Implantar](lesson-13-deploy.md).  
  
  
