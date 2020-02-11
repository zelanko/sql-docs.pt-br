---
title: Criar um cubo usando uma exibição da fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bec845a1-d10c-4d45-9acf-0a302adfee47
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84e134854770f0096cc99c94698cfd8d7e3e818a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66076562"
---
# <a name="create-a-cube-using-a-data-source-view"></a>Criar um cubo usando uma Exibição da Fonte de Dados
  Use este método de criar um novo cubo se você pretender usar uma exibição existente de fonte de dados. Com esse método, você especifica uma exibição de fonte de dados e seleciona tabelas de fatos e dimensões que deseja usar na exibição da fonte de dados. Em seguida, escolha as dimensões e as medidas que deseja incluir no cubo.  
  
 Para criar um cubo com uma fonte de dados, no Gerenciador de Soluções, clique com o botão direito do mouse em **Cubos** e selecione **Novo Cubo**. O Assistente para Cubos é aberto.  
  
## <a name="selecting-the-build-method"></a>Selecionando o Método de Criação  
 Na página **Selecionar Método de Criação** do assistente, clique em **Criar o cubo usando uma fonte de dados**.  
  
 Se você marcar a caixa de seleção **Criação automática** , o assistente analisará a exibição da fonte de dados para configurar o cubo e suas dimensões para você. O assistente identifica as tabelas de fatos e dimensões do cubo, seleciona as medidas para a serem incluídas no cubo e cria hierarquias. Em cada página do assistente, você pode examinar e alterar as escolhas que o assistente faz quando **Criação automática** é selecionada. Se você não selecionar **Criação automática**, fará todas estas escolhas manualmente.  
  
 Se você selecionar **Criação automática**, poderá clicar em **Fim** em qualquer página do assistente para ir para a última página e aceitar as configurações padrão para as páginas restantes do assistente. Na última página do assistente, você pode examinar a estrutura do cubo antes de concluir o assistente.  
  
 Se você não selecionar **Criação automática**, deverá selecionar as tabelas de fatos e dimensões por conta própria. O assistente cria as dimensões que você escolhe criar, mas você deve usar o Designer de Dimensão para manualmente criar hierarquias definidas pelo usuário nas dimensões. Este requisito poderá não fazer nenhuma diferença se você já tiver criado as dimensões que deseja usar no cubo antes de executar o Assistente para Cubos.  
  
