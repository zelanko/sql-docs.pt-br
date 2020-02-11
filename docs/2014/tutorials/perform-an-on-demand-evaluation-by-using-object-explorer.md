---
title: Executar uma avaliação sob demanda usando o pesquisador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d2aadd055334c7ee64871c2fdfe5239c9849e90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68210940"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>Realize uma avaliação sob demanda usando o Pesquisador de Objetos
  Nesta tarefa, você usará o Pesquisador de Objetos para realizar uma avaliação sob demanda das políticas de práticas recomendadas para o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] em uma única instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Você também pode avaliar políticas em uma única instância através de servidores registrados. Para obter mais informações, consulte [executar uma avaliação sob demanda usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Esta lição baseia-se na versão do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Para executar uma avaliação sob demanda das políticas de práticas recomendadas em relação a instâncias [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]que estão em execução, você deve usar o procedimento no tópico [executar uma avaliação sob demanda usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>Para realizar uma avaliação sob demanda usando o Pesquisador de Objetos  
  
1.  Inicie o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]e conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  No Pesquisador de objetos, expanda **Gerenciamento**, **Gerenciamento de políticas**, clique com o botão direito do mouse em **políticas**e clique em **avaliar**.  
  
    > [!NOTE]  
    >  Por padrão, a instância local é usada como a origem das políticas. Se você importou políticas de práticas recomendadas previamente, elas serão listadas, junto com qualquer outra política que você criou. Você pode selecionar qualquer uma das políticas de práticas recomendadas importadas e, em seguida, clicar em **avaliar**. Se você não importou as políticas de práticas recomendadas, continue com este procedimento.  
  
3.  Na caixa de diálogo **avaliar políticas** , ao lado da caixa **origem** , clique no botão de reticências (**...**).  
  
4.  Na caixa de diálogo **selecionar origem** , você pode selecionar **arquivos** ou **servidor** como a origem dos arquivos de política a serem avaliados. Se você clicar em **servidor**, poderá executar uma avaliação sob demanda de todas as políticas de práticas recomendadas que foram importadas anteriormente para o gerenciamento baseado em políticas em um servidor local ou remoto. Neste tutorial, você clicará em **arquivos**e, em seguida, selecionará os arquivos de política individuais que deseja avaliar. Para fazer isso, siga estas etapas:  
  
    1.  Clique em **arquivos**.  
  
    2.  Ao lado de **arquivos**, clique no botão de reticências (**...**).  
  
    3.  Na caixa de diálogo **selecionar política** , navegue até a seguinte pasta, que contém as políticas de práticas recomendadas:  
  
         **C:\Arquivos de Programas (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  O caminho do arquivo pode variar, dependendo de onde você instalou os arquivos de programa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , do sistema operacional em execução (32 bits ou 64 bits) e do identificador de idioma.  
  
    4.  Selecione um ou mais arquivos de política. XML a serem avaliados e clique em **abrir**.  
  
         A lista de arquivos selecionados aparece na caixa **arquivos** .  
  
    5.  Na caixa de diálogo **selecionar origem** , clique em **OK**.  
  
    6.  Se a caixa de diálogo **carregando políticas** for exibida, clique em **fechar**.  
  
     As políticas que você selecionou são listadas na página **seleção de política** . Observe que um ícone de aviso ao lado de uma política indica que a política contém scripts.  
  
5.  Clique em **avaliar** para avaliar as políticas.  
  
     Na tabela de **resultados** , os resultados de cada política são listados. Um ícone "x" vermelho indica falha na conformidade com a política.  
  
6.  Para algumas falhas de política, o Gerenciamento Baseado em Políticas permite aplicar ações de conformidade com políticas no destino imediatamente. Para esse tipo de falha, uma caixa de seleção será exibida ao lado da política com falha. Se você marcar a caixa de seleção, o botão **aplicar** ficará disponível. Quando você clica em **aplicar**, a configuração não compatível será atualizada automaticamente na instância de destino.  
  
    > [!CAUTION]  
    >  Tenha certeza de que você entende a configuração de política perfeitamente antes de atualizar uma instância de destino automaticamente. Recomendamos que, depois de selecionar uma ou mais caixas de seleção, você clique em **script**e escolha um local de saída para poder examinar o [!INCLUDE[tsql](../includes/tsql-md.md)] código subjacente antes de aplicar as alterações.  
  
7.  Para exibir resultados detalhados de uma política, clique na política na tabela de **resultados** .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Realize uma avaliação sob demanda usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
