---
title: Transformação Pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptrans.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47b04c547700eda94d4c4f19b4a1211f8cdbf694
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386544"
---
# <a name="lookup-transformation"></a>transformação Pesquisa
  A transformação Pesquisa executa pesquisas unindo dados em colunas de entrada com colunas em um conjunto de dados de referência. Você usa a pesquisa para acessar informações adicionais em uma tabela relacionada que tem como base valores de colunas comuns.  
  
 O conjunto de dados de referência pode ser um arquivo de cache, uma tabela ou uma exibição existente, uma nova tabela ou o resultado de uma consulta SQL. A transformação Pesquisa usa um gerenciador de conexões OLE DB ou um gerenciador de conexões de cache para se conectar ao conjunto de dados de referência. Para obter mais informações, consulte [Gerenciador de Conexões do OLE DB](../../connection-manager/ole-db-connection-manager.md) e [Gerenciador de Conexões de Cache](../../connection-manager/cache-connection-manager.md)  
  
 Você pode configurar a transformação Pesquisa das seguintes formas:  
  
-   Selecionando o gerenciador de conexões que deseja usar. Se você quiser se conectar a um banco de dados, selecione um gerenciador de conexões OLE DB. Se desejar se conectar a um arquivo de cache, selecione um gerenciador de conexões de cache.  
  
-   Especificando a tabela ou exibição que contém o conjunto de dados de referência.  
  
-   Gerando um conjunto de dados de referência com a especificação de uma instrução SQL.  
  
-   Especificando junções entre a entrada e o conjunto de dados de referência.  
  
-   Adicionando colunas do conjunto de dados de referência à saída da transformação Pesquisa.  
  
-   Configurando as opções de cache.  
  
 A transformação Pesquisa dá suporte aos seguintes provedores de banco de dados para o gerenciador de conexões OLE DB:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 A transformação Pesquisa tenta executar uma junção por igualdade entre valores na entrada da transformação e valores no conjunto de dados de referência. (Em uma junção por igualdade, cada linha na entrada da transformação deve corresponder a pelo menos uma linha do conjunto de dados de referência.) Se uma junção por igualdade não for possível, a transformação Pesquisa realizará uma das seguintes ações:  
  
-   Se não houver nenhuma entrada correspondente no conjunto de dados de referência, nenhuma junção ocorrerá. Por padrão, a transformação Pesquisa trata linhas sem entradas correspondentes como erros. No entanto, você pode configurar a transformação Pesquisa para redirecionar essas linhas para uma saída sem-correspondência. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;Página Geral&#41;](../../lookup-transformation-editor-general-page.md) e [Editor de Transformação Pesquisa &#40;Página Erro de Saída&#41;](../../lookup-transformation-editor-error-output-page.md).  
  
-   Se houver várias correspondências na tabela de referência, a transformação Pesquisa retornará apenas a primeira delas, retornada pela consulta de pesquisa. Se várias correspondências forem encontradas, a transformação Pesquisa gerará um erro ou aviso somente quando a transformação tiver sido configurada para carregar todos os conjuntos de dados de referência no cache. Neste caso, a transformação Pesquisa gera um aviso quando a transformação detecta várias correspondências à medida que ela preenche o cache.  
  
 A junção pode ser composta, o que significa que você pode unir várias colunas na entrada da transformação com colunas no conjunto de dados de referência. A transformação dá suporte às colunas de junção com qualquer tipo de dados, com exceção de DT_R4, DT_R8, DT_TEXT, DT_NTEXT ou DT_IMAGE. Para obter mais informações, consulte [Integration Services Data Types](../integration-services-data-types.md).  
  
 Normalmente, valores do conjunto de dados de referência são adicionados à saída da transformação. Por exemplo, a transformação Pesquisa pode extrair um nome de produto de uma tabela usando um valor de uma coluna de entrada e, em seguida, adicionar esse nome à saída da transformação. Os valores da tabela de referência podem ser substituídos por valores de coluna ou podem ser adicionados a novas colunas.  
  
 As pesquisas executadas pela transformação Pesquisa diferenciam maiúsculas e minúsculas. Para evitar falhas na pesquisa, causadas por diferenças entre maiúsculas e minúsculas nos dados, use primeiro a transformação Mapa de Caracteres para converter os dados em letras maiúsculas ou minúsculas. Depois, inclua as funções UPPER ou LOWER na instrução SQL que gera a tabela de referência. Para obter mais informações, consulte [Transformação de Mapa de Caracteres](character-map-transformation.md), [UPPER &#40;Transact-SQL&#41;](/sql/t-sql/functions/upper-transact-sql) e [LOWER &#40;Transact-SQL&#41;](/sql/t-sql/functions/lower-transact-sql).  
  
 A transformação Pesquisa tem as seguintes entradas e saídas:  
  
-   Entrada.  
  
-   Saída de correspondência. A saída de correspondência controla as linhas na saída de transformação que correspondem a pelo menos uma entrada no conjunto de dados de referência.  
  
-   Saída sem-correspondência. A saída sem-correspondência controla as linhas na entrada que não correspondem a pelo menos uma entrada no conjunto de dados de referência. Se você configurar a transformação Pesquisa para tratar as linhas sem entradas correspondentes como erros, as linhas serão redirecionadas à saída de erro. Caso contrário, a transformação redirecionará essas linhas para a saída sem-correspondência.  
  
    > [!NOTE]  
    >  No [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)], a transformação Pesquisa tinha apenas uma saída. Para obter mais informações sobre como executar uma transformação de pesquisa que foi criada no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], consulte [atualizar transformações de pesquisa](../../../sql-server/install/upgrade-lookup-transformations.md).  
  
