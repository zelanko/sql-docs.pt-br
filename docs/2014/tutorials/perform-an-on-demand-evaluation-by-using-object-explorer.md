---
title: Executar uma avaliação sob demanda usando o Pesquisador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: ddb0eeb783f2bdb617ba5c2ac2b18896c23abdcc
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52536559"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>Realize uma avaliação sob demanda usando o Pesquisador de Objetos
  Nesta tarefa, você usará o Pesquisador de Objetos para realizar uma avaliação sob demanda das políticas de práticas recomendadas para o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] em uma única instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Você também pode avaliar políticas em uma única instância através de servidores registrados. Para obter mais informações, consulte [realizar uma avaliação sob demanda por usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Esta lição baseia-se na versão do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Para realizar uma avaliação sob demanda de políticas de práticas recomendadas em relação a instâncias que estão executando [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], você deve usar o procedimento no tópico [realizar uma avaliação sob demanda por usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>Para realizar uma avaliação sob demanda usando o Pesquisador de Objetos  
  
1.  Inicie o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]e conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  No Pesquisador de objetos, expanda **Management**, expanda **gerenciamento de política**, clique com botão direito **políticas**e, em seguida, clique em **Evaluate**.  
  
    > [!NOTE]  
    >  Por padrão, a instância local é usada como a origem das políticas. Se você importou políticas de práticas recomendadas previamente, elas serão listadas, junto com qualquer outra política que você criou. Você pode selecionar qualquer uma das políticas de práticas recomendadas importadas e, em seguida, clique em **Evaluate**. Se você não importou as políticas de práticas recomendadas, continue com este procedimento.  
  
3.  No **avaliar políticas** caixa de diálogo, em seguida o **fonte** , clique no botão de reticências (**...** ) botão.  
  
4.  No **Selecionar origem** caixa de diálogo, você pode selecionar um **arquivos** ou **Server** como a origem dos arquivos de política para avaliar. Se você clicar **Server**, você pode realizar uma avaliação sob demanda de quaisquer políticas de práticas recomendadas que foram importados anteriormente para o gerenciamento baseado em políticas em um servidor local ou remoto. Neste tutorial, você clicará **arquivos**e, em seguida, selecione os arquivos de política individuais que você deseja avaliar. Para fazer isso, siga estas etapas:  
  
    1.  Clique em **arquivos**.  
  
    2.  Lado **arquivos**, clique no botão de reticências (**...** ) botão.  
  
    3.  No **Selecionar política** caixa de diálogo, navegue até a pasta a seguir, que contém as políticas de práticas recomendadas:  
  
         **C:\Program arquivos (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  O caminho do arquivo pode variar, dependendo de onde você instalou os arquivos de programa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , do sistema operacional em execução (32 bits ou 64 bits) e do identificador de idioma.  
  
    4.  Selecione um ou mais arquivos de política. XML para avaliar e, em seguida, clique em **aberto**.  
  
         A lista de arquivos selecionadas aparece na **arquivos** caixa.  
  
    5.  No **Selecionar origem** caixa de diálogo, clique em **Okey**.  
  
    6.  Se o **Carregando políticas** caixa de diálogo for exibida, clique em **fechar**.  
  
     As políticas que você selecionou são listadas na **seleção de política** página. Observe que um ícone de aviso ao lado de uma política indica que a política contém scripts.  
  
5.  Clique em **Evaluate** para avaliar as políticas.  
  
     No **resultados** de tabela, os resultados para cada política estão listados. Um ícone "x" vermelho indica falha na conformidade com a política.  
  
6.  Para algumas falhas de política, o Gerenciamento Baseado em Políticas permite aplicar ações de conformidade com políticas no destino imediatamente. Para esse tipo de falha, uma caixa de seleção será exibida ao lado da política com falha. Se você selecionar a caixa de seleção, o **aplicar** botão fica disponível. Quando você clica em **aplicar**, a configuração de não conformidade será atualizada automaticamente na instância de destino.  
  
    > [!CAUTION]  
    >  Tenha certeza de que você entende a configuração de política perfeitamente antes de atualizar uma instância de destino automaticamente. É recomendável que, depois de selecionar uma ou mais caixas de seleção, você clicar **Script**e escolha um local de saída para que você possa examinar subjacente [!INCLUDE[tsql](../includes/tsql-md.md)] antes de aplicar as alterações de código.  
  
7.  Para exibir os resultados detalhados para uma política, clique na política na **resultados** tabela.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Realize uma avaliação sob demanda usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
