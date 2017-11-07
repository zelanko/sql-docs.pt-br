---
title: "Lição 1: Criar um novo projeto de modelo de tabela | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fe2cd5dff362f5db219f5e61071bde8093b45ce5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Lição 1: Criar um novo projeto de modelo de tabela
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará um novo projeto de modelo de tabela em branco no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Quando seu novo projeto é criado, você pode começar a adicionar dados usando o Assistente de Importação de Tabela. Esta lição fornece uma breve introdução ao ambiente no SSDT de criação de modelo de tabela.  
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico é a primeira lição em um tutorial de criação de modelo de tabela. Para concluir esta lição, você deve ter o banco de dados de exemplo AdventureWorksDW instalado em uma instância do SQL Server. Para obter mais informações, consulte [modelagem de tabela &#40; Tutorial do Adventure Works &#41; ](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Criar um novo projeto de modelo de tabela  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Para criar um novo projeto de modelo de tabela  
  
1.  No SSDT, sobre o **arquivo** menu, clique em **novo** > **projeto**.  
  
2.  No **novo projeto** caixa de diálogo caixa, expanda **instalado** > **Business Intelligence** > **Analysis Services**e, em seguida, clique em **projeto Tabular do Analysis Services**.  
  
3.  Em **nome**, tipo **de vendas pela Internet AW**e, em seguida, especifique um local para os arquivos de projeto.  
  
    Por padrão, o **Nome da Solução** será igual ao nome do projeto; no entanto, você poderá digitar outro nome de solução.  
  
4.  Clique em **OK**.  
  
5.  No **designer de modelo Tabular** caixa de diálogo, selecione **integrado de espaço de trabalho**.  
  
    O espaço de trabalho irá hospedar um banco de dados de modelo de tabela com o mesmo nome que o projeto durante a criação do modelo. Espaço de trabalho integrado significa que SSDT usará uma instância interna, eliminando a necessidade de instalar uma instância de servidor do Analysis Services separada apenas para a criação do modelo. Para obter mais informações, consulte [banco de dados do espaço de trabalho](../analysis-services/tabular-models/workspace-database-ssas-tabular.md).
      
6.  Em **Nível de compatibilidade**, verifique se a opção **SQL Server 2016 (1200)** está selecionada e clique em **OK**.   
 
    ![como-tabela-lição 1-tmd](../analysis-services/media/as-tabular-lesson1-tmd.png)
      
    Se você não vir o SQL Server 2016 RTM (1200) na caixa de listagem de nível de compatibilidade, você não estiver usando a versão mais recente do SQL Server Data Tools. Para obter a versão mais recente, consulte [Instalar o SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

    Se você estiver usando a versão mais recente do SSDT, você também pode escolher o SQL Server 2017 (1400). No entanto, para concluir lição 13: implantar, você precisará de um servidor de 2017 do SQL Server ou do Azure para implantar.
      
    Selecionar um nível de compatibilidade anterior é recomendada apenas se você pretende implantar o modelo de tabela concluído para uma instância diferente do Analysis Services executando uma versão anterior do SQL Server. Não há suporte para o espaço de trabalho integrado para níveis de compatibilidade anteriores. Para saber mais, consulte [Nível de compatibilidade](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Noções básicas sobre o modelo de tabela do SSDT ambiente de criação  
Agora que você criou um novo projeto de modelo de tabela, vamos explorar o ambiente no SSDT de criação do modelo de tabela.  
  
Depois que o projeto é criado, ele é aberto no SSDT. No lado direito, em **Gerenciador de modelos de tabela**, você verá uma exibição de árvore de objetos em seu modelo. Desde que você ainda não tiver importado dados, as pastas estará vazias. Clique com botão direito uma pasta de objeto para executar ações, semelhantes à barra de menus. Conforme você percorrer este tutorial, você usará o Gerenciador de modelos de tabela para navegar objetos diferentes em seu projeto de modelo.

![como-tabela-lição 1-tempo](../analysis-services/media/as-tabular-lesson1-tme.png)

Clique o **Solution Explorer** guia. Aqui, você verá seu **Model.bim** arquivo. Se você não vir a janela do designer para a esquerda (a janela vazia com a guia Model.bim), em **Solution Explorer**, em **projeto de vendas da Internet AW**, clique duas vezes o **Model.bim** arquivo. O arquivo Model.bim contém todos os metadados para o seu projeto de modelo. 

![como-tabela-lição 1-se](../analysis-services/media/as-tabular-lesson1-se.png)
  
Vamos examinar as propriedades do modelo. Clique em **Model.bim**. No **propriedades** janela, você verá o [propriedades de modelo](../analysis-services/tabular-models/model-properties-ssas-tabular.md), mais importante do que é o **o modo DirectQuery** propriedade. Essa propriedade especifica se o modelo será implantado ou não no modo Na Memória (Desativado) ou no modo DirectQuery (Ativado). Neste tutorial, você criará e implantará o modelo no modo Em Memória.

![tabela-lição 1-propriedades como](../analysis-services/media/as-tabular-lesson1-properties.png)
  
Quando você cria um novo modelo, determinadas propriedades de modelo são definidas automaticamente acordo com as configurações de modelagem de dados que podem ser especificadas o **ferramentas** > **opções** caixa de diálogo. As propriedades de Backup de Dados, Retenção de Espaço de trabalho e Servidor de Espaço de Trabalho especificam como e onde o banco de dados de espaço de trabalho (seu banco de dados de criação de modelo) será submetido a backup, retido na memória e compilado. Você poderá alterar essas configurações posteriormente se necessário, mas, por enquanto, deixe essas propriedades como estão.  

Em **Solution Explorer**, clique com botão direito **de vendas pela Internet AW** (projeto) e, em seguida, clique em **propriedades**. O **páginas de propriedades de vendas de Internet AW** caixa de diálogo é exibida. Essas são as avançadas [propriedades do projeto](../analysis-services/tabular-models/project-properties-ssas-tabular.md). Você definirá posteriormente algumas dessas propriedades quando estiver pronto para implantar o modelo.  
  
Quando você tiver instalado o SSDT, vários novos itens de menu foram adicionados ao ambiente do Visual Studio. Vamos examinar os específicos para a criação de modelos de tabela. Clique no menu **Modelo** . Aqui, você pode iniciar o Assistente de importação de tabela, exibir e editar conexões existentes, atualizar dados de espaço de trabalho, procurar seu modelo no Excel com o recurso analisar no Excel, criar perspectivas e funções, selecione o modo de exibição do modelo e definir opções de cálculo.  
  
Clique no menu **Tabela** . Aqui, você pode criar e gerenciar relações entre tabelas, criar e gerenciar, especifique configurações de tabela de data, criar partições e editar propriedades de tabela.  
  
Clique no menu **Coluna** . Aqui, você pode adicionar e excluir colunas em uma tabela, congelar colunas e especificar a ordem de classificação. Você também pode usar o recurso AutoSum para criar uma medida de agregação padrão para uma coluna selecionada. Outros botões da barra de ferramentas fornecem acesso rápido a recursos e comandos frequentemente usados.  
  
Explore algumas das caixas de diálogo e locais de vários recursos específicos da criação de modelos de tabela. Embora alguns itens ainda não estejam ativos, você poderá ter uma boa noção do ambiente de criação de modelo de tabela.  


## <a name="additional-resources"></a>Recursos adicionais
Para saber mais sobre os diferentes tipos de projetos de modelo de tabela, consulte [Projetos de modelo de tabela &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md). Para saber mais sobre o ambiente de criação do modelo de tabela, consulte [Designer de modelo de tabela &#40;SSAS&#41;](../analysis-services/tabular-models/tabular-model-designer-ssas.md).  
  

## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 2: adicionar dados](../analysis-services/lesson-2-add-data.md).

  
  
  

