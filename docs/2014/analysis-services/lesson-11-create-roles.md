---
title: 'Lição 12: Criar funções | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 7c3b98fbbcbedca2a8bcdbefcd8e41e5d3d5c60b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007616"
---
# <a name="lesson-12-create-roles"></a>Lição 12: Criar funções
  Nesta lição, você criará funções. As funções fornecem objeto de banco de dados modelo e segurança de dados, limitando o acesso somente a esses usuários do Windows, que são os membros da função. Cada função é definida com uma permissão única: Nenhum, Leitura, Leitura e Processo, Processo, ou Administrador. As funções podem ser definidas durante a criação do modelo usando a caixa de diálogo Gerenciador de Funções no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Depois que um modelo foi implantado, você pode gerenciar funções usando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Funções &#40;SSAS Tabular&#41;](tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
>  A criação de funções não é necessária para concluir este tutorial. Por padrão, a conta à qual você está conectada no momento terá privilégios de Administrador no modelo. No entanto, para que outros usuários da organização procurem o modelo usando um aplicativo cliente de relatório, você deve criar pelo menos uma função com permissões Leitura e adicionar esses usuários como membros.  
  
 Você criará três funções:  
  
-   Gerente de Vendas – Essa função pode incluir os usuários da organização na qual você deseja ter a permissão Leitura para todos os dados e objetos de modelo.  
  
-   Analista de Vendas dos EUA – Esta função pode incluir usuários em sua organização para a qual você só deseja ser capaz de procurar dados relacionados a vendas nos EUA (Estados Unidos). Para esta função, você usará uma fórmula DAX para definir um *Filtro de Linha*, que restringe os membros procurar somente dados dos Estados Unidos.  
  
-   Administrador – Essa função pode incluir os usuários para os quais você deseja ter a permissão Administrador, que fornece acesso ilimitado e permissões para executar tarefas administrativas no banco de dados modelo.  
  
 Como o usuário e as contas de grupo do Windows da sua organização são exclusivas, você pode adicionar contas da sua organização específica a membros. Porém, para este tutorial, você também pode deixar os membros em branco. Você ainda poderá testar o efeito de cada função posteriormente na Lição 12: Analisar no Excel.  
  
 Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 11: Criar partições](lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Criar Funções  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Para criar a função de usuário Gerente de Vendas  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Funções**.  
  
2.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
     Uma nova função com a permissão Nenhum é adicionada à lista.  
  
3.  Clique na nova função e, em seguida, no **nome** coluna, renomeie a função para `Internet Sales Manager`.  
  
4.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Leitura** .  
  
5.  Opcional: Clique na guia **Membros** e em **Adicionar**.  
  
6.  Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
7.  Verifique as seleções e clique em **OK**  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Para criar a função de usuário Analista de Vendas dos EUA  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Funções**.  
  
2.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
     Uma nova função com a permissão Nenhum é adicionada à lista.  
  
3.  Clique na nova função e, em seguida, no **nome** coluna, renomeie a função para `Internet Sales US`.  
  
4.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Leitura** .  
  
5.  Clique na guia Filtros de Linha e somente para a tabela **Geografia** , na coluna Filtro DAX, digite a seguinte fórmula:  
  
     `=Geography[Country Region Code] = "US"`  
  
     Uma fórmula de Filtro de Linha deve resolver para um valor Booliano (TRUE/FALSE). Com esta fórmula, você está especificando que somente linhas com o valor Country Region Code de "US" estão visíveis ao usuário.  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
6.  Opcional: Clique na guia **Membros** e em **Adicionar**.  
  
7.  Na caixa de diálogo **Selecionar Usuários ou Grupos** , insira os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
8.  Verifique as seleções e clique em **OK**  
  
#### <a name="to-create-an-administrator-role"></a>Para criar uma função de Administrador  
  
1.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
2.  Clique na nova função e, em seguida, no **nome** coluna, renomeie a função para `Internet Sales Administrator`.  
  
3.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Administrador** .  
  
4.  Clique na guia **Membros** e em **Adicionar**.  
  
5.  Opcional: na caixa de diálogo **Selecionar Usuários ou Grupos** , digite os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
6.  Verifique as seleções e clique em **OK**  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 13: Analisar no Excel](lesson-12-analyze-in-excel.md).  
  
  