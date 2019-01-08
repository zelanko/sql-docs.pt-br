---
title: Criar um projeto do Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- templates [Analysis Services]
- templates [Analysis Services], projects
- projects [Analysis Services], creating
- projects [Analysis Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, defining projects [Analysis Services]
- items [Analysis Services]
ms.assetid: d00913b0-cd6d-4de0-a1e7-4ce86fcc078d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ccf355df8a26136a72b48c4b81a1953d84d90186
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529638"
---
# <a name="create-an-analysis-services-project-ssdt"></a>Criar um Projeto de Analysis Services (SSDT)
  Você pode definir um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o modelo de projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou Assistente para Importação de Banco de Dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para ler o conteúdo de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se não houver uma solução carregada no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a criação de um novo projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] criará automaticamente uma nova solução. Caso contrário, o novo projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] será adicionado à solução existente. As práticas recomendadas para o desenvolvimento de soluções exigem a criação de projetos separados para tipos diferentes de dados de aplicativo, usando uma única solução se os projetos forem relacionados. Por exemplo, você pode ter uma única solução que contém projetos separados para pacotes de Integration Services, bancos de dados do Analysis Services e relatórios do Reporting Services que são todos usados pelo mesmo aplicativo de negócios.  
  
 Um projeto do Analysis Services contém objetos usados em um único banco de dados do Analysis Services. As propriedades de implantação do projeto especificam o servidor e o nome do banco de dados para o qual os metadados do projeto serão implantados como objetos instanciados.  
  
 Este tópico contém as seguintes seções:  
  
 [Criar um novo projeto usando o modelo do projeto do Analysis Services](#bkmk_NewUsingTemplate)  
  
 [Criar um novo projeto usando um banco de dados existente do Analysis Services](#bkmk_NewUsingWizard)  
  
 [Adicionar um projeto do Analysis Services a uma solução existente](#bkmk_AddtoExistingSolution)  
  
 [Criar e implantar a solução](#bkmk_buildDeploy)  
  
 [Pastas do projeto do Analysis Services](#bkmk_ProjectFolders)  
  
 [Tipos de arquivo do Analysis Services](#bkmk_FileTypes)  
  
 [Modelos de item do Analysis Services](#bkmk_ItemTemplates)  
  
##  <a name="bkmk_NewUsingTemplate"></a> Criar um novo projeto usando o modelo do projeto do Analysis Services  
 Use estas instruções para criar um projeto vazio no qual você define objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que você pode então implantá-los como um novo banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique em **Arquivo**, aponte para **Novo**e clique em **Projeto**. Na caixa de diálogo **Novo Projeto** , no painel **Tipos de projeto** , selecione **Projetos do Business Intelligence**.  
  
2.  Na caixa de diálogo **Novo Projeto** , na categoria **Modelos instalados do Visual Studio** , selecione **Projeto do Analysis Services**.  
  
3.  Na caixa de texto **Nome** , digite o nome do projeto. O nome que você insere será usado como o nome do banco de dados padrão.  
  
4.  Na lista suspensa **Localização** , digite ou selecione a pasta na qual armazenar os arquivos do projeto ou clique em **Procurar** para selecionar uma pasta.  
  
5.  Para adicionar o projeto novo à solução existente, na lista suspensa **Solução** , selecione **Adicionar à Solução**.  
  
     -ou-  
  
     Para criar uma nova solução, na lista suspensa **Solução** , selecione **Criar nova Solução**. Para criar uma nova pasta para a nova solução, selecione **Criar diretório para a solução**. Em **Nome da Solução**, digite o nome da nova solução.  
  
6.  Clique em **OK**.  
  
##  <a name="bkmk_NewUsingWizard"></a> Criar um novo projeto usando um banco de dados existente do Analysis Services  
 Use o Assistente para Importação de Bancos de Dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para criar um projeto com base nos objetos no banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Quando você define um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com base em um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , os metadados desse banco de dados serão abertos em um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Esses objetos poderão ser modificados dentro do projeto, sem afetar os objetos originais e, em seguida, ser implantados no mesmo banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se as propriedades de implantação especificarem esse banco de dados, ou no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recém-criado para um teste comparativo. Até que as alterações sejam implantadas, nenhuma alteração afetará o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Você também pode usar o modelo de Importação de Bancos de Dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para criar um projeto a partir do banco de dados de produção no qual foram feitas alterações diretamente desde que o projeto original do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] foi implantado.  
  
 Antes de você processar ou implantar o projeto, pode precisar alterar o provedor de dados que está especificado nas fontes de dados. Se o software do SQL Server que você está usando for mais novo que o software usado para criar o banco de dados, o provedor de dados especificado em seu projeto pode não ser instalado em seu computador. Durante o processamento, a conta de serviço será usada para recuperar os dados em seu banco de dados do Analysis Services. Se o banco de dados estiver em um servidor remoto, verifique se o serviço local tem permissões de processo e leitura naquele servidor.  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique em **Arquivo**, aponte para **Novo**e clique em **Projeto**. Na caixa de diálogo **Novo Projeto** , no painel **Tipos de projeto** , selecione **Projetos do Business Intelligence**.  
  
2.  Na caixa de diálogo **Novo Projeto** , na categoria **Modelos instalados do Visual Studio** , selecione **Importar Bancos de Dados do Analysis Services**.  
  
3.  Insira informações de propriedade para o projeto e solução, inclusive nome e local para os arquivos. Clique em **OK**.  
  
4.  Na página Bem-vindo ao **Assistente para Importação de Banco de Dados do Analysis Services** , clique em **Avançar**.  
  
5.  Na página **Banco de Dados de Origem** , especifique o servidor e o banco de dados por meio dos quais o assistente extrairá o conteúdo e criará o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, clique em **Avançar**.  
  
     Os bancos de dados com suporte incluem os criados nas seguintes versões do Analysis Services: [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
     Você pode digitar o nome de banco de dados ou consultar o servidor para exibir os bancos de dados existentes nele. Se o banco de dados estiver em um servidor remoto ou servidor de produção, você pode precisar solicitar permissão para ler o banco de dados. Os parâmetros de configuração do firewall podem restringir mais ainda o acesso a um banco de dados. Se você obtiver um erro ao tentar se conectar ao banco de dados, primeiro verifique as permissões e as configurações do firewall.  
  
6.  Quando o assistente terminar de extrair o conteúdo do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , clique em **Concluir** na página **Concluindo o Assistente** .  
  
7.  Abra a janela Gerenciador de Soluções para exibir o conteúdo do projeto.  
  
##  <a name="bkmk_AddtoExistingSolution"></a> Adicionar um projeto do Analysis Services a uma solução existente  
 Se você já tiver uma solução que contém todos os arquivos de origem de um aplicativo de negócios, poderá adicionar um novo projeto do Analysis Services àquela solução.  
  
 Adicionar um projeto existente a uma solução associa, mas não copia, o projeto com a solução. Se o projeto de Analysis Services tiver sido criado em uma solução diferente, os arquivos de projeto permanecerão com a solução original para a qual foram criados. Isto significa que qualquer alteração que você fizer ao projeto por meio de qualquer solução funcionará no mesmo conjunto de arquivos de origem. Se este comportamento não for o que você pretende, você deverá copiar ou mover os arquivos de projeto para a nova pasta de solução primeiro e, em seguida, adicionar o projeto à solução.  
  
1.  Abra a solução no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. No Gerenciador de Soluções, clique com o botão direito do mouse na solução, aponte para **Adicionar**e clique em **Projeto Existente** para selecionar o projeto que deseja adicionar.  
  
2.  Selecione um projeto .dwproj para adicionar à solução.  
  
##  <a name="bkmk_buildDeploy"></a> Criar e implantar a solução  
 Por padrão, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] implanta um projeto na instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no computador local. É possível alterar o destino de implantação na caixa de diálogo **Páginas de Propriedades** do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para alterar a propriedade de configuração **Servidor** .  
  
> [!NOTE]  
>  Por padrão, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] processa apenas objetos alterados pelo script de implantação e os objetos dependentes ao implantar uma solução. É possível alterar essa funcionalidade na caixa de diálogo **Páginas de Propriedades** do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para alterar a propriedade de configuração Opções de Processamento.  
  
 Construa e implante a solução em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para teste. Construir uma solução valida as definições do objeto e as dependências no projeto, além de gerar um script de implantação. A implantação da solução usa o mecanismo de implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para enviar o script de implantação a uma instância especificada.  
  
 Depois de implantar o projeto, examine e teste o banco de dados implantado. Você pode modificar as definições de objeto, criar e implantar novamente até que o projeto esteja concluído.  
  
 Depois que o projeto estiver concluído, você poderá usar o Assistente para Implantação para implantar o script de implantação, gerado quando você compilou a solução, nas instâncias de destino para teste final, preparação e implantação.  
  
##  <a name="bkmk_ProjectFolders"></a> Pastas do projeto do Analysis Services  
 Um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contém as pastas a seguir, usadas para organizar os itens incluídos no projeto.  
  
|Pasta|Descrição|  
|------------|-----------------|  
|Fontes de dados|Contém as fontes de dados de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você cria esses objetos com o Assistente de Fonte de Dados e os edita no Designer de Fonte de Dados.|  
|Exibições da fonte de dados|Contém as exibição da fonte de dados de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você cria esses objetos com o Assistente de Exibição da Fonte de Dados e os edita no Designer de Exibição da Fonte de Dados.|  
|Cubes|Contém os cubos de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você cria esses objetos com o Assistente para Cubos e os edita no Designer de Cubo.|  
|Dimensões|Contém as dimensões de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você cria esses objetos com o Assistente para Dimensões ou Assistente para Cubos e os edita no Designer de Dimensão.|  
|Estruturas de mineração|Contém as estruturas de mineração de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você cria esses objetos com o Assistente para Modelo de Mineração e os edita no Designer de Modelo de Mineração.|  
|Funções|Contém as funções de banco de dados de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você cria e administra funções no Designer de Função.|  
|Assemblies|Contém referências a bibliotecas COM e assemblies do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você cria referências na caixa de diálogo **Adicionar Referência** .|  
|Diversos|Contém qualquer tipo de arquivo, com exceção dos tipos de arquivo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Use essa pasta para adicionar os arquivos diversos, como arquivos de texto com observações sobre o projeto.|  
  
##  <a name="bkmk_FileTypes"></a> Tipos de arquivo do Analysis Services  
 A solução do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] pode conter vários tipos de arquivo, dependendo dos projetos incluídos nela e de seus itens. Em geral, os arquivos de cada projeto de uma solução do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] são armazenados na pasta da solução, em uma pasta separada para cada projeto.  
  
> [!NOTE]  
>  Copiar um arquivo de um objeto para uma pasta de projeto não adiciona esse objeto ao projeto. Use o comando **Adicionar** do menu de contexto do projeto no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para adicionar a definição de um objeto existente a um projeto.  
  
 A pasta de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode conter os tipos de arquivo listados na tabela a seguir.  
  
|Tipo de arquivo|Descrição|  
|---------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] arquivo de definição de projeto (.dwproj)|Contém metadados sobre itens, configurações e referências de assembly definidos e incluídos no projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configurações de usuário do projeto (.dwproj.user)|Contém informações de configuração para o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para um usuário específico.|  
|Arquivo de fonte de dados (.ds)|Contém elementos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Idioma (ASSL) que definem metadados para uma fonte de dados.|  
|Arquivo de exibição da fonte de dados (.dsv)|Contém elementos ASSL que definem metadados para uma exibição da fonte de dados.|  
|Arquivo de cubo (.cube)|Contém elementos ASSL que definem metadados para um cubo, incluindo grupos de medidas, medidas e dimensões de cubo.|  
|Arquivo de partição (.partitions)|Contém elementos ASSL que definem metadados para as partições do cubo especificado.|  
|Arquivo de dimensão (.dim)|Contém elementos ASSL que definem metadados para uma dimensão do banco de dados.|  
|Arquivo de estrutura de mineração (.dmm)|Contém elementos ASSL que definem metadados para uma estrutura de mineração e modelos de mineração associados.|  
|Arquivo de banco de dados (.database)|Contém elementos ASSL que definem metadados para um banco de dados, incluindo tipos de contas, traduções e permissões do banco de dados.|  
|Arquivo de funções do banco de dados (.role)|Contém elementos ASSL que definem metadados para uma função de banco de dados, inclusive membros de função.|  
  
##  <a name="bkmk_ItemTemplates"></a> Modelos de item do Analysis Services  
 Se você usar a caixa de diálogo **Adicionar Novo Item** para adicionar novos itens a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , terá a opção de usar um modelo de item, um script predefinido ou uma instrução que demonstra como executar uma determinada ação.  
  
 Os modelos de item, listados na tabela a seguir, estão disponíveis na categoria Itens de Projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na caixa de diálogo **Adicionar Novo Item** .  
  
|Categoria|Modelo de item|Descrição|  
|--------------|-------------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Itens de projeto|Cube|Inicia o Assistente para Cubos para adicionar um cubo novo ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||fonte de dados|Inicia o Assistente para Fonte de Dados para adicionar uma nova fonte de dados ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Exibição da Fonte de Dados|Inicia o Assistente de Exibição da Fonte de Dados para adicionar uma nova exibição da fonte de dados ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Função de banco de dados|Adiciona uma nova função de banco de dados ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, exibe o Designer de Funções para a nova função de banco de dados.|  
||Dimensão|Inicia o Assistente para Dimensões para adicionar uma nova dimensão de banco de dados ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Estrutura de mineração|Use o Assistente de Data Mining para adicionar uma nova estrutura de mineração e um novo modelo de mineração ao projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)   
 [Criar projetos do Analysis Services &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)   
 [Implantar projetos do Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
