---
title: 'Lição 12: Criar funções | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a2f507e9f22e4d090407b0b0849f69a8e7914e8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469121"
---
# <a name="lesson-11-create-roles"></a>Lição 11: Criar Funções
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará funções. As funções fornecem objeto de banco de dados modelo e segurança de dados, limitando o acesso somente a esses usuários do Windows, que são os membros da função. Cada função é definida com uma única permissão: Nenhum, leitura, leitura e processo, processo ou administrador. As funções podem ser definidas durante a criação de modelo usando o Gerenciador de funções. Depois que um modelo foi implantado, você pode gerenciar funções usando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Funções](../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
> A criação de funções não é necessária para concluir este tutorial. Por padrão, a conta à qual você está conectada no momento terá privilégios de Administrador no modelo. No entanto, para permitir que outros usuários na sua organização procurem o modelo usando um cliente de relatório, você deve criar pelo menos uma função com permissões de ler permissões e adicionar esses usuários como membros.  
  
Você criará três funções:  
  
-   **Gerente de vendas** -essa função pode incluir usuários em sua organização para o qual você deseja ter permissão de leitura para todos os objetos de modelo e dados.  
  
-   **Analista de vendas dos EUA** -essa função pode incluir usuários em sua organização para o qual você deseja apenas ser capaz de procurar dados relacionados a vendas nos Estados Unidos. Para esta função, você usará uma fórmula DAX para definir um *Filtro de Linha*, que restringe os membros procurar somente dados dos Estados Unidos.  
  
-   **Administrador** -essa função pode incluir usuários para o qual você deseja ter a permissão de administrador, que permite acesso ilimitado e permissões para executar tarefas administrativas no banco de dados modelo.  
  
Como o usuário e as contas de grupo do Windows da sua organização são exclusivas, você pode adicionar contas da sua organização específica a membros. Porém, para este tutorial, você também pode deixar os membros em branco. Você ainda poderá testar o efeito de cada função posteriormente na lição 12: Analise no Excel.  
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 10: Criar partições](../analysis-services/lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Criar Funções  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Para criar a função de usuário Gerente de Vendas  
  
1.  No Gerenciador de modelos tabulares, clique com botão direito **funções** > **funções**.  
  
2.  No Gerenciador de função, clique em **New**.  
  
3.  Clique na nova função e, em seguida, na **nome** coluna, renomeie a função para **gerente de vendas**.  
  
4.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Leitura** . 

    ![as-tabular-lesson11-new-role](../analysis-services/media/as-tabular-lesson11-new-role.png) 
  
5.  Opcional: Clique o **membros** guia e, em seguida, clique em **Add**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Para criar a função de usuário Analista de Vendas dos EUA  
  
1.  No Gerenciador de função, clique em **New**.    
  
2.  Renomeie a função para **analista de vendas dos EUA**.  
  
3.  Dê a essa função **leitura** permissão.  
  
4.  Clique na guia filtros de linha e, em seguida, para o **DimGeography** tabela somente, na coluna filtro DAX, digite a seguinte fórmula:  
  
    ```
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Uma fórmula de Filtro de Linha deve resolver para um valor Booliano (TRUE/FALSE). Com esta fórmula, você está especificando que somente as linhas com o valor de código do país região "US" fique visível para o usuário.  
    ![as-tabular-lesson11-role-filter](../analysis-services/media/as-tabular-lesson11-role-filter.png) 
  
6.  Opcional: Clique na guia **Membros** e em **Adicionar**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
#### <a name="to-create-an-administrator-user-role"></a>Para criar uma função de usuário administrador  
  
1.  Clique em **Nova**.  
  
2.  Renomeie a função para **administrador**.  
  
3.  Dê a essa função **administrador** permissão.  
  
4.  Opcional: Clique na guia **Membros** e em **Adicionar**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função. 
  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [Lição 12: Analisar no Excel](../analysis-services/lesson-12-analyze-in-excel.md).

  
  
