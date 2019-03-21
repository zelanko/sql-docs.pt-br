---
title: Usar o Assistente para Indexação de Texto Completo | Microsoft Docs
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql13.swb.fulltextindexingwizard.welcome.f1
- sql13.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql13.swb.fulltextindexingwizard.progress.f1
- sql13.swb.fulltextindexingwizard.selectchangetracking.f1
- sql13.swb.fulltextindexingwizard.selectacatalog.f1
- sql13.swb.fulltextindexingwizard.selectatableorview.f1
- sql13.swb.fulltextindexingwizard.selectanindex.f1
- sql13.swb.fulltextindexingwizard.summary.f1
- sql13.swb.fulltextindexingwizard.selecttablecolumns.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 250334bceefa2a3cac6226d32792a8be5ef89206
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973840"
---
# <a name="use-the-full-text-indexing-wizard"></a>Usar o Assistente para Indexação de Texto Completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O Assistente para Indexação de Texto Completo do SSMS descreve uma série de etapas criadas para ajudá-lo a criar um índice de texto completo.  
  
## <a name="create-a--full-text-index"></a>Criar um índice de Texto Completo 

1. No Pesquisador de Objetos, clique com o botão direito do mouse na tabela em que você deseja criar um **Índice de Texto Completo**e clique em **Índice de Texto Completo**. Essa ação inicia o Assistente em uma janela separada.
   Clique em Avançar 
  
2. **Índice Exclusivo.**  Selecione um índice na lista suspensa. O índice deve ser um índice não nulo, exclusivo e de coluna de chave única. Selecione o menor índice de chave exclusiva para a chave exclusiva de texto completo. Para obter um melhor desempenho, é recomendável um índice clusterizado.  
  
3.  **Colunas Disponíveis.** Marque a caixa ao lado de todos os nomes das colunas que você deseja incluir.  caixa de seleção ao lado do nome da coluna. As colunas não qualificadas ficam acinzentadas e suas caixas de seleção desabilitadas.  
  
4. **Idioma do Separador de Palavras.** Selecione um idioma da lista suspensa. Essa seleção será usada para indicar os separadores de palavras corretos para o índice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa separadores de palavras para identificar limites das palavras nos dados de indexação de texto completo.  
  
5.  **Coluna de Tipo.** Selecione o nome da coluna que possui o tipo de documento de coluna que está sendo indexado com texto completo.  
> **OBSERVAÇÃO:** a **Coluna de Tipo** só será habilitada quando a coluna nomeada na coluna **Colunas Disponíveis** for do tipo **varbinary(max)** ou **image**.  
  
6. **Semântica Estatística.** Especifique se habilitará a indexação semântica da coluna selecionada. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
>**OBSERVAÇÕES** 
>
>Se o idioma selecionado não tiver um Modelo de Idioma Semântico associado, a caixa de seleção **Semântica Estatística** não estará habilitada. Se você selecionar **Semântica Estatística** antes de selecionar um **Idioma**, os idiomas disponíveis na caixa de combinação suspensa serão restringidos a esses para os quais o Modelo de Idioma Semântico dá suporte.  
>
> A Pesquisa Semântica **não está disponível para o Banco de Dados SQL do Azure**. A opção Semântica Estatística não será exibida durante a execução desse Assistente em um Banco de Dados SQL do Azure.
  
7. Selecione as opções de controle de alterações.  
  
     **Automaticamente**  
     Selecione esse botão de opção para que o índice de texto completo seja atualizado automaticamente à medida que ocorrem alterações nos dados subjacentes.  
  
     **Manualmente**  
     Selecione esse botão de opção se não deseja que o índice de texto completo seja atualizado automaticamente à medida que ocorrem alterações nos dados subjacentes. São mantidas as alterações nos dados subjacentes. Porém, para aplicar as alterações no índice de texto completo você deve iniciar ou agendar esse processo manualmente.  
  
     **Não rastrear alterações**  
     Selecione esse botão de opção se não deseja que o índice de texto completo seja atualizado com as alterações nos dados subjacentes.  
  
8.  Inicie a população completa quando o índice for criado (disponível somente com a opção Não controlar alterações).
  
     Selecione esse botão de opção para iniciar uma população completa à conclusão com êxito desse assistente. Isso consistirá na criação da estrutura de índice de texto completo no catálogo e em populá-lo com dados indexados de texto completo.  
     
     Clique em Avançar
  
## <a name="catalog-index-filegroup-and-stoplist"></a>Catálogo, grupo de arquivos de índice e lista de palavras irrelevantes   
  
9.  **Selecione o catálogo de texto completo**  

     **Selecionar um catálogo:** Selecione um catálogo de texto completo na lista. O catálogo padrão para o banco de dados será o item selecionado por padrão na lista. Se não houver catálogos disponíveis, a lista permanecerá desabilitada e a caixa de seleção **Criar um novo catálogo** estará marcada e desabilitada.  
  
  OU
  
 10. **Criar um novo catálogo**
 - Selecione o catálogo de texto completo.  
  
    A. **Nome**  
     Insira um nome para o novo catálogo de texto completo.  
  
     B. **Definir como catálogo padrão**  
     Marque para tornar este o catálogo padrão do banco de dados.  
  
     c. **Distinção de acentos**  
     Especifique se o novo catálogo diferenciará caracteres com e sem acentos. Se o banco de dados diferenciar acentos, a opção **Sensível** estará selecionada por padrão.  
  
     d. **Selecionar grupo de arquivos de índice**  
     Especifique o grupo de arquivos no qual criar o índice de texto completo.  
  
     e. Selecione um valor:  
      |Valor|Descrição|  
      |-----------|-----------------|
      |**<default>**| Se a tabela ou exibição não for particionada, selecione para usar o mesmo grupo de arquivos da tabela ou exibição subjacente. Se a tabela ou a exibição for particionada, o grupo de arquivos primário será utilizado|
      |**PRIMARY**|Selecione para usar o grupo de arquivos primário para o novo índice de texto completo.|
      *grupo de arquivos padrão especificado pelo usuário*|Se existir uma lista de palavras irrelevantes padrão definida pelo usuário, selecione o nome na lista para usar esse grupo de arquivos para o novo índice de texto completo.|   
  
     
 11. **Selecionar lista de palavras irrelevantes de texto completo**  
     Especifique uma lista de palavras irrelevantes para usar no índice de texto completo ou desabilitar seu uso.  
  
     As palavras irrelevantes são gerenciadas nos bancos de dados por meio de objetos denominados listas de palavras irrelevantes (stoplists). Uma *lista de palavras irrelevantes (stoplist)* é uma lista que, quando associada a um índice de texto completo, é aplicada às consultas de texto completo desse índice. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
     Selecione um destes valores:  
  
   |Valor|Descrição|  
    |-----------|-----------------|  
    |**<system>**|Selecione para usar a lista de palavras irrelevantes do sistema no novo índice de texto completo. Esse é o padrão.|  
    |**<off>**|Selecione para desabilitar as listas de palavras irrelevantes para o novo índice de texto completo.|  
    |*user-defined-stoplist-name*|A lista exibe o nome de cada lista de palavras irrelevantes definida pelo usuário, se houver alguma, que foi criada no banco de dados. Selecione qualquer lista de palavras irrelevantes definida pelo usuário para usar no novo índice de texto completo.|  
  
  Clique em Avançar
  
11. Opcionalmente, apenas para o SQL Server, defina o agendamento da população. As operações de indexação começarão imediatamente, a menos que tenham sido agendadas para execução futura. Serão criadas agendas imediatamente, embora elas sejam executadas somente na hora agendada.  
  
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
  
  
