---
title: 'Lição 12: criar funções | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec4bad8ef036e8f19ce0a856f3d9c04bafd0e7c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079265"
---
# <a name="lesson-12-create-roles"></a>Lição 12: Criar funções
  Nesta lição, você criará funções. As funções fornecem objeto de banco de dados modelo e segurança de dados, limitando o acesso somente a esses usuários do Windows, que são os membros da função. Cada função é definida com uma única permissão: Nenhum, Leitura, Leitura e Processo, Processo ou Administrador. As funções podem ser definidas durante a criação do modelo usando a caixa de diálogo Gerenciador de Funções no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Depois que um modelo foi implantado, você pode gerenciar funções usando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Funções &#40;SSAS Tabular&#41;](tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Não é necessário criar funções para concluir este tutorial. Por padrão, a conta com a qual você está conectado terá privilégios de Administrador no modelo. No entanto, para que outros usuários da organização procurem o modelo usando um aplicativo cliente de relatório, você deve criar pelo menos uma função com permissões Leitura e adicionar esses usuários como membros.  
  
 Você criará três funções:  
  
-   Gerente de vendas-essa função pode incluir usuários em sua organização para os quais você deseja ter permissão de leitura para todos os objetos de modelo e dados.  
  
-   Analista de vendas dos EUA-essa função pode incluir usuários em sua organização para os quais você deseja apenas procurar dados relacionados a vendas nos EUA (Estados Unidos). Para essa função, você usará uma fórmula DAX para definir um *Filtro de Linha*, que restringe os membros para procurar dados apenas para os Estados Unidos.  
  
-   Administrador – essa função pode incluir os usuários para os quais você deseja ter permissão de administrador, o que permite acesso ilimitado e permissões para executar tarefas administrativas no banco de dados modelo.  
  
 Já que as contas de usuário e de grupo do Windows em sua organização são exclusivas, você pode adicionar contas da sua organização privada para membros. No entanto, para este tutorial, você também pode deixar os membros em branco. Você ainda poderá testar o efeito de cada função posteriormente na Lição 12: Analisar no Excel.  
  
 Tempo estimado para conclusão desta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 11: Criar partições](lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Criar Funções  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Para criar uma função de usuário de Gerente de Vendas  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Funções**.  
  
2.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
     Uma nova função com a permissão Nenhum é adicionada à lista.  
  
3.  Clique na nova função e, na coluna **nome** , renomeie a função como `Internet Sales Manager`.  
  
4.  Na coluna **Permissões**, clique na lista suspensa e, em seguida, selecione a permissão **Leitura**.  
  
5.  Opcional: clique na guia **Membros** e, em seguida, clique em **Adicionar**.  
  
6.  Na caixa de diálogo **Selecionar Usuários ou Grupos**, digite os grupos os usuários do Windows da sua organização que você deseja incluir na função.  
  
7.  Verifique suas seleções e clique em **OK**  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Para criar uma função de usuário de Analista de Vendas dos EUA  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Funções**.  
  
2.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
     Uma nova função com a permissão Nenhum é adicionada à lista.  
  
3.  Clique na nova função e, na coluna **nome** , renomeie a função como `Internet Sales US`.  
  
4.  Na coluna **Permissões**, clique na lista suspensa e, em seguida, selecione a permissão **Leitura**.  
  
5.  Clique na guia Filtros de Linha e somente para a tabela **Geografia** , na coluna Filtro DAX, digite a seguinte fórmula:  
  
     `=Geography[Country Region Code] = "US"`  
  
     Uma fórmula de Filtro de Linha deve ser resolvida para um valor booliano (TRUE/FALSE). Com essa fórmula, você está especificando que somente as linhas com o valor de código do país Region de "US" fiquem visíveis para o usuário.  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
6.  Opcional: clique na guia **Membros** e, em seguida, clique em **Adicionar**.  
  
7.  Na caixa de diálogo **Selecionar Usuários ou Grupos**, digite os grupos os usuários do Windows da sua organização que você deseja incluir na função.  
  
8.  Verifique suas seleções e clique em **OK**  
  
#### <a name="to-create-an-administrator-role"></a>Para criar uma função de Administrador  
  
1.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
2.  Clique na nova função e, na coluna **nome** , renomeie a função como `Internet Sales Administrator`.  
  
3.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Administrador** .  
  
4.  Clique na guia **Membros** e em **Adicionar**.  
  
5.  Opcional: na caixa de diálogo **Selecionar Usuários ou Grupos** , digite os usuários ou grupos do Windows de sua organização a serem incluídos na função.  
  
6.  Verifique suas seleções e clique em **OK**  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 13: Analisar no Excel](lesson-12-analyze-in-excel.md).  
  
  
