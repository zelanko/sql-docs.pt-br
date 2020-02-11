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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66822375"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>Realize uma avaliação sob demanda usando servidores registrados

  Você pode realizar uma avaliação sob demanda de políticas de práticas recomendadas em relação a uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando Servidores Registrados. Você pode usar grupos de servidores locais ou um servidor de gerenciamento central.  
  
> [!NOTE]  
>  Você pode realizar uma avaliação sob demanda de políticas de práticas recomendadas em relação a membros de grupo de servidores que estão executando o [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] ou uma versão posterior do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, você pode receber um erro de exceção se houver algumas propriedades referidas por uma política que não tem suporte no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] ou [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar essa tarefa, você deve configurar um ou mais registros de servidor em Servidores Registrados. Para obter mais informações, consulte estes tópicos:  
  
-   [Criar ou editar um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registre um servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
-   [Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>Para avaliar políticas de práticas recomendadas em relação a um grupo de servidores  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Servidores Registrados**.  
  
2.  Expanda **mecanismo de banco de dados**e, em seguida, expanda **grupos de servidores locais**ou **servidores de gerenciamento central**, dependendo de sua configuração.  
  
3.  Execute um destes procedimentos:  
  
    -   Para avaliar as políticas em relação a todos os servidores gerenciados pelo grupo de servidores local ou do servidor de gerenciamento central, clique com o botão direito do mouse no nome do grupo de servidores locais ou no nome do servidor de gerenciamento central e clique em **avaliar políticas**.  
  
        > [!NOTE]  
        >  Quando você avaliar políticas através de um servidor de gerenciamento central, as políticas não serão avaliadas em relação ao próprio servidor de gerenciamento central.  
  
    -   Para avaliar as políticas em relação a um servidor ou grupo de servidores específico, expanda **grupos de servidores locais** ou o nome do servidor de gerenciamento central, clique com o botão direito do mouse no servidor ou grupo de servidores do qual você deseja avaliar políticas e clique em **avaliar políticas**.  
  
4.  Na caixa de diálogo **avaliar políticas** , ao lado da caixa **origem** , clique no botão de reticências (**...**).  
  
5.  Na caixa de diálogo **selecionar origem** , você pode selecionar **arquivos** ou **servidor** como a origem dos arquivos de política a serem avaliados. Se você clicar em **servidor**, poderá executar uma avaliação sob demanda de todas as políticas de práticas recomendadas que foram importadas anteriormente para o gerenciamento baseado em políticas em um servidor local ou remoto. Neste tutorial, você clicará em **arquivos**e, em seguida, selecionará os arquivos de política individuais que deseja avaliar. Para fazer isso, siga estas etapas:  
  
    1.  Clique em **arquivos**.  
  
    2.  Ao lado de **arquivos**, clique no botão de reticências (**...**).  
  
    3.  Selecione um ou mais arquivos de política. XML a serem avaliados e clique em **abrir**.  
  
         A lista de arquivos selecionados aparece na caixa **arquivos** .  
  
    4.  Na caixa de diálogo **selecionar origem** , clique em **OK**.  
  
    5.  Se a caixa de diálogo **carregando políticas** for exibida, clique em **fechar**.  
  
     As políticas que você selecionou são listadas na página **seleção de política** . Observe que um ícone de aviso ao lado de uma política indica que a política contém scripts.  
  
6.  Clique em **avaliar** para avaliar as políticas.  
  
7.  Para algumas falhas de política, o Gerenciamento Baseado em Políticas permite aplicar ações de conformidade com políticas no destino imediatamente. Para esse tipo de falha, uma caixa de seleção será exibida ao lado da política com falha. Se você marcar a caixa de seleção ou clicar na linha com a política com falha, as caixas de seleção aparecerão no painel **detalhes de destino** ao lado das instâncias de destino que falharam na avaliação. Se qualquer uma das caixas de seleção estiver selecionada, o botão **aplicar** ficará disponível. Quando você clica em **aplicar**, a configuração não compatível será atualizada automaticamente nas instâncias de destino que você selecionou.  
  
    > [!CAUTION]  
    >  Tenha certeza de que você entende a configuração de política perfeitamente antes de atualizar uma instância de destino automaticamente. Recomendamos que, depois de selecionar uma ou mais caixas de seleção, você clique em **script**e escolha um local de saída para poder examinar o [!INCLUDE[tsql](../includes/tsql-md.md)] código subjacente antes de aplicar as alterações.  
  
8.  Para exibir resultados detalhados de uma política, clique na política na tabela de **resultados** . A tabela **detalhes de destino** mostra os detalhes de cada instância.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Avalie as políticas de práticas recomendadas de forma agendada](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o gerenciamento baseado em políticas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [Administrar vários servidores usando os Servidores de Gerenciamento Centrais](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
