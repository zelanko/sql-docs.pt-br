---
title: 'Lição 1: Criar um novo projeto de modelo de tabela | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 293b4aa3e1723fa5376e3658e65e4da2104acad4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404808"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Lição 1: Criar um novo projeto de modelo de tabela
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará um novo projeto de modelo de tabela em branco no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Quando seu novo projeto é criado, você pode começar a adicionar dados usando o Assistente de Importação de Tabela. Esta lição fornece uma breve introdução ao ambiente no SSDT de criação de modelos tabulares.  
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico é a primeira lição em um tutorial de criação de modelo de tabela. Para concluir esta lição, você deve ter o banco de dados AdventureWorksDW instalado em uma instância do SQL Server. Para obter mais informações, consulte [modelagem de tabela &#40;Tutorial do Adventure Works&#41;](tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Criar um novo projeto de modelo de tabela  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Para criar um novo projeto de modelo de tabela  
  
1.  No SSDT, sobre o **arquivo** menu, clique em **New** > **projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda **instalado** > **Business Intelligence** > **Analysis Services**e, em seguida, clique em **projeto Tabular do Analysis Services**.  
  
3.  Na **nome**, digite **vendas pela Internet AW**e, em seguida, especifique um local para os arquivos de projeto.  
  
    Por padrão, o **Nome da Solução** será igual ao nome do projeto; no entanto, você poderá digitar outro nome de solução.  
  
4.  Clique em **OK**.  
  
5.  No **designer de modelo Tabular** caixa de diálogo, selecione **espaço de trabalho integrado**.  
  
    O espaço de trabalho hospedará um banco de dados de modelo de tabela com o mesmo nome que o projeto durante a criação do modelo. Espaço de trabalho integrado significa que o SSDT usará uma instância interna, eliminando a necessidade de instalar uma instância de servidor do Analysis Services separada apenas para a criação do modelo. Para obter mais informações, consulte [banco de dados do espaço de trabalho](../tabular-models/workspace-database-ssas-tabular.md).
      
6.  Em **Nível de compatibilidade**, verifique se a opção **SQL Server 2016 (1200)** está selecionada e clique em **OK**.   
 
    ![as-tabular-lesson1-tmd](media/as-tabular-lesson1-tmd.png)
      
    Se você não vir o SQL Server 2016 RTM (1200) na caixa de listagem de nível de compatibilidade, você não estiver usando a versão mais recente do SQL Server Data Tools. Para obter a versão mais recente, consulte [Instalar o SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

    Se você estiver usando a versão mais recente do SSDT, você também pode escolher o SQL Server 2017 (1400). No entanto, a completa lição 13: Implantar, você precisará de um SQL Server 2017 ou o servidor do Azure para implantar.
      
    Selecionar um nível de compatibilidade anterior é recomendado somente se você pretende implantar seu modelo de tabela concluído em uma instância do Analysis Services diferente, executando uma versão anterior do SQL Server. Não há suporte para o espaço de trabalho integrado para níveis de compatibilidade anteriores. Para saber mais, consulte [Nível de compatibilidade](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Noções básicas sobre o modelo de tabela SSDT ambiente de criação  
Agora que você criou um novo projeto de modelo de tabela, vamos explorar o ambiente no SSDT de criação do modelo de tabela.  
  
Depois que o projeto é criado, ele é aberto no SSDT. No lado direito, na **Gerenciador de modelos tabulares**, você verá uma exibição de árvore dos objetos em seu modelo. Uma vez que você ainda não tiver importado dados, as pastas estará vazias. Clique com botão direito uma pasta de objeto para executar ações, semelhantes à barra de menus. Conforme você percorre este tutorial, você usará o Gerenciador de modelos tabulares para navegar por diferentes objetos no seu projeto de modelo.

![as-tabular-lesson1-tme](media/as-tabular-lesson1-tme.png)

Clique o **Gerenciador de soluções** guia. Aqui, você verá sua **Model. BIM** arquivo. Se você não vir a janela do designer para a esquerda (a janela vazia com a guia Model. BIM), em **Gerenciador de soluções**, em **projeto de vendas pela Internet AW**, clique duas vezes o **Model. BIM** arquivo. O arquivo Model. BIM contém todos os metadados para seu projeto de modelo. 

![as-tabular-lesson1-se](media/as-tabular-lesson1-se.png)
  
Vamos examinar as propriedades do modelo. Clique em **Model.bim**. No **propriedades** janela, você verá o [propriedades de modelo](../tabular-models/model-properties-ssas-tabular.md), mais importante do que é o **modo DirectQuery** propriedade. Essa propriedade especifica se o modelo será implantado ou não no modo Na Memória (Desativado) ou no modo DirectQuery (Ativado). Neste tutorial, você criará e implantará o modelo no modo Em Memória.

![as-tabular-lesson1-properties](media/as-tabular-lesson1-properties.png)
  
Quando você cria um novo modelo, determinadas propriedades de modelo são definidas automaticamente acordo com as configurações de modelagem de dados que podem ser especificadas na **ferramentas** > **opções** caixa de diálogo. As propriedades de Backup de Dados, Retenção de Workspace e Servidor de Workspace especificam como e onde o banco de dados de workspace (seu banco de dados de criação de modelo) será submetido a backup, retido na memória e compilado. Você poderá alterar essas configurações posteriormente se necessário, mas, por enquanto, deixe essas propriedades como estão.  

Na **Gerenciador de soluções**, clique com botão direito **vendas pela Internet AW** (projeto) e, em seguida, clique em **propriedades**. O **páginas de propriedades de vendas de Internet do AW** caixa de diálogo é exibida. Esses são os avançados [propriedades do projeto](../tabular-models/project-properties-ssas-tabular.md). Você definirá posteriormente algumas dessas propriedades quando estiver pronto para implantar o modelo.  
  
Quando você instalou o SSDT, vários novos itens de menu foram adicionados ao ambiente do Visual Studio. Examinaremos aqueles específicos para a criação de modelos de tabela. Clique no menu **Modelo** . A partir daqui, você pode iniciar o Assistente de importação de tabela, exibir e editar conexões existentes, atualizar os dados de espaço de trabalho, navegar pelo seu modelo no Excel com o recurso analisar no Excel, criar perspectivas e funções, selecione a exibição do modelo e definir opções de cálculo.  
  
Clique no menu **Tabela** . Aqui, você pode criar e gerenciar relações entre tabelas, criar e gerenciar, especifique configurações de tabela de data, criar partições e editar propriedades de tabela.  
  
Clique no menu **Coluna** . Aqui, você pode adicionar e excluir colunas em uma tabela, congelar colunas e especificar a ordem de classificação. Você também pode usar o recurso AutoSum para criar uma medida de agregação padrão para uma coluna selecionada. Outros botões da barra de ferramentas fornecem acesso rápido a recursos e comandos frequentemente usados.  
  
Explore algumas das caixas de diálogo e locais de vários recursos específicos da criação de modelos de tabela. Embora alguns itens ainda não estejam ativos, você poderá ter uma boa noção do ambiente de criação de modelo de tabela.  


## <a name="additional-resources"></a>Recursos adicionais
Para saber mais sobre os diferentes tipos de projetos de modelo tabular, consulte [projetos de modelo de tabela](../tabular-models/tabular-model-projects-ssas-tabular.md). Para saber mais sobre o ambiente de criação de modelos tabulares, consulte [Designer de modelo de tabela](../tabular-models/tabular-model-designer-ssas.md).  
  

## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [Lição 2: Adicionar dados](lesson-2-add-data.md).

  
  
  