## <a name="selecting-the-data-source-view"></a>Selecionando a Exibição da fonte de dados  
 Se você usar uma fonte de dados existente para criar um cubo, a primeira etapa é especificar a exibição de fonte de dados na qual basear o cubo. Na página **Selecionar Exibição da Fonte de Dados** , selecione uma exibição de fonte de dados existente. No painel de visualização, você pode exibir as tabelas em uma exibição da fonte de dados selecionada. Para exibir o esquema para qualquer exibição da fonte de dados selecionada, clique em **Procurar**.  
  
 Se a exibição da fonte de dados que você deseja usar não estiver listada, no Assistente para Cubos, clique em **Cancelar**e abra o Assistente de Exibição da Fonte de Dados. Você também pode clicar em **Adicionar Novo Item** no menu **Arquivo** para adicionar uma exibição de fonte de dados existentes de outro banco de dados (ou outro local). Para obter mais informações sobre exibições de fonte de dados, consulte [Exibições de Fonte de Dados em Modelos Multidimensionais](data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Uma exibição da fonte de dados deve conter pelo menos uma tabela a ser listada nesta página. Você não pode criar um cubo com base em uma exibição da fonte de dados sem tabelas.  
  
## <a name="identify-fact-and-dimension-tables"></a>Identificar Tabelas de Fatos e Dimensões  
 No Assistente para Cubos, use a página **Identificar Tabelas de Fatos e Dimensões** do assistente para selecionar as tabelas de fatos e dimensões necessárias para criar o cubo. Se você marcou a caixa de seleção **Criação automática** para criar o cubo, serão selecionadas as tabelas de fatos ou dimensões que o assistente detecta quando esta página aparecer primeiro. Se o assistente detectar uma tabela que é uma tabela de fato e uma tabela de dimensão, serão selecionadas ambas as colunas. Se o assistente detectar uma tabela que é nenhuma delas, nenhuma coluna será selecionada. Se você não precisar de uma tabela para seu design de cubo, desmarque as caixas de seleção **Fato** e **Dimensão** .  
  
 Se você não marcou a caixa de seleção **Criação automática** , deve fazer todas as seleções manualmente. Use a guia **Tabelas** ou a guia **Diagrama** :  
  
-   A guia **Tabelas** lista as tabelas em formato de tabela. Marque a caixa de seleção na coluna **Fato** ou na coluna **Diagrama** .  
  
-   A guia **Diagrama** exibe o esquema da exibição de fonte de dados. As tabelas são codificadas por cores para indicar fato ou dimensão. Clique em qualquer tabela no esquema e clique em **Fato** ou **Dimensão** para selecionar ou desmarcar a configuração nessa tabela. Use o botão de **Zoom** para alterar a ampliação.  
  
> [!NOTE]  
>  Na guia **Diagrama** , você pode ampliar ou maximizar a janela do assistente para exibir o esquema.  
  
 Se houver uma tabela de dimensão de tempo na exibição da fonte de dados, selecione-a na lista **Tabela de dimensões de tempo** . Se não houver nenhum, deixe ** \<nenhuma>** selecionada. Este é o item padrão na lista. Selecionar uma tabela como a tabela de dimensão de tempo também a seleciona como uma tabela de dimensão nas guias **Tabelas** e **Diagrama** .  
  
## <a name="defining-time-periods"></a>Definindo períodos de tempo  
 Se você especificou uma tabela de dimensão de tempo enquanto selecionava tipos de tabela, use a página **Definir períodos de tempo** do assistente para especificar as colunas na tabela que correspondem a períodos de tempo padrão. Procure os períodos padrão em **Nome da Propriedade de Tempo**. Para cada linha que tem uma coluna correspondente na tabela de dimensão de tempo, escolha a coluna correta em **Colunas da Tabela de Tempo**. O assistente usa as associações que você especifica para criar atributos e sugerir hierarquias de tempo que fazem sentido para seus dados. Estas associações também definem a propriedade **Tipo** para os atributos correspondentes na nova dimensão de tempo. O assistente cria uma dimensão de tempo com base em uma tabela de dimensão de tempo.  
  
 Depois de criar o cubo, você pode usar o Assistente de Business Intelligence para adicionar aprimoramentos de inteligência de tempo ao cubo. Esses aprimoramentos incluem exibições do período até esta data, de média móvel e de período a período.  
  
## <a name="selecting-dimensions"></a>Selecionando dimensões  
 Use a página **Selecionar Dimensões** do assistente para adicionar dimensões ao cubo. Esta página só aparecerá se já houver dimensões compartilhadas correspondentes a tabelas de dimensão no novo cubo.  
  
 Para adicionar dimensões existentes, selecione uma ou mais dimensões na lista **Dimensões compartilhadas** e clique no botão de seta para a direita (**>**) para movê-las para a lista **Dimensões do cubo** . Clique no botão de seta dupla**>>**() para mover todas as dimensões na lista.  
  
 Se uma dimensão existente não aparecer na lista e você achar que deve, clique em **Voltar** e altere as configurações de tipo de tabela para uma ou mais tabelas. Uma dimensão existente também deve estar relacionada a pelo menos uma das tabelas de fato no cubo para aparecer na lista **Dimensões compartilhadas** .  
  
## <a name="selecting-measures"></a>Selecionando medidas  
 Use a página **Selecionar Medidas** do assistente para selecionar as medidas que você quer incluir no cubo. Todas as tabelas marcadas como uma tabela de fato aparecem como um grupo de medidas nesta lista e todas as colunas que não são de chave numérica aparecem como uma medida na lista. Por padrão toda medida em todo grupo de medidas é selecionada. Você pode desmarcar a caixa de seleção ao lado das medidas que não deseja incluir no cubo. Para remover todas as medidas de um grupo de medidas do cubo, desmarque a caixa de seleção **Grupos de Medidas/Medidas** .  
  
 Os nomes de medidas listados em **Grupos de Medidas/Medidas** refletem nomes de coluna. Clique na célula que contém o nome para editá-lo.  
  
 Para exibir dados para qualquer medida, clique com o botão direito do mouse em qualquer linha de medida na lista e clique em **Exibir dados de exemplo**. Isto abre o **Visualizador de Exemplos de Dados** e exibe até os primeiros 1000 registros da tabela de fato correspondente.  
  
## <a name="reviewing-new-dimensions"></a>Examinando novas dimensões  
 Use a página **Examinar Novas Dimensões** do assistente para examinar as estruturas das dimensões criadas pelo assistente. As dimensões são listadas nesta página do assistente no modo de exibição de árvore **Novas dimensões** . Você pode examinar as dimensões das seguintes formas:  
  
-   Expanda qualquer dimensão para exibir seus atributos e hierarquias.  
  
-   Expanda a pasta **Atributos** em qualquer dimensão para exibir os atributos de uma dimensão.  
  
-   Expanda a pasta **Hierarquia** em qualquer dimensão para exibir as hierarquias de uma dimensão.  
  
-   Expanda qualquer hierarquia para exibir seus níveis.  
  
> [!NOTE]  
>  Você pode ampliar ou maximizar a janela do assistente para exibir melhor a árvore.  
  
 Para remover qualquer objeto na árvore do cubo, desmarque a caixa de seleção ao lado dele. Desmarcar a caixa de seleção ao lado de um objeto também remove todos os objetos debaixo dele. As dependências entre objetos são impostas, de modo que, se você remover um atributo, os níveis de hierarquia dependentes no atributo também serão removidos. Por exemplo, desmarcar uma caixa de seleção ao lado de uma hierarquia desmarca as caixas de seleção ao lado de todos os níveis na hierarquia, e remove os níveis e também as hierarquias. O atributo de chave para uma dimensão não pode ser removido.  
  
 Você pode renomear qualquer dimensão, atributo, hierarquia ou nível clicando no nome ou clicando com o botão direito do mouse no nome e, em seguida, no menu de atalho, clicando em **renomear \<objeto>**, em que ** \<o objeto>** é **dimensão**, **atributo**ou **nível**.  
  
 Não há necessariamente uma relação de um para um entre o número de tabelas de dimensão definido na página **Identificar Tabelas de Fatos e Dimensões** do assistente e o número de dimensões listadas nesta página do assistente. Dependendo das relações entre as tabelas na exibição da fonte de dados, o assistente pode usar duas ou mais tabelas para criar uma dimensão (por exemplo, como exigido por um esquema de floco de neve).  
  
## <a name="completing-the-cube-wizard"></a>Concluindo o Assistente para Cubos  
 Na página **Concluindo o Assistente** do assistente, você pode exibir os grupos de medidas, as medidas e as dimensões no novo cubo. Na caixa **Nome do cubo** , digite um nome para o cubo. Em seguida, se estiver satisfeito com o cubo, clique em **Concluir**. Clique em **Voltar** para voltar para uma página anterior do assistente e fazer alterações.  
  
  
