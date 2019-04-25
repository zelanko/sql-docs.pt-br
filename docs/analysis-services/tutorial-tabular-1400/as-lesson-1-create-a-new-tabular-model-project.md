---
title: 'Analysis Services lição do tutorial 1: Criar um novo projeto de modelo de tabela | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 52e0b3f317044e25b2004512083fdcaff7a77ecf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62467977"
---
# <a name="create-a-tabular-model-project"></a>Criar um projeto de modelo de tabela

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você usa o Visual Studio com SQL Server Data Tools (SSDT) ou o Visual Studio 2017 com VSIX de projetos do Microsoft Analysis Services para criar um novo projeto de modelo tabular no nível de compatibilidade 1400. Depois que seu novo projeto é criado, você pode começar a adicionar dados e criar seu modelo. Esta lição fornece uma breve introdução ao ambiente no Visual Studio de criação de modelos tabulares.  
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites

Este artigo é a primeira lição em um tutorial de criação de modelo tabular. Para concluir esta lição, existem vários pré-requisitos que você precisa ter no local. Para obter mais informações, consulte [Analysis Services – tutorial da Adventure Works](../tutorial-tabular-1400/as-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Criar um novo projeto de modelo de tabela  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Para criar um novo projeto de modelo de tabela  
  
1.  No Visual Studio, sobre o **arquivo** menu, clique em **New** > **projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda **instalado** > **Business Intelligence** > **Analysis Services**e, em seguida, clique em **projeto Tabular do Analysis Services**.  
  
3.  Na **nome**, digite **vendas pela Internet AW**e, em seguida, especifique um local para os arquivos de projeto.  
  
    Por padrão, **nome da solução** é o mesmo que o nome do projeto; no entanto, você pode digitar outro nome da solução.  
  
4.  Clique em **OK**.  
  
5.  No **designer de modelo Tabular** caixa de diálogo, selecione **espaço de trabalho integrado**.  
  
    O espaço de trabalho hospeda um banco de dados de modelo de tabela com o mesmo nome que o projeto durante a criação do modelo. Espaço de trabalho integrado significa que o Visual Studio usa uma instância interna, eliminando a necessidade de instalar uma instância de servidor do Analysis Services separada apenas para a criação do modelo.
      
6.  Na **nível de compatibilidade**, selecione **SQL Server 2017 / Azure Analysis Services (1400)**.   
 
    ![as-lesson1-tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    Se você não vir o SQL Server 2017 / Azure Analysis Services (1400) na caixa de listagem de nível de compatibilidade, você não estiver usando a versão mais recente do SQL Server Data Tools. Para obter a versão mais recente, consulte [Instalar o SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Noções básicas sobre o modelo de tabela SSDT ambiente de criação  

Agora que você criou um novo projeto de modelo de tabela, vamos explorar o ambiente no Visual Studio de criação do modelo de tabela.  
  
Depois que o projeto é criado, ele é aberto no Visual Studio. No lado direito, na **Gerenciador de modelos tabulares**, ver uma exibição de árvore dos objetos em seu modelo. Uma vez que você ainda não tiver importado dados, as pastas estarão vazias. Clique com botão direito uma pasta de objeto para executar ações, semelhantes à barra de menus. Conforme você percorre este tutorial, você use o Gerenciador de modelos tabulares para navegar por diferentes objetos no seu projeto de modelo.

![as-lesson1-tme](../tutorial-tabular-1400/media/as-lesson1-tme.png)

Clique o **Gerenciador de soluções** guia. Aqui, você verá sua **Model. BIM** arquivo. Se você não vir a janela do designer para a esquerda (a janela vazia com a guia Model. BIM), em **Gerenciador de soluções**, em **projeto de vendas pela Internet AW**, clique duas vezes o **Model. BIM** arquivo. O arquivo Model. BIM contém os metadados para seu projeto de modelo. 

![as-lesson1-se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
Clique em **Model.bim**. No **propriedades** janela, você ver as propriedades do modelo, mais importantes do que é a **o modo DirectQuery** propriedade. Esta propriedade especifica se o modelo é implantado no modo na memória (desativado) ou no modo DirectQuery (ativado). Para este tutorial, você pode cria e implanta o modelo no modo na memória.

![as-lesson1-properties](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
Quando você cria um projeto de modelo, determinadas propriedades de modelo são definidas automaticamente acordo com as configurações de modelagem de dados que podem ser especificadas na **ferramentas** menu > **opções** caixa de diálogo. As propriedades de Backup de Dados, Retenção de Workspace e Servidor de Workspace especificam como e onde o banco de dados de workspace (seu banco de dados de criação de modelo) será submetido a backup, retido na memória e compilado. Você pode alterar essas configurações posteriormente se necessário, mas por enquanto, deixe essas propriedades como estão.  

Na **Gerenciador de soluções**, clique com botão direito **vendas pela Internet AW** (projeto) e, em seguida, clique em **propriedades**. O **páginas de propriedades de vendas de Internet do AW** caixa de diálogo é exibida. Você define algumas dessas propriedades posteriormente quando implantar seu modelo.  
  
Quando você instalou o SSDT, vários novos itens de menu foram adicionados ao ambiente do Visual Studio. Clique o **modelo** menu. A partir daqui, você pode importar dados, atualizar os dados de espaço de trabalho, navegar pelo seu modelo no Excel, criar perspectivas e funções, selecione a exibição do modelo e definir opções de cálculo. Clique o **tabela** menu. A partir daqui, você pode criar e gerenciar relações, especificar configurações de tabela de data, criar partições e editar propriedades da tabela. Se você clicar na **coluna** menu, você pode adicionar e excluir colunas em uma tabela, congelar colunas e especificar ordem de classificação. O SSDT também adiciona alguns botões à barra. Mais útil é o recurso AutoSoma, para criar uma medida de agregação padrão para uma coluna selecionada. Outros botões da barra de ferramentas fornecem acesso rápido a recursos e comandos frequentemente usados.  
  
Explore algumas das caixas de diálogo e locais de vários recursos específicos da criação de modelos de tabela. Embora alguns itens ainda não estiverem ativas, você pode obter uma boa ideia do ambiente de criação de modelos tabulares.  
  

## <a name="whats-next"></a>O que vem a seguir?

[Lição 2: Obter dados](../tutorial-tabular-1400/as-lesson-2-get-data.md).

  
  
  
