---
title: Executar uma avaliação sob demanda usando o Pesquisador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 55ca364c60c2b9fcca407561ed195035ce7205fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012401"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>Realize uma avaliação sob demanda usando o Pesquisador de Objetos
  Nesta tarefa, você usará o Pesquisador de Objetos para realizar uma avaliação sob demanda das políticas de práticas recomendadas para o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] em uma única instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Você também pode avaliar políticas em uma única instância através de servidores registrados. Para obter mais informações, consulte [realizar uma avaliação sob demanda usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Esta lição baseia-se na versão do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Para realizar uma avaliação sob demanda de políticas de práticas recomendadas em relação a instâncias que estão executando [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], você deve usar o procedimento no tópico [realizar uma avaliação sob demanda usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>Para realizar uma avaliação sob demanda usando o Pesquisador de Objetos  
  
1.  Inicie o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]e conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  No Pesquisador de objetos, expanda **gerenciamento**, expanda **gerenciamento de política de**, clique com botão direito **políticas**e, em seguida, clique em **avaliar**.  
  
    > [!NOTE]  
    >  Por padrão, a instância local é usada como a origem das políticas. Se você importou políticas de práticas recomendadas previamente, elas serão listadas, junto com qualquer outra política que você criou. Você pode selecionar qualquer uma das políticas de práticas recomendadas importados e, em seguida, clique em **avaliar**. Se você não importou as políticas de práticas recomendadas, continue com este procedimento.  
  
3.  No **avaliar políticas** caixa de diálogo, em seguida o **fonte** , clique no botão de reticências (**...** ) botão.  
  
4.  No **Selecionar origem** caixa de diálogo, você pode selecionar o **arquivos** ou **Server** como a origem dos arquivos de política para avaliar. Se você clicar em **Server**, você pode executar uma avaliação sob demanda de quaisquer políticas de práticas recomendadas que foram importados anteriormente para o gerenciamento baseado em políticas em um servidor local ou remoto. Neste tutorial, você clicará em **arquivos**e, em seguida, selecione os arquivos de política individuais que você deseja avaliar. Para fazer isso, siga estas etapas:  
  
    1.  Clique em **arquivos**.  
  
    2.  Ao lado de **arquivos**, clique no botão de reticências (**...** ) botão.  
  
    3.  No **Selecionar política** caixa de diálogo, navegue até a pasta a seguir, que contém as políticas de práticas recomendadas:  
  
         **C:\Program arquivos (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  O caminho do arquivo pode variar, dependendo de onde você instalou os arquivos de programa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , do sistema operacional em execução (32 bits ou 64 bits) e do identificador de idioma.  
  
    4.  Selecione um ou mais arquivos de política. XML para avaliar e, em seguida, clique em **abrir**.  
  
         A lista de arquivos selecionadas aparece no **arquivos** caixa.  
  
    5.  No **Selecionar origem** caixa de diálogo, clique em **Okey**.  
  
    6.  Se o **Carregando políticas** caixa de diálogo for exibida, clique em **fechar**.  
  
     As políticas selecionadas são listadas no **seleção de política** página. Observe que um ícone de aviso ao lado de uma política indica que a política contém scripts.  
  
5.  Clique em **avaliar** para avaliar as políticas.  
  
     No **resultados** tabela, os resultados para cada política estão listados. Um ícone "x" vermelho indica falha na conformidade com a política.  
  
6.  Para algumas falhas de política, o Gerenciamento Baseado em Políticas permite aplicar ações de conformidade com políticas no destino imediatamente. Para esse tipo de falha, uma caixa de seleção será exibida ao lado da política com falha. Se você selecionar a caixa de seleção, o **aplicar** botão fica disponível. Quando você clica em **aplicar**, a configuração de não conformidade será atualizada automaticamente na instância de destino.  
  
    > [!CAUTION]  
    >  Tenha certeza de que você entende a configuração de política perfeitamente antes de atualizar uma instância de destino automaticamente. É recomendável que, depois de selecionar uma ou mais caixas de seleção, você clicar **Script**e escolha um local de saída para que você possa examinar subjacente [!INCLUDE[tsql](../includes/tsql-md.md)] antes de aplicar as alterações de código.  
  
7.  Para exibir os resultados detalhados para uma política, clique na política no **resultados** tabela.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Realize uma avaliação sob demanda usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  