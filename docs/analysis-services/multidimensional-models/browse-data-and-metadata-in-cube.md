---
title: Procurar dados e metadados no cubo | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5faf2a9d-df39-465f-9c81-a00d5cd63f5a
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a4f1dcea3c74fdf61af401a854aba9c2166f5610
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="browse-data-and-metadata-in-cube"></a>Procurar dados e metadados no Cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Use o **navegador** guia do Designer de cubo para procurar dados de cubo. Você pode usar esta exibição para examinar a estrutura de um cubo e verificar dados, cálculo, formatação e segurança de objetos de banco de dados. Você pode examinar rapidamente um cubo como usuários finais o veem em ferramentas de relatório ou outros aplicativos cliente. Quando você procurar dados do cubo, poderá exibir dimensões diferentes, detalhar os membros e segmentar as dimensões.  
  
 Antes de você procurar um cubo, deverá processá-lo e se reconectar a ele. Depois de processá-lo, abra a guia **Navegador** do Designer de Cubo. Clique no botão Reconectar na barra de ferramentas para atualizar a conexão.  
  
 A guia **Navegador** tem três painéis: o painel de Metadados, o painel de Filtro e o painel de Dados. Use o painel de Metadados para examinar a estrutura do cubo em formato de árvore. Use o painel de Filtro na parte superior da guia **Navegador** para definir o subcubo pelo qual você deseja navegar. Use o painel de Dados para exibir o conjunto de resultados e analisar as hierarquias da dimensão.  
  
## <a name="setting-up-the-browser"></a>Configurando o navegador  
 Para preparar para procurar um cubo, você pode especificar uma perspectiva ou tradução que você queira usar. Você adiciona medidas e dimensões ao painel de Dados e especifica os filtros no painel de Filtros.  
  
##### <a name="specifying-a-perspective"></a>Especificando uma perspectiva  
 Use a lista **Perspectiva** para escolher uma perspectiva que seja definida para o cubo. As perspectivas são definidas na guia **Perspectivas** do Designer de Cubo. Para alternar para uma perspectiva diferente, selecione uma perspectiva na lista.  
  
##### <a name="specifying-a-translation"></a>Especificando uma tradução  
 Use a lista **Idioma** para escolher uma tradução que seja definida para o cubo. As traduções são definidas na guia **Translações** do Designer de Cubo. A guia **Navegador** inicialmente mostra legendas para o idioma padrão que é especificado pela propriedade **Idioma** para o cubo. Para alternar para um idioma diferente, selecione um idioma na lista.  
  
##### <a name="formatting-the-data-pane"></a>Formatando o painel de dados  
 Você pode formatar legendas e células no painel de Dados. Clique com o botão direito do mouse nas células ou legendas selecionadas que você deseja formatar e clique em **Comandos e Opções**. Dependendo da seleção, a caixa de diálogo **Comandos e Opções** exibe configurações para **Formato**, **Filtro e Grupo**, **Relatório**e **Comportamento**.  
  
## <a name="setting-up-the-data"></a>Configurando os dados  
  
##### <a name="adding-or-removing-measures"></a>Adicionando ou removendo medidas  
 Arraste as medidas pelas quais você deseja navegar do painel de Metadados até a área de detalhes do painel de Dados que é o painel vazio grande no lado inferior direito do espaço de trabalho. À medida que você arrasta medidas adicionais, elas são adicionadas como colunas. Uma linha vertical indica onde cada medida adicional será solta. Arrastar a pasta **Medidas** solta todas as medidas na área de detalhes.  
  
 Para remover uma medida da área de detalhes, arraste-a para fora do painel de Dados ou clique com o botão direito do mouse nela e clique em **Excluir** no menu de atalho.  
  
