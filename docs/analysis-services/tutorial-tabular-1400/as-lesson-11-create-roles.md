---
title: 'Lição do Analysis Services tutorial 11: criar funções | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
ms.openlocfilehash: 8e630d53aed8f722c2de4a21afea8391cefe8bd8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="create-roles"></a>Criar Funções

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você cria funções. As funções fornecem segurança de dados e de objetos de banco de dados de modelo, limitando o acesso somente aos usuários que são membros da função. Cada função é definida com uma permissão única: Nenhum, Leitura, Leitura e Processo, Processo, ou Administrador. Funções podem ser definidas durante a criação do modelo usando o Gerenciador de função. Depois que um modelo tiver sido implantado, você pode gerenciar funções usando o SQL Server Management Studio (SSMS). Para obter mais informações, consulte [funções](../tabular-models/roles-ssas-tabular.md).
  
> [!NOTE]  
> A criação de funções não é necessária para concluir este tutorial. Por padrão, a conta que você está conectado no momento tem privilégios de administrador no modelo. No entanto, para outros usuários na sua organização navegar usando um cliente de relatório, você deve criar pelo menos uma função com leitura permissões e adicione esses usuários como membros.  
  
Você cria três funções:  
  
-   **Gerente de vendas** – essa função pode incluir usuários em sua organização para o qual você deseja ter permissão de leitura para todos os objetos de modelo e dados.  
  
-   **Analista de vendas dos EUA** – essa função pode incluir usuários em sua organização para o qual você deseja apenas ser capaz de procurar dados relacionados a vendas nos Estados Unidos. Para essa função, você deve usar uma fórmula DAX para definir um *filtro de linha*, que restringe os membros para procurar dados apenas para os Estados Unidos.  
  
-   **Administrador** – essa função pode incluir os usuários para o qual você deseja ter a permissão de administrador, que fornece acesso ilimitado e permissões para executar tarefas administrativas no banco de dados modelo.  
  
Como o usuário e as contas de grupo do Windows da sua organização são exclusivas, você pode adicionar contas da sua organização específica a membros. Porém, para este tutorial, você também pode deixar os membros em branco. Testar o efeito de cada função posteriormente na lição 12: analisar no Excel.  
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 10: criar partições](../tutorial-tabular-1400/as-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Criar Funções  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Para criar a função de usuário Gerente de Vendas  
  
1.  No Gerenciador de modelos de tabela, clique com botão direito **funções** > **funções**.  
  
2.  No Gerenciador de função, clique em **novo**.  
  
3.  Clique na nova função e, em seguida, o **nome** coluna, renomeie a função para **gerente de vendas**.  
  
4.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Leitura** . 

    ![as-lesson11-new-role](../tutorial-tabular-1400/media/as-lesson11-new-role.png) 
  
5.  Opcional: Clique o **membros** guia e, em seguida, clique em **adicionar**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Para criar a função de usuário Analista de Vendas dos EUA  
  
1.  No Gerenciador de função, clique em **novo**.    
  
2.  Renomeie a função para **analista de vendas dos EUA**.  
  
3.  Fornecer essa função **leitura** permissão.  
  
4.  Clique na guia filtros de linha e, em seguida, para o **DimGeography** tabela somente na coluna filtro DAX, digite a seguinte fórmula:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Uma fórmula de Filtro de Linha deve resolver para um valor Booliano (TRUE/FALSE). Com essa fórmula, você está especificando que somente as linhas com o valor de código de região de país "US" estão visíveis para o usuário.  
    ![as-lesson11-role-filter](../tutorial-tabular-1400/media/as-lesson11-role-filter.png) 
  
6.  Opcional: Clique o **membros** guia e, em seguida, clique em **adicionar**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
#### <a name="to-create-an-administrator-user-role"></a>Para criar uma função de usuário administrador  
  
1.  Clique em **Nova**.  
  
2.  Renomeie a função para **administrador**.  
  
3.  Fornecer essa função **administrador** permissão.  
  
4.  Opcional: Clique o **membros** guia e, em seguida, clique em **adicionar**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função. 
  
  
## <a name="whats-next"></a>O que vem a seguir?

[Lição 12: Analisar no Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).

  
  
