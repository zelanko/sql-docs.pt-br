---
title: Designer de modelo de tabela no SQL Server Data Tools | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98c836650ef00b283718ddf22834f7e4d4a56e0f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044840"
---
# <a name="tabular-model-designer"></a>Designer de modelo de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
O designer de modelo tabular faz parte do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], integrado com o Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], com modelos adicionais de tipo de projeto especificamente para desenvolver soluções profissionais de modelo tabular.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] é instalado como um download gratuito da Web. Consulte [Baixar o SSDT (SQL Server Data Tools)](../../ssdt/download-sql-server-data-tools-ssdt.md) para obter detalhes.    
  
##  <a name="bkmk_benefits"></a> Benefícios  
 Quando você instala o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], novos modelos de projeto para criar modelos de tabela são adicionados aos tipos de projeto disponíveis. Depois de criar um novo projeto de modelo tabular com o uso de um dos modelos, você pode começar a criar modelos usando as ferramentas e os assistentes de designer de modelo tabular.  
  
 Além dos novos modelos e ferramentas para criar soluções profissionais multidimensionais de modelo tabular, o ambiente de desenvolvimento do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] fornece recursos de desenvolvimento, depuração e ciclo de vida de projeto que garantem a criação das mais avançadas soluções de BI para sua organização. Para obter mais informações sobre o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], consulte o [Guia de Introdução ao Visual Studio](http://go.microsoft.com/fwlink/?LinkId=206389).  
  
##  <a name="bkmk_proj_temp"></a> Modelos de projeto  
 Quando você instala o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], os seguintes modelos de projeto de modelo de tabela são adicionados aos tipos de projeto de Business intelligence:  
  
 **Projeto tabular do Analysis Services**  
 Este modelo pode ser usado para criar um novo projeto de modelo de tabela em branco. Níveis de compatibilidade são especificados quando você cria o projeto.
  
 **Importar do servidor (tabular)**  
 Este modelo de projeto pode ser usado para criar um novo projeto de modelo de tabela por meio da extração de metadados de um modelo de tabela existente no Analysis Services.  
  
 Os modelos mais antigos têm níveis de compatibilidade mais antigos. Você pode atualizar, alterando a propriedade de nível de compatibilidade depois de importar a definição do modelo.  
  
 **Importar do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**  
 Este modelo é usado para criar um novo projeto de modelo de tabela por meio da extração de metadados e de dados de um arquivo do [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] .  
  
##  <a name="bkmk_wind_men"></a> Janelas e menus  
 O ambiente de criação de modelo tabular do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] inclui o seguinte:  
  
### <a name="designer-window"></a>Janela Designer  
 A janela do designer é usada para criar modelos tabulares fornecendo uma representação visual do modelo. Quando você abre o arquivo Model.bim, o modelo é aberto na janela do designer. Você pode criar um modelo na janela de designer usando dois modos de exibição diferentes:  
  
 **Exibição de dados**  
 A exibição de dados exibe tabelas em um formato de grade, tabular. Você também pode definir medidas usando a grade de medida, que pode ser mostrada para cada tabela somente na Exibição de Dados.  
  
 **Exibição de diagrama**  
 A exibição de diagrama exibe tabelas, com relações entre elas, em um formato gráfico. Colunas, medidas, hierarquias e KPIs podem ser filtrados e você pode optar por exibir o modelo usando uma perspectiva definida.  
  
 A maioria das tarefas de criação de modelos podem ser executadas em qualquer exibição.  
  
### <a name="view-code-window"></a>Exibir a janela de código  
 Você pode exibir o código por trás de um arquivo Model.bim clicando com o botão direito do mouse para selecionar **Exibir Código** no arquivo do Gerenciador de Soluções. Para modelos de tabela no nível de compatibilidade 1200 e posterior, a definição do modelo é expressa em JSON.  
  
 Observe que você precisará de uma versão completa do Visual Studio que forneça o editor de JSON. Você poderá baixar e instalar o [Visual Studio Community Edition gratuito](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) se não precisar dos recursos adicionais das edições comerciais.  
  