##### <a name="adding-or-removing-dimensions"></a>Adicionando ou removendo dimensões  
 Arraste as hierarquias ou dimensões para as áreas de linha ou filtro.  
  
 Se você quiser trabalhar com várias dimensões, use Analisar no Excel. Analisar no Excel é um atalho que iniciará o Excel se instalado no mesmo computador do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. O Excel abrirá uma pasta de trabalho que contém uma conexão existente com o banco de dados atual e uma Lista de Campos da Tabela Dinâmica pré-carregada com medidas e dimensões. Para obter mais informações, consulte [Analisar no Excel &#40;Guia Navegador, Designer de Cubo&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](http://msdn.microsoft.com/library/890ed457-137e-44ac-9b2c-83344a1b8fc9).  
  
 Para remover uma dimensão, arraste-a para fora do painel de Dados ou clique com o botão direito do mouse nela e clique em **Excluir** no menu de atalho.  
  
##### <a name="adding-or-removing-filters"></a>Adicionando ou removendo filtros  
 Você pode usar um dos seguintes métodos para adicionar um filtro:  
  
-   Expanda uma dimensão no painel de Metadados e arraste uma hierarquia para o painel de Filtro.  
  
     \- ou –  
  
-   No **dimensão** coluna o **filtro** painel, clique em  **\<selecionar dimensão >** e selecione uma dimensão na lista e clique em  **\<Selecionar hierarquia >** no **hierarquia** coluna e selecione uma hierarquia na lista.  
  
 Depois que você especificar a hierarquia, especifique o operador e a expressão de filtro. A tabela a seguir descreve os operadores e as expressões de filtro.  
  
|Operador|Expressão de filtro|Description|  
|--------------|-----------------------|-----------------|  
|Equal|Um ou mais membros|Os valores devem ser iguais a um membro especificado.<br /><br /> (Fornece várias seleções de membro para hierarquias de atributo, além de hierarquias pai-filho e seleção única de membro para outras hierarquias.)|  
|Diferente de|Um ou mais membros|Os valores não devem ser iguais a um membro especificado.<br /><br /> (Fornece várias seleções de membro para hierarquias de atributo, além de hierarquias pai-filho e seleção única de membro para outras hierarquias.)|  
|Entrada|Um ou mais conjuntos nomeados|Os valores devem estar em um conjunto nomeado especificado.<br /><br /> (Suporte somente a hierarquias de atributo.)|  
|Não Está em|Um ou mais conjuntos nomeados|Os valores não devem estar em um conjunto nomeado especificado.<br /><br /> (Suporte somente a hierarquias de atributo.)|  
|Intervalo (Inclusivo)|Um ou dois membros delimitadores de um intervalo|Os valores devem estar entre ou ser iguais aos membros delimitadores. Se os membros delimitadores forem iguais ou somente um membro for especificado, nenhum intervalo será imposto e todos os valores serão permitidos.<br /><br /> (Suporte somente a hierarquias de atributo. O intervalo deve estar em um nível de uma hierarquia. Não há suporte para intervalos não associados no momento.)|  
|Intervalo (Exclusivo)|Um ou dois membros delimitadores de um intervalo|Os valores devem estar entre os membros delimitadores. Se os membros delimitadores forem iguais ou somente um membro for especificado, os valores deve ser maiores que ou menores que o membro delimitador.<br /><br /> (Suporte somente a hierarquias de atributo. O intervalo deve estar em um nível de uma hierarquia. Não há suporte para intervalos não associados no momento.)|  
|MDX|Uma expressão MDX que retorna um conjunto de membros|Os valores devem estar no conjunto de membro calculado. Selecionar esta opção exibe a caixa de diálogo **Construtor de Membro Calculado** para criar expressões MDX.|  
  
 Para hierarquias definidas pelo usuário, nas quais podem ser especificados vários membros na expressão de filtro, todos os membros especificados devem estar no mesmo nível e compartilhar o mesmo pai. Esta restrição não se aplica a hierarquias pai-filho.  
  
## <a name="working-with-data"></a>Trabalhando com dados  
  
##### <a name="drilling-down-into-a-member"></a>Analisando um membro  
 Para analisar um membro específico, clique no sinal de mais (+) ao lado do membro ou clique duas vezes no membro.  
  
##### <a name="slicing-through-cube-dimensions"></a>Fatiando as dimensões do cubo  
 Para filtrar os dados do cubo, clique na caixa de listagem suspensa no título da coluna de nível superior. Você pode expandir a hierarquia e selecionar ou desmarcar um membro em qualquer nível para mostrá-lo ou ocultá-lo e todos os seus descendentes. Desmarque a caixa de seleção ao lado de **(Tudo)** para desmarcar todos os membros na hierarquia.  
  
 Depois que você definir este filtro nas dimensões, poderá ativá-lo e desativá-lo clicando com o botão direito do mouse em qualquer lugar no painel de Dados e clicando em **Filtro Automático**.  
  
##### <a name="filtering-data"></a>Filtrando dados  
 Você pode usar a área de filtro para definir um subcubo no qual navegar. Você pode adicionar um filtro clicando em uma dimensão no painel de Filtro ou expandindo uma dimensão no painel de Metadados e arrastando uma hierarquia para o painel de Filtro. Em seguida, especifique **Operador** e **Expressão de filtro**.  
  
##### <a name="performing-actions"></a>Executando ações  
 Um triângulo marca um título ou célula no painel de Dados para qual há uma ação. Isto pode se aplicar a uma dimensão, nível, membro ou célula de cubo. Mova o ponteiro sobre o objeto do título para ver uma lista de ações disponíveis. Clique no triângulo na célula para exibir um menu e iniciar o processo associado.  
  
 Para segurança, a guia **Navegador** dá suporte somente às seguintes ações:  
  
-   URL  
  
-   Conjunto de linhas  
  
-   Detalhamento  
  
 Não há suporte para ações de linha de comando, de instrução e de propriedade. As ações de URL são tão seguras quanto a página Web à qual estão vinculadas.  
  
##### <a name="viewing-member-properties-and-cube-cell-information"></a>Exibindo as propriedades do membro e as informações de célula do cubo  
 Para exibir informações sobre um objeto de dimensão ou valor de célula, mova o ponteiro sobre a célula.  
  
##### <a name="showing-or-hiding-empty-cells"></a>Mostrando ou ocultando células vazias  
 Você pode ocultar células vazias na grade de dados clicando com o botão direito do mouse em qualquer lugar no painel de Dados e clicando em **Mostrar Células Vazias**.  
  
  
