---
title: Painel de detalhes do Pesquisador de Objetos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.summary.general.f1
- sql13.swb.summary.report.f1
helpviewer_keywords:
- object search [SQL Server], Object Explorer
- Object Explorer
- object search [SQL Server]
- searching objects [SQL Server]
ms.assetid: b963e3c2-dc9e-4d38-bd28-2e00fe9e0e47
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 56cc6461f56dfa21b27a8cb9d7992a0c46627e9c
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095277"
---
# <a name="object-explorer-details-pane"></a>Painel Detalhes do Pesquisador de Objetos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Detalhes do Pesquisador de Objetos, um componente do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], fornece uma exibição tabular de todos os objetos no servidor e apresenta uma interface de usuário para gerenciá-los. Os recursos do Pesquisador de Objetos variam ligeiramente, dependendo do tipo de servidor, mas normalmente incluem recursos de desenvolvimento de bancos de dados e recursos de gerenciamento para todos os tipos de servidor.  
  
Por padrão, o painel Detalhes do Pesquisador de Objetos está visível no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Se não for possível ver o Pesquisador de Objetos, no menu **Exibir** , clique em **Detalhes do Pesquisador de Objetos** ou pressione **F7**.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] exibe datas formatadas com as Opções Regionais e de Idiomas do Microsoft Windows em vigor quando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] foi iniciado. Reinicie o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para refletir as configurações mais novas.  
  
## <a name="object-explorer-details"></a>Detalhes do Pesquisador de Objetos  
Detalhes do Pesquisador de Objetos pode ser usado para navegar por pastas e objetos em sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Em sistemas operacionais de 32 bits, o Pesquisador de Objetos pode exibir apenas 64.000 objetos. Deve ser selecionado um ícone para acessar objetos adicionais.  
  
Detalhes do Pesquisador de Objetos inclui uma barra de ferramentas que contém os ícones descritos na tabela a seguir. Os ícones estão disponíveis apenas quando apropriado.  
  
|Ícone|Ação|  
|--------|----------|  
|**Voltar**|Move para os itens anteriores exibidos em Detalhes do Pesquisador de Objetos. Executa novamente uma pesquisa quando a exibição anterior é o resultado de uma operação de pesquisa.|  
|**Avançar**|Move para a próxima tela depois que uma operação **Voltar** é selecionada.|  
|**Para cima**|Move para o objeto ou a pasta pai.|  
|**Sincronizar**|Define o foco de Pesquisador de Objetos para o objeto selecionado em Detalhes do Pesquisador de Objetos.|  
|**Filter**|Quando disponível, mostra um subconjunto configurável de objetos.|  
|**Atualizar**|Atualiza a exibição em Detalhes do Pesquisador de Objetos.|  
|**Pesquisa**|Fornece uma área para inserir um termo de pesquisa para objetos de banco de dados específicos.|  
  
### <a name="column-header-selections"></a>Seleções de cabeçalho de coluna  
Detalhes do Pesquisador de Objetos possui colunas selecionáveis. Você pode clicar com o botão direito do mouse em qualquer cabeçalho de coluna e pode verificar os itens que deseja exibir. Suas seleções serão persistentes entre os diferentes objetos pelos quais você navega. As seleções de cada usuário são preservadas quando você sai do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e o reinicia.  
  
> [!CAUTION]  
> A exibição de todas as colunas de alguns tipos de objeto (por exemplo, Bancos de Dados) pode tornar a renderização de vídeo um pouco mais lenta para grandes conjuntos de objetos.  
  
### <a name="sorting"></a>Classificação  
Clique uma vez em um cabeçalho de coluna para classificar por essa coluna. Clique novamente no mesmo cabeçalho para classificar a coluna na ordem inversa. As seleções de classificação são mantidas para cada usuário em objetos e pastas e ao reiniciar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] .  
  
### <a name="filtering"></a>Filtragem  
Determinadas listas de objetos exibidos em Detalhes do Pesquisador de Objetos podem ser filtradas usando o ícone **Filtro** na barra de ferramentas Detalhes do Pesquisador de Objetos. O ícone será habilitado quando a filtragem for possível.  
  
