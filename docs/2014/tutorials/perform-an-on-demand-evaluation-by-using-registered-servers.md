---
title: Executar uma avaliação sob demanda usando servidores registrados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a3a79a6ec655e91264d6fcc00db5a920ad82a21e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822375"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>Realize uma avaliação sob demanda usando servidores registrados

  Você pode realizar uma avaliação sob demanda de políticas de práticas recomendadas em relação a uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando Servidores Registrados. Você pode usar grupos de servidores locais ou um servidor de gerenciamento central.  
  
> [!NOTE]  
>  Você pode realizar uma avaliação sob demanda de políticas de práticas recomendadas em relação a membros de grupo de servidores que estão executando o [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] ou uma versão posterior do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, você pode receber um erro de exceção se houver algumas propriedades referidas por uma política que não tem suporte no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] ou [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar essa tarefa, você deve configurar um ou mais registros de servidor em Servidores Registrados. Para mais informações, consulte os seguintes tópicos:  
  
-   [Criar ou editar um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registrar um servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
-   [Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>Para avaliar políticas de práticas recomendadas em relação a um grupo de servidores  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Servidores Registrados**.  
  
2.  Expandir **mecanismo de banco de dados**e, em seguida, expanda **Local Server Groups**, ou **servidores centrais de gerenciamento**, dependendo de sua configuração.  
  
3.  Execute um destes procedimentos:  
  
    -   Para avaliar as políticas em relação a todos os servidores que são gerenciados pelo grupo de servidores locais ou o servidor de gerenciamento central, clique com botão direito o nome de grupo do servidor local ou o nome do servidor de gerenciamento central e, em seguida, clique em **avaliar políticas** .  
  
        > [!NOTE]  
        >  Quando você avaliar políticas através de um servidor de gerenciamento central, as políticas não serão avaliadas em relação ao próprio servidor de gerenciamento central.  
  
    -   Para avaliar as políticas em relação a um servidor específico ou um grupo de servidores, expanda **grupos de servidores locais** ou o servidor de gerenciamento central de nome, clique com botão direito do servidor ou grupo que você deseja avaliar políticas em relação a e, em seguida, clique em **Avaliar políticas**.  
  
4.  No **avaliar políticas** caixa de diálogo, em seguida o **fonte** , clique no botão de reticências ( **...** ) botão.  
  
5.  No **Selecionar origem** caixa de diálogo, você pode selecionar um **arquivos** ou **Server** como a origem dos arquivos de política para avaliar. Se você clicar **Server**, você pode realizar uma avaliação sob demanda de quaisquer políticas de práticas recomendadas que foram importados anteriormente para o gerenciamento baseado em políticas em um servidor local ou remoto. Neste tutorial, você clicará **arquivos**e, em seguida, selecione os arquivos de política individuais que você deseja avaliar. Para fazer isso, siga estas etapas:  
  
    1.  Clique em **arquivos**.  
  
    2.  Lado **arquivos**, clique no botão de reticências ( **...** ) botão.  
  
    3.  Selecione um ou mais arquivos de política. XML para avaliar e, em seguida, clique em **aberto**.  
  
         A lista de arquivos selecionadas aparece na **arquivos** caixa.  
  
    4.  No **Selecionar origem** caixa de diálogo, clique em **Okey**.  
  
    5.  Se o **Carregando políticas** caixa de diálogo for exibida, clique em **fechar**.  
  
     As políticas que você selecionou são listadas na **seleção de política** página. Observe que um ícone de aviso ao lado de uma política indica que a política contém scripts.  
  
6.  Clique em **Evaluate** para avaliar as políticas.  
  
7.  Para algumas falhas de política, o Gerenciamento Baseado em Políticas permite aplicar ações de conformidade com políticas no destino imediatamente. Para esse tipo de falha, uma caixa de seleção será exibida ao lado da política com falha. Se você selecionar a caixa de seleção, ou clique na linha com a política com falha, caixas de seleção aparecer na **detalhes de destino** painel ao lado de instâncias de destino que falharam a avaliação. Se qualquer uma das caixas de seleção estiver selecionada, o **aplicar** botão fica disponível. Quando você clica em **aplicar**, a configuração de não conformidade será atualizada automaticamente nas instâncias de destino que você selecionou.  
  
    > [!CAUTION]  
    >  Tenha certeza de que você entende a configuração de política perfeitamente antes de atualizar uma instância de destino automaticamente. É recomendável que, depois de selecionar uma ou mais caixas de seleção, você clicar **Script**e escolha um local de saída para que você possa examinar subjacente [!INCLUDE[tsql](../includes/tsql-md.md)] antes de aplicar as alterações de código.  
  
8.  Para exibir os resultados detalhados para uma política, clique na política na **resultados** tabela. O **detalhes de destino** tabela mostra os detalhes para cada instância.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Avaliar as políticas de práticas recomendadas de forma programada](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o gerenciamento baseado em políticas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [Administrar vários servidores usando os Servidores de Gerenciamento Centrais](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
