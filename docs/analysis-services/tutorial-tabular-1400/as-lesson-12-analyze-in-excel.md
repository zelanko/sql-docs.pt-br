---
title: 'Lição tutorial do Analysis Services 12: analisar no Excel | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d215045f87ed780a4adc97f9ae4fed9ac7e6991a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="analyze-in-excel"></a>Analisar no Excel

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você usa o recurso analisar no Excel para abrir o Microsoft Excel, criar automaticamente uma conexão para o espaço de trabalho do modelo e adicionar automaticamente uma tabela dinâmica à planilha. O recurso Analisar no Excel foi criado para fornecer um modo rápido e fácil de testar a eficácia do design de modelos antes da sua implantação. Você não executar análises de dados nesta lição. Esta lição visa familiarizar você, o autor modelo, com as ferramentas a serem usadas para testar seu design modelo.   
  
Para concluir esta lição, o Excel deve ser instalado no mesmo computador que o Visual Studio.
  
Tempo estimado para concluir esta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 11: criar funções](../tutorial-tabular-1400/as-lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Procurar usando as perspectivas Padrão e Vendas pela Internet  

Nestas primeiras tarefas, procurar seu modelo usando a perspectiva padrão, que inclui todos os objetos de modelo, e também usando a perspectiva de vendas pela Internet você anteriormente. A perspectiva Vendas pela Internet exclui o objeto de tabela Cliente.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para navegar usando a perspectiva Padrão  
  
1.  Clique o **modelo** menu > **analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , clique em **OK**.  
  
    O Excel abre com uma nova pasta de trabalho. Uma conexão da fonte de dados é criada usando a conta de usuário atual e a perspectiva Padrão é usada para definir campos visíveis. Uma tabela dinâmica é adicionada automaticamente à planilha.  
  
3.  No Excel, no **lista de campos da tabela dinâmica**, observe o **DimDate** e **FactInternetSales** grupos de medidas são exibidos. O **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales** também as tabelas com suas respectivas colunas aparecem.  
  
4.  Feche o Excel sem salvar a pasta de trabalho.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para navegar usando a perspectiva Vendas pela Internet  
  
1.  Clique o **modelo** menu e clique **analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , deixe marcada a opção **Usuário do Windows Atual** e, na caixa de listagem suspensa **Perspectiva** , selecione **Vendas pela Internet**e clique em **OK**. 
    
    ![Perspectiva como lesson12](../tutorial-tabular-1400/media/as-lesson12-perspective.png)
    
3.  No Excel, na **PivotTable Fields**, observe que a tabela DimCustomer foi excluída da lista de campos.  
    
    ![campos como lesson12](../tutorial-tabular-1400/media/as-lesson12-fields.png)
    
4.  Feche o Excel sem salvar a pasta de trabalho.  
  
## <a name="browse-by-using-roles"></a>Procurar usando funções  

Funções são uma parte importante de qualquer modelo de tabela. Pelo menos uma função à qual os usuários são adicionados como membros, os usuários não podem acessar e analisar dados usando o modelo. O recurso Analisar no Excel oferece um modo de testar as funções que você definiu.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Para navegar usando a função de usuário do gerente de vendas  
  
1.  No SSDT, clique no **modelo** menu e clique **analisar no Excel**.  
  
2.  Em **especifique o nome de usuário ou função a ser usada para conectar-se ao modelo**, selecione **função**e, em seguida, na caixa de listagem suspensa, selecione **gerente de vendas**e, em seguida, clique em **Okey**.  
  
    O Excel abre com uma nova pasta de trabalho. Uma tabela dinâmica é criada automaticamente. A lista de campos de tabela dinâmica inclui todos os campos de dados disponíveis no novo modelo.  
      
3.  Feche o Excel sem salvar a pasta de trabalho.  
  
## <a name="whats-next"></a>O que vem a seguir?

Vá para a próxima lição: [lição 13: implantar](../tutorial-tabular-1400/as-lesson-13-deploy.md).

  
  
  