### <a name="details-pane"></a>Painel Detalhes  
A área mais inferior de Detalhes do Pesquisador de Objetos contém um painel que exibe determinados detalhes do objeto selecionado. Várias seleções de objetos mostram apenas a contagem dos objetos. Quando houver itens selecionados no painel, clique no ícone **Copiar** para copiar o texto exibido para a área de transferência.  
  
A tecla de seta para baixo move a seleção para o próximo item na lista. A tecla de seta para cima move a seleção para o item anterior na lista. Pressione a tecla de seta para baixo para acelerar a passagem pelos itens. A seleção para na parte inferior ou superior da lista de propriedades.  
  
Digite o primeiro caractere do nome de uma propriedade para passar a seleção para a próxima propriedade que começa com esse caractere.  
  
Quando as propriedades forem organizadas em várias colunas, use as teclas de seta para a esquerda e para a direita para passar para colunas adjacentes.  
  
Para copiar valores de propriedade na área de transferência, use as combinações de teclas seguintes:  
  
-   Ctrl+C copia o valor da propriedade.  
  
-   Ctrl+Shift+C copia o nome e o valor da propriedade com um delimitador tabulações.  
  
Use o menu de clique com o botão direito do mouse no painel de propriedades Detalhes do Pesquisador de Objetos para copiar todas as propriedades ou todas as propriedades e nomes na área de transferência.  
  
Para exibir um valor de propriedade quando a largura de campo não exibir um valor de propriedade completamente, passe o cursor do mouse sobre o valor ou defina o foco de IU no valor de propriedade para ativar uma dica de ferramenta com o valor de propriedade inteiro. Os leitores de tela de acessibilidade relatarão o valor de propriedade completo quando o usuário enfatizar o valor de propriedade longo.  
  
Se o número de propriedades no painel de propriedades exceder esse que se ajustará na área de conteúdo, uma barra de rolagem aparecerá à direita do painel de propriedades. Use a barra de rolagem para ajustar a exibição de valores de propriedade na área de conteúdo.  
  
### <a name="multiple-object-selection"></a>Seleção de vários objetos  
Detalhes do Pesquisador de Objetos dá suporte à seleção de vários objetos. Por exemplo, se você selecionar Tabelas no Pesquisador de Objetos e, na janela Detalhes do Pesquisador de Objetos, mantiver a tecla **Ctrl** pressionada, poderá selecionar várias tabelas, clicar com o botão direito do mouse nelas e selecionar **Excluir** ou **Script de Tabela como** para agir em todas as tabelas selecionadas imediatamente. Os comandos de cópia padrão copiarão o texto exibido para a área de transferência.  
  
## <a name="sql-server-object-search"></a>Pesquisa de objetos do SQL Server  
Curingas  
  
-   Há suporte para os caracteres curinga padrão. Por exemplo, uma pesquisa por **dm_os%counters** retorna dm_os_memory_cache_counters e dm_os_performance_counters. Para obter mais informações, confira [Como pesquisar com curingas](../../relational-databases/scripting/search-text-with-wildcards.md).  
  
Escopo de pesquisa  
  
-   O escopo de cada pesquisa é definido como o foco atual na árvore Pesquisador de Objetos. Por exemplo, se o foco do Pesquisador de Objetos estiver em um banco de dados, uma pesquisa por **dm_os%counters** retornará dm_os_memory_cache_counters e dm_os_performance_counters nesse banco de dados. Se o foco do Pesquisador de Objetos estiver no nó Bancos de Dados, todos os bancos de dados serão pesquisados e várias instâncias das exibições dinâmicas serão retornadas.  
  
Conjuntos grandes  
  
-   A pesquisa de conjuntos de objetos grandes pode levar muito tempo e reduzir o desempenho do servidor.  
  
## <a name="see-also"></a>Consulte Também  
[Pesquisador de Objetos](../../ssms/object/object-explorer.md)  
  