-   Saída de erro.  
  
## <a name="caching-the-reference-dataset"></a>Armazenando o conjunto de dados de referência em cache  
 Um cache na memória armazena o conjunto de dados de referência e uma tabela de hash que indexa os dados. O cache permanece na memória até que a execução do pacote seja concluída. Você pode persistir o cache para um arquivo de cache (.caw).  
  
 Quando você persiste o cache para um arquivo, o sistema carrega esse cache mais rapidamente. Isso melhora o desempenho da transformação Pesquisa e do pacote. Lembre-se de que, quando você usa um arquivo de cache, está trabalhando com dados que não são tão atuais quanto os dados do banco de dados.  
  
 A seguir, veja alguns benefícios adicionais da persistência de cache para um arquivo:  
  
-   ***Compartilhe o arquivo de cache entre vários pacotes. Para obter mais informações, consulte*** [Implementar uma Transformação de Pesquisa em modo de Cache Cheio usando o Gerenciador de Conexões de Cache](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md) ***.***  
  
-   Implante o arquivo de cache com um pacote. ***Você pode usar os dados em vários computadores.*** Para obter mais informações, consulte [Criar e implantar um cache para a Transformação de Pesquisa](create-and-deploy-a-cache-for-the-lookup-transformation.md).  
  
-   Use a fonte de arquivos brutos para ler dados do arquivo de cache. Você pode usar outros componentes de fluxo de dados para transformar ou mover os dados. Para obter mais informações, consulte [Raw File Source](../raw-file-source.md).  
  
    > [!NOTE]  
    >  O gerenciador de conexões de cache não dá suporte para arquivos de cache criados ou modificados usando o destino dos arquivos brutos.  
  
-   Execute operações e defina atributos no arquivo de cache usando a tarefa Sistema de Arquivos. Para obter mais informações, consulte [Tarefa do Sistema de Arquivos](../../control-flow/file-system-task.md).  
  
 A seguir, veja as opções de cache:  
  
-   O conjunto de dados de referência é gerado usando uma tabela, exibição ou consulta SQL e carregando no cache, antes da execução da transformação Pesquisa. Use o gerenciador de conexões OLE DB para acessar o conjunto de dados.  
  
     Esta opção de cache é compatível com a opção de cache completo que está disponível para a transformação Pesquisa no [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   O conjunto de dados de referência é gerado a partir de uma fonte de dados conectada ao fluxo de dados ou de um arquivo de cache e é carregado no cache antes da execução da transformação Pesquisa. Use o gerenciador de conexões de cache e, opcionalmente, a transformação Pesquisa para acessar o conjunto de dados. Para obter mais informações, consulte [Editor do Gerenciador de Conexões de Cache](../../connection-manager/cache-connection-manager.md) e [Transformação de Cache](cache-transform.md).  
  
-   O conjunto de dados de referência é gerado usando uma tabela, exibição ou consulta SQL durante a execução da transformação Pesquisa As linhas com e sem entradas correspondentes no conjunto de dados de referência são armazenadas em cache.  
  
     Quando o tamanho da memória do cache é excedido, a transformação Pesquisa remove automaticamente as linhas usadas com menos frequência do cache.  
  
     Esta opção de cache é compatível com a opção de cache parcial que está disponível para a transformação Pesquisa no [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   O conjunto de dados de referência é gerado usando uma tabela, exibição ou consulta SQL durante a execução da transformação Pesquisa Nenhum dado é armazenado em cache.  
  
     Esta opção de cache é compatível com a opção sem cache que está disponível para a transformação Pesquisa no [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diferem quanto à forma que comparam cadeias de caracteres. Se a transformação Pesquisa é configurada para carregar o conjunto de dados de referência no cache antes da execução da transformação Pesquisa, o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] faz a comparação de pesquisa no cache. Por outro lado, a operação de pesquisa usa uma instrução SQL parametrizada e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] faz a comparação de pesquisa. Isso significa que a transformação Pesquisa pode retornar um número diferente de correspondências a partir da mesma tabela de consulta, dependendo do tipo de cache.  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente. Para obter mais detalhes, consulte os tópicos a seguir.  
  
-   [Implementar uma pesquisa no modo Sem Cache ou Cache Parcial](implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [Implementar uma Transformação Pesquisa em modo de Cache cheio usando o Gerenciador de Conexões do Cache](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [Implementar uma transformação Pesquisa em modo de cache cheio por meio da transformação Gerenciador de Conexões OLE DB](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Vídeo, [Como Implementar uma transformação pesquisa em modo Cache cheio](https://go.microsoft.com/fwlink/?LinkId=131031), em msdn.microsoft.com  
  
-   Entrada de blog, [Práticas recomendadas para usar os modos de cache de transformação de pesquisa](https://go.microsoft.com/fwlink/?LinkId=146623), em blogs.msdn.com  
  
-   Entrada de blog, [padrão de pesquisa: Diferencia maiusculas de minúsculas](https://go.microsoft.com/fwlink/?LinkId=157782), em blogs.msdn.com  
  
-   Exemplo [Transformação de Pesquisa](https://go.microsoft.com/fwlink/?LinkId=267528), em msftisprodsamples.codeplex.com.  
  
     Para obter informações sobre como instalar exemplos e bancos de dados de exemplo do produto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , consulte [Exemplos do produto SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=267527).  
  
## <a name="see-also"></a>Consulte também  
 [Transformação Pesquisa Difusa](fuzzy-lookup-transformation.md)   
 [Transformação Pesquisa de Termo](term-lookup-transformation.md)   
 [Fluxo de Dados](../data-flow.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  