### <a name="solution-explorer"></a>Gerenciador de Soluções  
 A janela Gerenciador de Soluções apresenta a solução ativa como um contêiner lógico para um projeto de modelo de tabela e seus itens associados. O projeto modelo (.smproj) contém apenas um objeto Referências (vazio) e o arquivo Model.bim. Você pode abrir itens de projeto para modificação e executar outras tarefas de gerenciamento diretamente dessa exibição.  
  
 As soluções de modelo de tabela geralmente contêm só um projeto; no entanto, uma solução também pode conter outros projetos; por exemplo, para Integration Services ou projeto de serviços de Relatório. Você pode somar qualquer número de arquivos contanto que eles não sejam do mesmo tipo que os arquivos de projeto de modelo de tabela e a sua propriedade de Ação de Construção não esteja definida como Nenhum, nem a propriedade Copiar para Diretório de Saída esteja definida como Não Copiar.  
  
 Para exibir o Gerenciador de Soluções, clique no menu **Exibir** e clique no **Gerenciador de Soluções**.  

### <a name="tabular-model-explorer"></a>Gerenciador de Modelos de Tabela
  Primeira disponível na versão de agosto de 2016 (14.0.60812.0) do [SQL Server Data Tools](https://msdn.microsoft.com/mt186501), Gerenciador de modelos de tabela ajuda você a navegar objetos de metadados em modelos de tabela.

 Para mostrar o Gerenciador de Modelos de Tabela, clique em **Exibir** > **Outras Janelas**e em **Gerenciador de Modelos de Tabela**.
   
  ![Gerenciador de Modelos de Tabela](../../analysis-services/tabular-models/media/tabular-model-explorer.png) 
  
 Gerenciador de modelos de tabela organiza os objetos de metadados em uma estrutura de árvore que é parecido com o esquema de um modelo de tabela. Fontes de dados, perspectivas, relações, funções, tabelas e traduções correspondem aos objetos de esquema de nível superior. Há algumas exceções, especificamente KPIs e Medidas, que tecnicamente não são objetos de nível superior, mas objetos filho de várias tabelas no modelo. No entanto, a consolidação de contêineres de nível superior para todos os KPIs e Medidas facilita o trabalho com esses objetos, especialmente se seu modelo incluir um número muito grande de tabelas. As medidas também são listadas em suas tabelas pai correspondentes, para que você tenha uma visão clara das relações pai-filho reais. Se você selecionar uma medida no contêiner Medidas de nível superior, a mesma medida também será selecionada na coleção filho em sua tabela e vice-versa.  
 
 Os nós de objeto no Gerenciador de Modelos de Tabela são vinculados às opções de menu apropriadas que até agora estavam ocultas nos menus Modelo, Tabela e Coluna do Visual Studio. É possível clicar com o botão direito do mouse em um objeto para explorar as opções do tipo de objeto. Nem todos os tipos de nó de objeto ainda têm um menu de contexto, mas em breve, as próximas versões terão melhorias e outras opções. 

 O Gerenciador de Modelos de Tabela também oferece um recurso de pesquisa conveniente. Basta digitar uma parte do nome na caixa de pesquisa e o Gerenciador de Modelos de Tabela restringirá a exibição de árvore às correspondências. 
  
### <a name="properties-window"></a>Janela Propriedades  
 A janela Propriedades lista as propriedades do objeto selecionado. Os objetos a seguir têm propriedades que podem ser exibidas e editadas na janela de Propriedades:  
  
-   Model.bim  
  
-   Table  
  
-   Coluna  
  
-   Measure  
  
 Propriedades do projeto exibem somente o nome do projeto e a pasta do projeto na janela Propriedades. Projetos também têm opções de implantação adicionais e configurações de servidor de implantação que você pode definir usando uma caixa de diálogo de propriedades modais. Para exibir essas propriedades, no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
 Os campos na janela Propriedades têm controles inseridos que são abertos quando você clica neles. O tipo de controle de edição depende da propriedade específica. Esses controles incluem caixas de edição, listas suspensas e links para caixas de diálogo personalizadas. Propriedades que são mostradas esmaecidas são somente leitura.  
  
 Para exibir a janela **Propriedades** , clique no menu **Exibir** e clique na **Janela de Propriedades**.  
  
### <a name="error-list"></a>Lista de Erros  
 A janela Lista de Erros contém mensagens sobre o estado do modelo:  
  
-   Notificações sobre práticas recomendadas em relação à segurança.  
  
-   Requisitos para processamento de dados.  
  
-   Informações de erro semânticas para colunas calculadas, medidas e filtros de linha para funções. Para colunas calculadas, você pode clicar duas vezes na mensagem de erro para navegar até a origem do erro.  
  
-   Erros de validação DirectQuery.  
  
 Por padrão, a **Lista de Erros** não aparece a menos que um erro seja retornado. Porém, você pode exibir a janela **Lista de Erros** a qualquer momento. Para exibir a janela **Lista de Erros** , clique no menu **Exibir** e clique na **Lista de Erros**.  
  
### <a name="output"></a>Saída  
 As informações de build e implantação são exibidas na janela **Saída** (além da caixa de diálogo de andamento modal). Para exibir a janela **Saída** , clique no menu **Exibir** e clique em Saída.  
  
### <a name="menu-items"></a>Itens de menu  
 Quando você instala o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], itens de menu adicionais especificamente para criação de modelos tabulares são adicionados à barra de menus do Visual Studio. O menu **Modelo** pode ser usado para iniciar o Assistente de Importação de Dados, exibir as conexões existentes, processar dados do espaço de trabalho e navegar no espaço de trabalho de modelo no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. O menu **Tabela** é usado para criar e gerenciar relações entre tabelas, criar e gerenciar medidas, especificar configurações de tabelas de dados, especificar opções de cálculo e especificar outras propriedades de tabela. Com o menu **Coluna** é possível adicionar e excluir colunas em uma tabela, ocultar e reexibir colunas e especificar outras propriedades de coluna, como tipos de dados e filtros. Você pode criar e implantar soluções de modelo de tabela no menu **Criar** . As funções Copiar/Colar são incluídas no menu **Editar** .  
  
 Além desses itens de menu, mais configurações foram adicionadas às opções do Analysis Services nos itens do menu Ferramentas.  
  
