---
title: 'Lição 12: Analisar no Excel | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c42a45ec20edbde61a2f1b7c5b026f3467cd2371
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468418"
---
# <a name="lesson-12-analyze-in-excel"></a>Lição 12: Analisar no Excel
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você usará o analisar no recurso do Excel no SSDT para abrir o Microsoft Excel, criar automaticamente uma conexão de fonte de dados no espaço de trabalho do modelo e adicionar automaticamente uma tabela dinâmica à planilha. O recurso Analisar no Excel foi criado para fornecer um modo rápido e fácil de testar a eficácia do design de modelos antes da sua implantação. Você não executará análises de dados nesta lição. Esta lição visa familiarizar você, o autor modelo, com as ferramentas a serem usadas para testar seu design modelo. Ao contrário de usar o analisar no recurso do Excel, o que é destinado para autores de modelos, os usuários finais usarão aplicativos cliente de relatório como Excel ou Power BI para conectar e procurar dados de modelo de implantados.  
  
Para concluir esta lição, o Excel deve ser instalado no mesmo computador que o SSDT. Para obter mais informações, consulte [Analisar no Excel](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 11: Criar funções](../analysis-services/lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Procurar usando as perspectivas Padrão e Vendas pela Internet  
Nestas primeiras tarefas, você procurará seu modelo usando a perspectiva padrão, que inclui todos os objetos de modelo, e também usando a perspectiva de vendas pela Internet você viu anteriormente. A perspectiva Vendas pela Internet exclui o objeto de tabela Cliente.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para navegar usando a perspectiva Padrão  
  
1.  Clique o **modelo** menu > **analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , clique em **OK**.  
  
    O Excel será aberto com uma nova pasta de trabalho. Uma conexão da fonte de dados é criada usando a conta de usuário atual e a perspectiva Padrão é usada para definir campos visíveis. Uma tabela dinâmica é adicionada automaticamente à planilha.  
  
3.  No Excel, no **lista de campos da tabela dinâmica**, observe o **DimDate** e **FactInternetSales** grupos de medidas são exibidos, bem como o **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, e **FactInternetSales** tabelas com todas as suas respectivas colunas são exibidas.  
  
4.  Feche o Excel sem salvar a pasta de trabalho.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para navegar usando a perspectiva Vendas pela Internet  
  
1.  Clique o **modelo** menu e clique **analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , deixe marcada a opção **Usuário do Windows Atual** e, na caixa de listagem suspensa **Perspectiva** , selecione **Vendas pela Internet**e clique em **OK**. 
    
    ![as-tabular-lesson12-perspective](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  No Excel, na **PivotTable Fields**, observe que a tabela DimCustomer é excluída da lista de campos.  
    
    ![as-tabular-lesson12-fields](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  Feche o Excel sem salvar a pasta de trabalho.  
  
## <a name="browse-by-using-roles"></a>Navegar usando funções  
Funções são parte integrante de qualquer modelo de tabela. Pelo menos uma função à qual os usuários são adicionados como membros, os usuários não poderão acessar e analisar dados usando seu modelo. O recurso Analisar no Excel oferece um modo de testar as funções que você definiu.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Para navegar usando a função de usuário do gerente de vendas  
  
1.  No SSDT, clique o **modelo** menu e clique **analisar no Excel**.  
  
2.  No **analisar no Excel** na caixa **especifique o nome de usuário ou função a ser usada para se conectar ao modelo**, selecione **função**e, em seguida, na caixa de listagem suspensa, selecione **Gerente de vendas**e, em seguida, clique em **Okey**.  
  
    O Excel será aberto com uma nova pasta de trabalho. Uma tabela dinâmica é criada automaticamente. A Lista de Campos de Tabela Dinâmica inclui todos os campos de dados disponíveis no novo modelo.  
      
3.  Feche o Excel sem salvar a pasta de trabalho.  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [Lição 13: Implantar](../analysis-services/lesson-13-deploy.md).

  
  
  
