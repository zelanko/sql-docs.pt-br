---
title: "Lição 13: Analisar no Excel | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c7360a1b13ae19ab6f19e4b6344056a8d9b55d3d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-12-analyze-in-excel"></a>Lição 12: Analisar no Excel
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você usará o analisar no recurso do Excel no SSDT para abrir o Microsoft Excel, criar automaticamente uma conexão de fonte de dados no espaço de trabalho do modelo e adicionar automaticamente uma tabela dinâmica à planilha. O recurso Analisar no Excel foi criado para fornecer um modo rápido e fácil de testar a eficácia do design de modelos antes da sua implantação. Você não executará análises de dados nesta lição. Esta lição visa familiarizar você, o autor modelo, com as ferramentas a serem usadas para testar seu design modelo. Ao contrário de usar o analisar no recurso do Excel, que é destinado para autores de modelo, os usuários finais usarão aplicativos cliente de relatório como Excel ou Power BI para conectar e procurar dados modelo implantados.  
  
Para concluir esta lição, o Excel deve ser instalado no mesmo computador que o SSDT. Para obter mais informações, consulte [Analisar no Excel](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 11: criar funções](../analysis-services/lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Procurar usando as perspectivas Padrão e Vendas pela Internet  
Nestas primeiras tarefas, você procurará seu modelo usando a perspectiva padrão, que inclui todos os objetos de modelo, e também usando a perspectiva de vendas pela Internet você anteriormente. A perspectiva Vendas pela Internet exclui o objeto de tabela Cliente.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para navegar usando a perspectiva Padrão  
  
1.  Clique o **modelo** menu > **analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , clique em **OK**.  
  
    O Excel será aberto com uma nova pasta de trabalho. Uma conexão da fonte de dados é criada usando a conta de usuário atual e a perspectiva Padrão é usada para definir campos visíveis. Uma tabela dinâmica é adicionada automaticamente à planilha.  
  
3.  No Excel, no **lista de campos da tabela dinâmica**, observe o **DimDate** e **FactInternetSales** grupos de medidas são exibidos, bem como a **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, e **FactInternetSales** tabelas com todas as suas respectivas colunas aparecem.  
  
4.  Feche o Excel sem salvar a pasta de trabalho.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para navegar usando a perspectiva Vendas pela Internet  
  
1.  Clique o **modelo** menu e clique **analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , deixe marcada a opção **Usuário do Windows Atual** e, na caixa de listagem suspensa **Perspectiva** , selecione **Vendas pela Internet**e clique em **OK**. 
    
    ![como tabular-lesson12-perspectivas](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  No Excel, na **PivotTable Fields**, observe que a tabela DimCustomer foi excluída da lista de campos.  
    
    ![como tabular-lesson12-campos](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  Feche o Excel sem salvar a pasta de trabalho.  
  
## <a name="browse-by-using-roles"></a>Procurar usando funções  
Funções são parte integrante de qualquer modelo de tabela. Pelo menos uma função à qual os usuários são adicionados como membros, os usuários não poderão acessar e analisar dados usando seu modelo. O recurso Analisar no Excel oferece um modo de testar as funções que você definiu.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Para navegar usando a função de usuário do gerente de vendas  
  
1.  No SSDT, clique no **modelo** menu e clique **analisar no Excel**.  
  
2.  No **analisar no Excel** na caixa **especifique o nome de usuário ou função a ser usada para conectar-se ao modelo**, selecione **função**e, em seguida, na caixa de listagem suspensa, selecione **Gerente de vendas**e, em seguida, clique em **Okey**.  
  
    O Excel será aberto com uma nova pasta de trabalho. Uma tabela dinâmica é criada automaticamente. A Lista de Campos de Tabela Dinâmica inclui todos os campos de dados disponíveis no novo modelo.  
      
3.  Feche o Excel sem salvar a pasta de trabalho.  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 13: implantar](../analysis-services/lesson-13-deploy.md).

  
  
  
