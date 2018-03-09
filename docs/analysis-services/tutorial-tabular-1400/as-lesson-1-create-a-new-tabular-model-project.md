---
title: "Lição do Analysis Services tutorial 1: criar um novo projeto de modelo de tabela | Microsoft Docs"
description: Descreve como criar um novo projeto do tutorial do Analysis Services.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: 6b8d24a31ade8fe621ef2a71b932e87c13211451
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="create-a-tabular-model-project"></a>Criar um projeto de modelo de tabela

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você usa o Visual Studio com o SQL Server Data Tools (SSDT) ou o Visual Studio de 2017 com VSIX de projetos do Microsoft Analysis Services para criar um novo projeto de modelo de tabela no nível de compatibilidade 1400. Depois que o novo projeto é criado, você pode começar a adicionar dados e criar seu modelo. Esta lição fornece uma breve introdução ao ambiente do Visual Studio de criação de modelo de tabela.  
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites

Este artigo é a primeira lição em um tutorial de criação de modelo tabular. Para concluir esta lição, existem vários pré-requisitos que você precisa ter in-loco. Para obter mais informações, consulte [Analysis Services – tutorial do Adventure Works](../tutorial-tabular-1400/as-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Criar um novo projeto de modelo de tabela  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Para criar um novo projeto de modelo de tabela  
  
1.  No Visual Studio, no **arquivo** menu, clique em **novo** > **projeto**.  
  
2.  No **novo projeto** caixa de diálogo caixa, expanda **instalado** > **Business Intelligence** > **Analysis Services**e, em seguida, clique em **projeto Tabular do Analysis Services**.  
  
3.  Em **nome**, tipo **de vendas pela Internet AW**e, em seguida, especifique um local para os arquivos de projeto.  
  
    Por padrão, **nome da solução** é o mesmo que o nome do projeto; no entanto, você pode digitar outro nome de solução.  
  
4.  Clique em **OK**.  
  
5.  No **designer de modelo Tabular** caixa de diálogo, selecione **integrado de espaço de trabalho**.  
  
    O espaço de trabalho hospeda um banco de dados de modelo de tabela com o mesmo nome que o projeto durante a criação do modelo. Espaço de trabalho integrado significa que o Visual Studio usa uma instância interna, eliminando a necessidade de instalar uma instância de servidor do Analysis Services separada apenas para a criação do modelo.
      
6.  Em **nível de compatibilidade**, selecione **SQL Server 2017 / Azure Analysis Services (1400)**.   
 
    ![as-lesson1-tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    Se você não vir o SQL Server 2017 / Azure Analysis Services (1400) na caixa de listagem de nível de compatibilidade, você não estiver usando a versão mais recente do SQL Server Data Tools. Para obter a versão mais recente, consulte [Instalar o SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Noções básicas sobre o modelo de tabela do SSDT ambiente de criação  

Agora que você criou um novo projeto de modelo de tabela, vamos explorar o ambiente no Visual Studio de criação do modelo de tabela.  
  
Depois que o projeto é criado, ele é aberto no Visual Studio. No lado direito, em **Gerenciador de modelos de tabela**, verá uma exibição de árvore de objetos em seu modelo. Desde que você ainda não tiver importado dados, as pastas estão vazias. Clique com botão direito uma pasta de objeto para executar ações, semelhantes à barra de menus. Como você percorrer este tutorial, você usar o Gerenciador de modelos de tabela para navegar objetos diferentes em seu projeto de modelo.

![as-lesson1-tme](../tutorial-tabular-1400/media/as-lesson1-tme.png)

Clique o **Solution Explorer** guia. Aqui, você vê seu **Model.bim** arquivo. Se você não vir a janela do designer para a esquerda (a janela vazia com a guia Model.bim), em **Solution Explorer**, em **projeto de vendas da Internet AW**, clique duas vezes o **Model.bim** arquivo. O arquivo Model.bim contém os metadados para o seu projeto de modelo. 

![as-lesson1-se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
Clique em **Model.bim**. No **propriedades** janela, você ver as propriedades do modelo, mais importantes do que é o **o modo DirectQuery** propriedade. Essa propriedade especifica se o modelo é implantado no modo na memória (desativado) ou no modo DirectQuery (ativado). Para este tutorial, você pode cria e implanta o modelo no modo na memória.

![as-lesson1-properties](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
Quando você cria um projeto de modelo, determinadas propriedades de modelo são definidas automaticamente acordo com as configurações de modelagem de dados que podem ser especificadas o **ferramentas** menu > **opções** caixa de diálogo. As propriedades de Backup de Dados, Retenção de Espaço de trabalho e Servidor de Espaço de Trabalho especificam como e onde o banco de dados de espaço de trabalho (seu banco de dados de criação de modelo) será submetido a backup, retido na memória e compilado. Você pode alterar essas configurações posteriormente se necessário, mas por enquanto, deixe essas propriedades como estão.  

Em **Solution Explorer**, clique com botão direito **de vendas pela Internet AW** (projeto) e, em seguida, clique em **propriedades**. O **páginas de propriedades de vendas de Internet AW** caixa de diálogo é exibida. Você definir algumas dessas propriedades posteriormente quando você implanta o modelo.  
  
Quando você tiver instalado o SSDT, vários novos itens de menu foram adicionados ao ambiente do Visual Studio. Clique o **modelo** menu. A partir daqui, você pode importar dados, atualizar dados de espaço de trabalho, procurar seu modelo no Excel, criar perspectivas e funções, selecione o modo de exibição do modelo e definir opções de cálculo. Clique o **tabela** menu. A partir daqui, você pode criar e gerenciar relações, especifique configurações de tabela de data, criar partições e editar propriedades da tabela. Se você clicar no **coluna** menu, você pode adicionar e excluir colunas em uma tabela, congelar colunas e especificar a ordem de classificação. O SSDT também adiciona alguns botões para a barra. Mais útil é o recurso AutoSoma para criar uma medida de agregação padrão para uma coluna selecionada. Outros botões da barra de ferramentas fornecem acesso rápido a recursos e comandos frequentemente usados.  
  
Explore algumas das caixas de diálogo e locais de vários recursos específicos da criação de modelos de tabela. Enquanto alguns itens ainda não estiverem ativas, você pode ter uma boa noção do ambiente de criação de modelo de tabela.  
  

## <a name="whats-next"></a>O que vem a seguir?

[Lição 2: Obter dados](../tutorial-tabular-1400/as-lesson-2-get-data.md).

  
  
  
