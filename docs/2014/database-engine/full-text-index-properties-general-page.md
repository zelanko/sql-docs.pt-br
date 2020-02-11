---
title: Propriedades do índice de texto completo (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.general.f1
ms.assetid: f4dff61c-8c2f-4ff9-abe4-70a34421448f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a240ed4e3788d65ab795d8680dc93f253cfde059
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62778937"
---
# <a name="full-text-index-properties-general-page"></a>Propriedades do Índice de Texto Completo (página Geral)
  **Para exibir ou alterar as propriedades modificáveis de um índice de texto completo**  
  
-   [Gerenciar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Catálogo de texto completo**  
 Exibe o nome do catálogo de texto completo ao qual o índice de texto completo está associado.  
  
 **Backup de banco de dados**  
 Exibe o nome do banco de dados no qual o índice de texto completo reside.  
  
 **Table**  
 Exibe o nome da tabela na qual o índice de texto completo está definido.  
  
 **Chave de Índice de Texto Completo**  
 Exibe o nome da chave de índice de texto completo, que é um índice exclusivo em uma única coluna da tabela.  
  
 **Status da População de Texto Completo da Tabela**  
 Exibe o status da população da tabela indexada de texto completo.  
  
 Os valores possíveis são os seguintes:  
  
 0 = Ocioso  
  
 1 = População completa em andamento.  
  
 2 = População incremental em andamento.  
  
 3 = Propagação de alterações controladas em andamento.  
  
 4 = Índice de atualização em segundo plano em andamento, como o controle de alteração automática.  
  
 5 = Indexação de texto completo acelerado ou pausado.  
  
 **Índice de Texto Completo Ativo**  
 Indica se a tabela tem um índice de texto completo ativo.  
  
 1 = True  
  
 0 = False  
  
 **Grupo de arquivos do índice de texto completo**  
 O grupo de arquivos ao qual o índice de texto completo pertence.  
  
 **Lista de palavras irrelevantes de índice de texto completo**  
 A lista de palavras irrelevantes associada ao índice de texto completo no momento. Uma lista de palavras irrelevantes contém [palavras irrelevantes](../relational-databases/search/full-text-search.md). A lista de palavras irrelevantes associada a um índice de texto completo, se houver, é aplicada a consultas de texto completo nesse índice. Você pode remover a lista de palavras irrelevantes do índice selecionando ** \<desativado>** na listagem ou pode selecionar uma diferente lista de palavras irrelevantes; O sistema>indica a System STOPLIST. ** \<**  
  
 **Par criar uma lista de palavras irrelevantes (stoplist)**  
  
-   [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../relational-databases/search/full-text-search.md)  
  
 **Lista de propriedades de pesquisa**  
 A lista de propriedades de pesquisa associada atualmente o índice de texto completo, se houver algum. Uma lista de propriedades de pesquisa especifica um conjunto de propriedades de documento que são incluídos no índice de texto completo quando ele é preenchido. Para obter mais informações, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 Off>indica que atualmente não há nenhuma lista de propriedades de pesquisa associada ao índice. ** \<** Você pode remover a lista de propriedades de pesquisa atual do índice selecionando ** \<desativado>** na lista ou pode selecionar uma lista de propriedades de pesquisa diferente na lista. Somente as listas de propriedades de pesquisa do banco de dados atual são relacionadas aqui.  
  
> [!NOTE]  
>  Você pode associar uma determinada lista de propriedades de pesquisa a mais de um índice de texto completo no mesmo banco de dados.  
  
 **Para criar uma lista de propriedades de pesquisa**  
  
-   [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
 **Contagem de Itens de Texto Completo da Tabela**  
 Indica o número de linhas com indexação de texto completo bem-sucedida.  
  
 Essa propriedade corresponde à propriedade `TableFulltextItemCount` retornada pela função [!INCLUDE[tsql](../includes/tsql-md.md)] OBJECTPROPERTYEX.  
  
 **Documentos de Texto Completo da Tabela Processados**  
 Exibe o número de linhas processadas desde o início da indexação de texto completo. Em uma tabela que está sendo indexada para pesquisa de texto completo, todas as colunas de uma linha são consideradas parte de um documento a ser indexado. Linhas excluídas não são contadas.  
  
|||  
|-|-|  
|0|Indica que a indexação de texto completo está concluída e que não há população ativa.|  
|> 0|Para uma população ativa, indica o número de documentos processados pelas operações de inserção ou de atualização desde qualquer uma das seguintes opções: uma população, a habilitação do controle de alterações com população de índice de atualização em segundo plano (como controle de alterações automáticas), a alteração do esquema de índice de texto completo, a reconstrução do catálogo de texto completo, o reinício da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], etc.|  
  
 **Alterações de Texto Completo Pendentes da Tabela**  
 Número de entradas de controle de alterações pendentes a serem processadas.  
  
 0 = o controle de alterações não está habilitado.  
  
 NULL = A tabela não tem um índice de texto completo.  
  
 **Contagem de Falhas de Texto Completo da Tabela**  
 O número de linhas que a pesquisa de texto completo não indexou.  
  
 0 = A população foi concluída.  
  
 \>0 = um dos seguintes:  
  
-   O número de documentos que não foram indexados desde o início da população do controle de alterações completa, incremental ou manual.  
  
-   Para o controle de alterações com índice de atualização em segundo plano, o número de linhas que não foram indexadas desde o início ou reinício da população. A causa disso pode ter sido uma alteração de esquema, a reconstrução do catálogo, a reinicialização do servidor e assim por diante.  
  
 **Indexação de texto completo habilitada**  
 Especifica se a indexação de texto completo está habilitada.  
  
|||  
|-|-|  
|**Verdadeiro**|habilitado|  
|**Falso**|Desabilitado|  
  
 **Controle de alterações**  
 Especifica se a tabela tem o controle de alterações de texto completo habilitado, e nesse caso, de que tipo. O controle de alterações de texto completo mantém um registro das linhas que foram modificadas em uma tabela ou a exibição indexada que foi configurada para indexação de texto completo. Essas alterações podem ser propagadas para o índice de texto completo.  
  
 Os valores do **Controle de Alterações** são os seguintes:  
  
|||  
|-|-|  
|**Desconto**|O índice de texto completo não é atualizado com alterações nos dados subjacentes.|  
|**Manual**|O índice de texto completo não é atualizado automaticamente conforme as alterações ocorrem nos dados subjacentes. Porém, as alterações aos dados subjacentes são mantidas e você pode propagá-los para o índice de texto completo ou em uma agenda que usa o SQL Server Agent ou manualmente.|  
|**Automático**|O índice de texto completo é atualizado automaticamente conforme as alterações ocorrem nos dados subjacentes na tabela base.|  
  
 **Repopular o índice**  
 Clique para iniciar uma população no índice de texto completo ao sair da caixa de diálogo. Selecione um dos seguintes tipos de população:  
  
|||  
|-|-|  
|**Full**|Durante uma população completa de uma tabela, as entradas de índice são criadas para todas as linhas.|  
|**Lucrativ**|A população incremental atualiza o índice de texto completo para linhas adicionadas, excluídas ou modificadas após a última população ou enquanto a última população estava em andamento. A execução de uma população incremental requer que a tabela base contenha uma coluna do tipo de dados `timestamp`.|  
|**Cumulativo**|O índice de texto completo é atualizado sempre que os dados da tabela base são modificados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar a pesquisa de texto completo](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
