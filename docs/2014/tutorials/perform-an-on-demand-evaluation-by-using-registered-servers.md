---
title: Executar uma avaliação sob demanda usando servidores registrados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f7deecbab3fceb117bfb3d237cf5940fdc34f5bc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006974"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>Realize uma avaliação sob demanda usando servidores registrados
  Você pode realizar uma avaliação sob demanda de políticas de práticas recomendadas em relação a uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando Servidores Registrados. Você pode usar grupos de servidores locais ou um servidor de gerenciamento central.  
  
> [!NOTE]  
>  Você pode realizar uma avaliação sob demanda de políticas de práticas recomendadas em relação a membros de grupo de servidores que estão executando o [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] ou uma versão posterior do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, você pode receber um erro de exceção se houver algumas propriedades referidas por uma política que não tem suporte no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] ou [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar essa tarefa, você deve configurar um ou mais registros de servidor em Servidores Registrados. Para obter mais informações, consulte os tópicos a seguir:  
  
-   [Criar ou editar um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registrar um servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
-   [Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>Para avaliar políticas de práticas recomendadas em relação a um grupo de servidores  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Servidores Registrados**.  
  
2.  Expanda **mecanismo de banco de dados**e, em seguida, expanda **Local Server Groups**, ou **servidores centrais de gerenciamento**, dependendo de sua configuração.  
  
3.  Execute um destes procedimentos:  
  
    -   Para avaliar as políticas em relação a todos os servidores que são gerenciados pelo grupo de servidores locais ou o servidor de gerenciamento central, clique o nome do grupo de servidor local ou o nome do servidor de gerenciamento central e, em seguida, clique em **avaliar políticas** .  
  
        > [!NOTE]  
        >  Quando você avaliar políticas através de um servidor de gerenciamento central, as políticas não serão avaliadas em relação ao próprio servidor de gerenciamento central.  
  
    -   Para avaliar as políticas em relação a um servidor específico ou um grupo de servidores, expanda **Local Server Groups** ou servidor de gerenciamento central do nome, clique no servidor ou grupo de servidores que você deseja avaliar políticas em relação e, em seguida, clique em **Avaliar políticas**.  
  
4.  No **avaliar políticas** caixa de diálogo, em seguida o **fonte** , clique no botão de reticências (**...** ) botão.  
  
5.  No **Selecionar origem** caixa de diálogo, você pode selecionar o **arquivos** ou **Server** como a origem dos arquivos de política para avaliar. Se você clicar em **Server**, você pode executar uma avaliação sob demanda de quaisquer políticas de práticas recomendadas que foram importados anteriormente para o gerenciamento baseado em políticas em um servidor local ou remoto. Neste tutorial, você clicará em **arquivos**e, em seguida, selecione os arquivos de política individuais que você deseja avaliar. Para fazer isso, siga estas etapas:  
  
    1.  Clique em **arquivos**.  
  
    2.  Ao lado de **arquivos**, clique no botão de reticências (**...** ) botão.  
  
    3.  Selecione um ou mais arquivos de política. XML para avaliar e, em seguida, clique em **abrir**.  
  
         A lista de arquivos selecionadas aparece no **arquivos** caixa.  
  
    4.  No **Selecionar origem** caixa de diálogo, clique em **Okey**.  
  
    5.  Se o **Carregando políticas** caixa de diálogo for exibida, clique em **fechar**.  
  
     As políticas selecionadas são listadas no **seleção de política** página. Observe que um ícone de aviso ao lado de uma política indica que a política contém scripts.  
  
6.  Clique em **avaliar** para avaliar as políticas.  
  
7.  Para algumas falhas de política, o Gerenciamento Baseado em Políticas permite aplicar ações de conformidade com políticas no destino imediatamente. Para esse tipo de falha, uma caixa de seleção será exibida ao lado da política com falha. Se você selecionar a caixa de seleção, ou clique na linha com a política com falha, caixas de seleção aparecer no **detalhes de destino** painel ao lado de instâncias de destino que falharam a avaliação. Se qualquer uma das caixas de seleção for selecionada, o **aplicar** botão fica disponível. Quando você clica em **aplicar**, a configuração de não conformidade será atualizada automaticamente nas instâncias de destino que você selecionou.  
  
    > [!CAUTION]  
    >  Tenha certeza de que você entende a configuração de política perfeitamente antes de atualizar uma instância de destino automaticamente. É recomendável que, depois de selecionar uma ou mais caixas de seleção, você clicar **Script**e escolha um local de saída para que você possa examinar subjacente [!INCLUDE[tsql](../includes/tsql-md.md)] antes de aplicar as alterações de código.  
  
8.  Para exibir os resultados detalhados para uma política, clique na política no **resultados** tabela. O **detalhes de destino** tabela mostra os detalhes para cada instância.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Avalie as políticas de práticas recomendadas de forma agendada](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o gerenciamento baseado em políticas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [Administrar vários servidores usando os Servidores de Gerenciamento Centrais](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  