---
title: Usar o Assistente para Indexação de Texto Completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextindexingwizard.selecttablecolumns.f1
- sql12.swb.fulltextindexingwizard.welcome.f1
- sql12.swb.fulltextindexingwizard.selectacatalog.f1
- sql12.swb.fulltextindexingwizard.progress.f1
- sql12.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql12.swb.fulltextindexingwizard.selectatableorview.f1
- sql12.swb.fulltextindexingwizard.selectchangetracking.f1
- sql12.swb.fulltextindexingwizard.selectanindex.f1
- sql12.swb.fulltextindexingwizard.summary.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f7bab4ee8f03eb666e1a8396fbf8957b1e42f2c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010896"
---
# <a name="use-the-full-text-indexing-wizard"></a>Usar o Assistente para Indexação de Texto Completo
  O Assistente para Indexação de Texto Completo guia você por uma série de etapas planejadas para ajudá-lo a criar um índice de texto completo.  
  
#### <a name="to-use-the-full-text-indexing-wizard"></a>Para usar o Assistente para Indexação de Texto Completo  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela em que você deseja criar um **Índice de Texto Completo**e clique em **Índice de Texto Completo**.  
  
     **Índice exclusivo**  
     Selecione um índice na lista suspensa. O índice deve ser um índice não nulo, exclusivo e de coluna de chave única. Selecione o menor índice de chave exclusiva para a chave exclusiva de texto completo. Para obter um melhor desempenho, é recomendável um índice clusterizado.  
  
     **Colunas disponíveis**  
     Para incluir uma coluna no índice, marque a caixa de seleção do lado do nome da coluna. As colunas que não são qualificadas para indexação de texto completo aparecem em cinza com suas caixas de seleção desabilitadas.  
  
     **Idioma do separador de palavras**  
     Selecione um idioma da lista suspensa. Essa seleção será usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para indicar os separadores de palavras corretos para o índice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa separadores de palavras para identificar limites das palavras nos dados de indexação de texto completo.  
  
     **Coluna de tipo**  
     Selecione o nome da coluna que possui o tipo de documento de coluna que está sendo indexado com texto completo.  
  
     O **coluna de tipo** é habilitado apenas quando a coluna nomeada na **colunas disponíveis** coluna é do tipo `varbinary(max)` ou `image`.  
  
     **Semântica Estatística**  
     Especifique se habilitará a indexação semântica da coluna selecionada. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](semantic-search-sql-server.md).  
  
     Se você selecionar um **Idioma** antes de selecionar **Semântica Estatística**, e o idioma selecionado não tiver um Modelo de Idioma Semântico associado, a caixa de seleção **Semântica Estatística** será desabilitada. Se você selecionar **Semântica Estatística** antes de selecionar um **Idioma**, os idiomas disponíveis na caixa de combinação suspensa serão restringidos a esses para os quais o Modelo de Idioma Semântico dá suporte.  
  
2.  Selecione as opções de controle de alterações.  
  
     **Automaticamente**  
     Selecione esse botão de opção para que o índice de texto completo seja atualizado automaticamente à medida que ocorrem alterações nos dados subjacentes.  
  
     **Manualmente**  
     Selecione esse botão de opção se não deseja que o índice de texto completo seja atualizado automaticamente à medida que ocorrem alterações nos dados subjacentes. São mantidas as alterações nos dados subjacentes. Porém, para aplicar as alterações no índice de texto completo você deve iniciar ou agendar esse processo manualmente.  
  
     **Não rastrear alterações**  
     Selecione esse botão de opção se não deseja que o índice de texto completo seja atualizado com as alterações nos dados subjacentes.  
  
     **Iniciar população completa quando o índice é criado**  
     Selecione esse botão de opção para iniciar uma população completa à conclusão com êxito desse assistente. Isso consistirá na criação da estrutura de índice de texto completo no catálogo e em populá-lo com dados indexados de texto completo.  
  