### <a name="toolbar"></a>Barra de Ferramentas  
 A barra de ferramentas de Analysis Services fornece acesso rápido e fácil aos comandos de criação de modelo mais frequentemente usados.  
  
##  <a name="bkmk_vsint"></a> Integração do Visual Studio  
 **Controle do código-fonte**  
 Os projetos do Analysis Services são integrados com o plug-in de controle do código-fonte selecionado. Se você configurou o Visual Studio para usar o controle do código-fonte, poderá usar check in/check out no Gerenciador de Soluções. Para configurar o uso do Team Foundation Server, consulte [Configurar o Visual Studio com o controle de versão do Team Foundation](http://msdn.microsoft.com/library/ms253064.aspx). Muitos plug-ins de controle do código-fonte de terceiros também têm suporte.  
  
 **Fontes**  
 Os modelos de tabela usam a fonte de ambiente do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para controlar as fontes na exibição. Poderá ser necessário alterar esta fonte se a fonte padrão de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] não tiver todos os caracteres Unicode que você precisa para seu idioma. Para alterar fontes, clique no menu **Ferramentas** , **Opções**e **Fontes e Cores**.  
  
 **Atalhos de teclado**  
 Os atalhos de teclado do Analysis Services podem ser configurados/remapeados pela caixa de diálogo Ferramentas->Opções->Teclado. Alguns atalhos globais [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , como criar, salvar, depurar, novo projeto, etc. têm suporte no contexto do designer de modelo de tabela. Outros atalhos específicos do designer de modelo tabular estão no contexto do Analysis Services.  
  
## <a name="see-also"></a>Consulte também  
 [Projetos de modelo de tabela](../../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md)   
  
  
