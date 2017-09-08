---
title: "Lição 12: Criar funções | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 659b8bb8af4d759367d81bb3e8828360fd2b1f28
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-11-create-roles"></a>Lição 11: Criar funções
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará funções. As funções fornecem objeto de banco de dados modelo e segurança de dados, limitando o acesso somente a esses usuários do Windows, que são os membros da função. Cada função é definida com uma permissão única: Nenhum, Leitura, Leitura e Processo, Processo, ou Administrador. Funções podem ser definidas durante a criação do modelo usando o Gerenciador de função. Depois que um modelo foi implantado, você pode gerenciar funções usando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Funções](../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
> A criação de funções não é necessária para concluir este tutorial. Por padrão, a conta à qual você está conectada no momento terá privilégios de Administrador no modelo. No entanto, para permitir que outros usuários na sua organização para procurar o modelo usando um cliente de relatório, você deve criar pelo menos uma função com leitura permissões e adicione esses usuários como membros.  
  
Você criará três funções:  
  
-   **Gerente de vendas** – essa função pode incluir usuários em sua organização para o qual você deseja ter permissão de leitura para todos os objetos de modelo e dados.  
  
-   **Analista de vendas dos EUA** – essa função pode incluir usuários em sua organização para o qual você deseja apenas ser capaz de procurar dados relacionados a vendas nos Estados Unidos. Para esta função, você usará uma fórmula DAX para definir um *Filtro de Linha*, que restringe os membros procurar somente dados dos Estados Unidos.  
  
-   **Administrador** – essa função pode incluir os usuários para o qual você deseja ter a permissão de administrador, que fornece acesso ilimitado e permissões para executar tarefas administrativas no banco de dados modelo.  
  
Como o usuário e as contas de grupo do Windows da sua organização são exclusivas, você pode adicionar contas da sua organização específica a membros. Porém, para este tutorial, você também pode deixar os membros em branco. Você ainda poderá testar o efeito de cada função posteriormente na Lição 12: Analisar no Excel.  
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 10: criar partições](../analysis-services/lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Criar Funções  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Para criar a função de usuário Gerente de Vendas  
  
1.  No Gerenciador de modelos de tabela, clique com botão direito **funções** > **funções**.  
  
2.  No Gerenciador de função, clique em **novo**.  
  
3.  Clique na nova função e, em seguida, no **nome** coluna, renomeie a função para **gerente de vendas**.  
  
4.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Leitura** . 

    ![como tabular-lesson11-novo-função](../analysis-services/media/as-tabular-lesson11-new-role.png) 
  
5.  Opcional: Clique o **membros** guia e, em seguida, clique em **adicionar**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Para criar a função de usuário Analista de Vendas dos EUA  
  
1.  No Gerenciador de função, clique em **novo**.    
  
2.  Renomeie a função para **analista de vendas dos EUA**.  
  
3.  Fornecer essa função **leitura** permissão.  
  
4.  Clique na guia filtros de linha e, em seguida, para o **DimGeography** tabela somente na coluna filtro DAX, digite a seguinte fórmula:  
  
    ```
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Uma fórmula de Filtro de Linha deve resolver para um valor Booliano (TRUE/FALSE). Com esta fórmula, você está especificando que somente linhas com o valor Country Region Code de "US" estão visíveis ao usuário.  
    ![como tabular-lesson11-função-filtro](../analysis-services/media/as-tabular-lesson11-role-filter.png) 
  
6.  Opcional: Clique na guia **Membros** e em **Adicionar**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
#### <a name="to-create-an-administrator-user-role"></a>Para criar uma função de usuário administrador  
  
1.  Clique em **Nova**.  
  
2.  Renomeie a função para **administrador**.  
  
3.  Fornecer essa função **administrador** permissão.  
  
4.  Opcional: Clique na guia **Membros** e em **Adicionar**. Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função. 
  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 12: analisar no Excel](../analysis-services/lesson-12-analyze-in-excel.md).

  
  

