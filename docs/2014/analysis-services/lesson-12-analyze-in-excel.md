---
title: 'Lição 13: Analisar no Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8175fee7c1bf1f6472c8e302cf13c418295b9380
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729442"
---
# <a name="lesson-13-analyze-in-excel"></a>Lição 13: Analisar no Excel
  Nesta lição, você usará o recurso Analisar no Excel no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para abrir o Microsoft Excel, criar automaticamente uma conexão de fonte de dados com o workspace modelo e adicionar automaticamente uma Tabela Dinâmica à planilha. O recurso Analisar no Excel foi criado para fornecer um modo rápido e fácil de testar a eficácia do design de modelos antes da sua implantação. Você não executará análises de dados nesta lição. Esta lição visa familiarizar você, o autor modelo, com as ferramentas a serem usadas para testar seu design modelo. Diferente do uso do recurso Analisar no Excel, que se destina a autores do modelo, os usuários finais usarão aplicativos de relatórios cliente como o Excel ou o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] para conectar e procurar dados modelo implantados.  
  
 Para concluir esta lição, o Excel deve ser instalado no mesmo computador como [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Para obter mais informações, consulte [Analisar no Excel &#40;SSAS Tabular&#41;](tabular-models/analyze-in-excel-ssas-tabular.md).  
  
 Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 11: Criar partições](lesson-10-create-partitions.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Procurar usando as perspectivas Padrão e Vendas pela Internet  
 Nestas primeiras tarefas, você procurará seu modelo usando a perspectiva padrão, que inclui todos os objetos de modelo, e também usando a perspectiva de vendas pela Internet que você criou na lição 8: Crie perspectivas. A perspectiva Vendas pela Internet exclui o objeto de tabela Cliente.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para navegar usando a perspectiva Padrão  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , clique em **OK**.  
  
     O Excel será aberto com uma nova pasta de trabalho. Uma conexão da fonte de dados é criada usando a conta de usuário atual e a perspectiva Padrão é usada para definir campos visíveis. Uma Tabela Dinâmica é adicionada automaticamente à planilha.  
  
3.  No Excel, nos **lista de campos da tabela dinâmica**, observe o **data** e **vendas pela Internet** as medidas são exibidas, bem como o **cliente**,  **Data**, **geografia**, **produto**, **categoria de produto**, **subcategoria de produto**e **Vendas pela Internet** tabelas com todas as suas respectivas colunas são exibidas.  
  
4.  Feche o Excel sem salvar a pasta de trabalho.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para navegar usando a perspectiva Vendas pela Internet  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel**, deixe marcada a opção **Usuário do Windows Atual** e, na caixa de listagem suspensa **Perspectiva**, selecione **Vendas pela Internet** e clique em **OK**. O Excel é aberto.  
  
3.  No Excel, na **Lista de Campos da Tabela Dinâmica**, observe que a tabela Customer é excluída da lista de campos.  
  
## <a name="browse-using-roles"></a>Procurar usando funções  
 Funções são parte integrante de qualquer modelo de tabela. Sem pelo menos uma função à qual os usuários são adicionados como membros, os usuários não poderão acessar e analisar dados usando seu modelo. O recurso Analisar no Excel oferece um modo de testar as funções que você definiu.  
  
#### <a name="to-browse-by-using-the-internet-sales-manager-user-role"></a>Para navegar usando a função de usuário Gerente de Vendas pela Internet  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , em **Especificar o nome de usuário ou a função a ser usada para se conectar ao modelo**, selecione **Função**e, na caixa de listagem suspensa, selecione **Gerente de Vendas pela Internet**e clique em **OK**.  
  
     O Excel será aberto com uma nova pasta de trabalho. Uma Tabela Dinâmica é criada automaticamente. A Lista de Campos de Tabela Dinâmica inclui todos os campos de dados disponíveis no novo modelo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 14: Implantar](lesson-13-deploy.md).  
  
  