3.  Selecione o catálogo, o grupo de arquivos de índice e a lista de palavras irrelevantes (stoplist).  
  
     **Selecione o catálogo de texto completo**  
     Selecione um catálogo de texto completo na lista. O catálogo padrão para o banco de dados será o item selecionado por padrão na lista. Se não houver catálogos disponíveis, a lista permanecerá desabilitada e a caixa de seleção **Criar um novo catálogo** estará marcada e desabilitada.  
  
    |||  
    |-|-|  
    |**Criar um novo catálogo**|Marque essa caixa de seleção para criar um novo catálogo de texto completo.|  
  
     **Nome**  
     Digite um nome para o novo catálogo de texto completo.  
  
     **Definir como catálogo padrão**  
     Marque para tornar este o catálogo padrão do banco de dados.  
  
     **Distinção de acentos**  
     Especifique se o novo catálogo diferenciará caracteres com e sem acentos. Se o banco de dados distinguir acentos, por padrão, **Com Distinção** será selecionado.  
  
     **Selecionar grupo de arquivos de índice**  
     Especifique o grupo de arquivos no qual criar o índice de texto completo.  
  
     Selecione um destes valores:  
  
    |Valor|Descrição|  
    |-----------|-----------------|  
    |**\<default>**|Se a tabela ou exibição não for particionada, selecione para usar o mesmo grupo de arquivos da tabela ou exibição subjacente. Se a tabela ou exibição for particionada, o grupo de arquivos primário será utilizado.|  
    |**PRIMARY**|Selecione para usar o grupo de arquivos primário para o novo índice de texto completo.|  
    |*grupo de arquivos padrão especificado pelo usuário*|Se existir uma lista de palavras irrelevantes padrão definida pelo usuário, selecione seu nome na lista para usar esse grupo de arquivos para o novo índice de texto completo.|  
  
     **Selecionar lista de palavras irrelevantes de texto completo**  
     Especifique uma lista de palavras irrelevantes para usar no índice de texto completo ou desabilitar seu uso.  
  
     No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e nas versões posteriores, as palavras irrelevantes (stopwords) são gerenciadas em bancos de dados por meio de objetos chamados listas de palavras irrelevantes. Uma *lista de palavras irrelevantes (stoplist)* é uma lista que, quando associada a um índice de texto completo, é aplicada às consultas de texto completo desse índice. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
     Selecione um destes valores:  
  
    |Valor|Descrição|  
    |-----------|-----------------|  
    |**\<system>**|Selecione para usar a lista de palavras irrelevantes do sistema no novo índice de texto completo. Esse é o padrão.|  
    |**\<off>**|Selecione para desabilitar as listas de palavras irrelevantes para o novo índice de texto completo.|  
    |*user-defined-stoplist-name*|A lista exibe o nome de cada lista de palavras irrelevantes definida pelo usuário, se houver alguma, que foi criada no banco de dados. Selecione qualquer lista de palavras irrelevantes definida pelo usuário para usar no novo índice de texto completo.|  
  
4.  Opcionalmente, defina a agenda de população. As operações de indexação começarão imediatamente, a menos que tenham sido agendadas para execução futura. Serão criadas agendas imediatamente, embora elas sejam executadas somente na hora agendada.  
  
     **Nova Agenda de Tabela**  
     Defina uma agenda de população para uma tabela.  
  
     **Nova Agenda do Catálogo**  
     Defina uma agenda de população para um catálogo de texto completo.  
  
     **Editar**  
     Edite uma agenda.  
  
     **Delete (excluir)**  
     Exclua uma agenda.  
  
5.  Exiba ou controle o progresso do Assistente de Indexação de Texto Completo.  
  
     **Parar**  
     Interrompe a operação atual e impede que sejam executadas operações de texto completo subsequentes pelo assistente durante esta sessão.  
  
     **Relatório**  
     Quando todas as operações terminarem de executar, clique nesse botão para acessar um relatório sobre as operações executadas. Você pode exibir o relatório, imprimi-lo em um arquivo, copiá-lo na área de transferência ou enviá-lo por email.  
  
  
