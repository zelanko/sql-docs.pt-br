---
title: Transformação Pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.lookuptrans.f1
- sql13.dts.designer.lookuptransformation.general.f1
- sql13.dts.designer.lookuptransformation.referencetable.f1
- sql13.dts.designer.lookuptransformation.columns.f1
- sql13.dts.designer.lookuptransformation.advanced.f1
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
ms.openlocfilehash: a866d6224417898b9ed442cb656b9c62f4071297
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726004"
---
# <a name="lookup-transformation"></a>transformação Pesquisa

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A transformação Pesquisa executa pesquisas unindo dados em colunas de entrada com colunas em um conjunto de dados de referência. Você usa a pesquisa para acessar informações adicionais em uma tabela relacionada que tem como base valores de colunas comuns.  
  
 O conjunto de dados de referência pode ser um arquivo de cache, uma tabela ou uma exibição existente, uma nova tabela ou o resultado de uma consulta SQL. A transformação Pesquisa usa um gerenciador de conexões OLE DB ou um gerenciador de conexões de cache para se conectar ao conjunto de dados de referência. Para obter mais informações, consulte [Gerenciador de Conexões do OLE DB](../../../integration-services/connection-manager/ole-db-connection-manager.md) e [Gerenciador de Conexões de Cache](../../../integration-services/data-flow/transformations/cache-connection-manager.md)  
  
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
  
-   Se não houver nenhuma entrada correspondente no conjunto de dados de referência, nenhuma junção ocorrerá. Por padrão, a transformação Pesquisa trata linhas sem entradas correspondentes como erros. No entanto, você pode configurar a transformação Pesquisa para redirecionar essas linhas para uma saída sem-correspondência.  
  
-   Se houver várias correspondências na tabela de referência, a transformação Pesquisa retornará apenas a primeira delas, retornada pela consulta de pesquisa. Se várias correspondências forem encontradas, a transformação Pesquisa gerará um erro ou aviso somente quando a transformação tiver sido configurada para carregar todos os conjuntos de dados de referência no cache. Neste caso, a transformação Pesquisa gera um aviso quando a transformação detecta várias correspondências à medida que ela preenche o cache.  
  
 A junção pode ser composta, o que significa que você pode unir várias colunas na entrada da transformação com colunas no conjunto de dados de referência. A transformação dá suporte às colunas de junção com qualquer tipo de dados, com exceção de DT_R4, DT_R8, DT_TEXT, DT_NTEXT ou DT_IMAGE. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Normalmente, valores do conjunto de dados de referência são adicionados à saída da transformação. Por exemplo, a transformação Pesquisa pode extrair um nome de produto de uma tabela usando um valor de uma coluna de entrada e, em seguida, adicionar esse nome à saída da transformação. Os valores da tabela de referência podem ser substituídos por valores de coluna ou podem ser adicionados a novas colunas.  
  
 As pesquisas executadas pela transformação Pesquisa diferenciam maiúsculas e minúsculas. Para evitar falhas na pesquisa, causadas por diferenças entre maiúsculas e minúsculas nos dados, use primeiro a transformação Mapa de Caracteres para converter os dados em letras maiúsculas ou minúsculas. Depois, inclua as funções UPPER ou LOWER na instrução SQL que gera a tabela de referência. Para obter mais informações, consulte [Transformação de Mapa de Caracteres](../../../integration-services/data-flow/transformations/character-map-transformation.md), [UPPER &#40;Transact-SQL&#41;](../../../t-sql/functions/upper-transact-sql.md) e [LOWER &#40;Transact-SQL&#41;](../../../t-sql/functions/lower-transact-sql.md).  
  
 A transformação Pesquisa tem as seguintes entradas e saídas:  
  
-   Entrada.  
  
-   Saída de correspondência. A saída de correspondência controla as linhas na saída de transformação que correspondem a pelo menos uma entrada no conjunto de dados de referência.  
  
-   Saída sem-correspondência. A saída sem-correspondência controla as linhas na entrada que não correspondem a pelo menos uma entrada no conjunto de dados de referência. Se você configurar a transformação Pesquisa para tratar as linhas sem entradas correspondentes como erros, as linhas serão redirecionadas à saída de erro. Caso contrário, a transformação redirecionará essas linhas para a saída sem-correspondência.  
  
-   Saída de erro.  
  
## <a name="caching-the-reference-dataset"></a>Armazenando o conjunto de dados de referência em cache  
 Um cache na memória armazena o conjunto de dados de referência e uma tabela de hash que indexa os dados. O cache permanece na memória até que a execução do pacote seja concluída. Você pode persistir o cache para um arquivo de cache (.caw).  
  
 Quando você persiste o cache para um arquivo, o sistema carrega esse cache mais rapidamente. Isso melhora o desempenho da transformação Pesquisa e do pacote. Lembre-se de que, quando você usa um arquivo de cache, está trabalhando com dados que não são tão atuais quanto os dados do banco de dados.  
  
 A seguir, veja alguns benefícios adicionais da persistência de cache para um arquivo:  
  
-   ***Compartilhe o arquivo de cache entre vários pacotes. Para obter mais informações, consulte*** [Implementar uma Transformação de Pesquisa em modo de Cache Cheio usando o Gerenciador de Conexões de Cache](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md) ***.***  
  
-   Implante o arquivo de cache com um pacote. ***Você pode usar os dados em vários computadores.*** Para obter mais informações, consulte [Criar e implantar um cache para a Transformação de Pesquisa](../../../integration-services/data-flow/transformations/create-and-deploy-a-cache-for-the-lookup-transformation.md).  
  
-   Use a fonte de arquivos brutos para ler dados do arquivo de cache. Você pode usar outros componentes de fluxo de dados para transformar ou mover os dados. Para obter mais informações, consulte [Raw File Source](../../../integration-services/data-flow/raw-file-source.md).  
  
    > [!NOTE]  
    >  O gerenciador de conexões de cache não dá suporte para arquivos de cache criados ou modificados usando o destino dos arquivos brutos.  
  
-   Execute operações e defina atributos no arquivo de cache usando a tarefa Sistema de Arquivos. Para obter mais informações, consulte [Tarefa do Sistema de Arquivos](../../../integration-services/control-flow/file-system-task.md).  
  
 A seguir, veja as opções de cache:  
  
-   O conjunto de dados de referência é gerado usando uma tabela, exibição ou consulta SQL e carregando no cache, antes da execução da transformação Pesquisa. Use o gerenciador de conexões OLE DB para acessar o conjunto de dados.  
  
     Esta opção de cache é compatível com a opção de cache completo que está disponível para a transformação Pesquisa no [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   O conjunto de dados de referência é gerado a partir de uma fonte de dados conectada ao fluxo de dados ou de um arquivo de cache e é carregado no cache antes da execução da transformação Pesquisa. Use o gerenciador de conexões de cache e, opcionalmente, a transformação Pesquisa para acessar o conjunto de dados. Para obter mais informações, consulte [Editor do Gerenciador de Conexões de Cache](../../../integration-services/data-flow/transformations/cache-connection-manager.md) e [Transformação de Cache](../../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   O conjunto de dados de referência é gerado usando uma tabela, exibição ou consulta SQL durante a execução da transformação Pesquisa As linhas com e sem entradas correspondentes no conjunto de dados de referência são armazenadas em cache.  
  
     Quando o tamanho da memória do cache é excedido, a transformação Pesquisa remove automaticamente as linhas usadas com menos frequência do cache.  
  
     Esta opção de cache é compatível com a opção de cache parcial que está disponível para a transformação Pesquisa no [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   O conjunto de dados de referência é gerado usando uma tabela, exibição ou consulta SQL durante a execução da transformação Pesquisa Nenhum dado é armazenado em cache.  
  
     Esta opção de cache é compatível com a opção sem cache que está disponível para a transformação Pesquisa no [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diferem quanto à forma que comparam cadeias de caracteres. Se a transformação Pesquisa é configurada para carregar o conjunto de dados de referência no cache antes da execução da transformação Pesquisa, o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] faz a comparação de pesquisa no cache. Por outro lado, a operação de pesquisa usa uma instrução SQL parametrizada e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] faz a comparação de pesquisa. Isso significa que a transformação Pesquisa pode retornar um número diferente de correspondências a partir da mesma tabela de consulta, dependendo do tipo de cache.  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente. Para obter mais detalhes, consulte os tópicos a seguir.  
  
-   [Implementar uma pesquisa no modo Sem Cache ou Cache Parcial](../../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [Implementar uma Transformação Pesquisa em modo de Cache cheio usando o Gerenciador de Conexões do Cache](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [Implementar uma transformação Pesquisa em modo de cache cheio por meio da transformação Gerenciador de Conexões OLE DB](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Vídeo, [Como implementar a transformação Pesquisa no modo de Cache Cheio](https://go.microsoft.com/fwlink/?LinkId=131031), em msdn.microsoft.com  
  
-   Entrada de blog, [Práticas recomendadas para usar os modos de cache de transformação de pesquisa](https://go.microsoft.com/fwlink/?LinkId=146623), em blogs.msdn.com  
  
-   Entrada de blog, [Padrão de pesquisa: não diferencia maiúsculas e minúsculas](https://go.microsoft.com/fwlink/?LinkId=157782), em blogs.msdn.com  
  
-   Exemplo [Transformação de Pesquisa](https://go.microsoft.com/fwlink/?LinkId=267528), em msftisprodsamples.codeplex.com.  
  
     Para obter informações sobre como instalar exemplos e bancos de dados de exemplo do produto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , consulte [Exemplos do produto SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=267527).  
  
## <a name="lookup-transformation-editor-general-page"></a>Editor da Transformação Pesquisa (página Geral)
  Use a página **Geral** da caixa de diálogo Editor da Transformação Pesquisa para selecionar o modo de cache, selecionar o tipo de conexão e especificar como lidar com as linhas com entradas sem-correspondência.  
  
### <a name="options"></a>Opções  
 **Cache cheio**  
 Gere e carregue o conjunto de dados de referência no cache antes de executar a transformação Pesquisa.  
  
 **Cache parcial**  
 Gere o conjunto de dados de referência durante a execução da transformação Pesquisa. Carregue as linhas com entradas com correspondência no conjunto de dados de referência e as linhas com entradas sem-correspondência no conjunto de dados no cache.  
  
 **Não cache**  
 Gere o conjunto de dados de referência durante a execução da transformação Pesquisa. Nenhum dado é carregado no cache.  
  
 **Gerenciador de conexões do cache**  
 Configure a transformação Pesquisa para usar um Gerenciador de conexão de cache. Esta opção estará disponível somente se a opção Cache cheio for selecionada.  
  
 **Gerenciador de conexões OLE DB**  
 Configure a transformação Pesquisa para usar um Gerenciador de conexões OLE DB.  
  
 **Especificar como lidar com linhas com entradas sem-correspondência**  
 Selecione uma opção para lidar com as linhas que não correspondem a pelo menos uma entrada no conjunto de dados de referência.  
  
 Ao selecionar **Redirecionar linhas para uma saída sem-correspondência**, as linhas serão redirecionadas a uma saída sem-correspondência e serão tratadas como erros. A opção **Erro** na página **Saída de Erro** da caixa de diálogo **Editor da Transformação Pesquisa** não estará disponível.  
  
 Ao selecionar uma opção na caixa de listas **Especificar como lidar com linhas com entradas sem-correspondência** , as linhas serão tratadas como erros. A opção **Erro** na página **Saída de Erro** estará disponível.  
  
### <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Lookup cache modes](https://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## <a name="lookup-transformation-editor-connection-page"></a>Editor da Transformação Pesquisa (página Conexão)
  Use a página **Conexão** da caixa de diálogo **Editor da Transformação Pesquisa** para selecionar um gerenciador de conexões. Se você selecionar um gerenciador de conexões OLE DB, também poderá selecionar uma consulta, tabela ou exibição para gerar o conjunto de dados de referência.  
  
### <a name="options"></a>Opções  
 As opções a seguir estarão disponíveis quando você selecionar **Cache cheio** e **Gerenciador de conexões de cache** na página Geral da caixa de diálogo **Editor da Transformação Pesquisa** .  
  
 **Gerenciador de conexões de cache**  
 Selecione um gerenciador de conexões de cache existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Editor de Gerenciador de Conexões de Cache** .  
  
 As opções a seguir estarão disponíveis quando você selecionar **Cache cheio**, **Cache parcial**ou **Sem cache**e **Gerenciador de conexões OLE DB**na página Geral da caixa de diálogo **Editor da Transformação Pesquisa** .  
  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Use uma tabela ou exibição**  
 Selecione uma tabela ou exibição existente na lista ou crie uma nova tabela clicando em **Nova**.  
  
> [!NOTE]  
>  Se você especificar uma instrução SQL na página **Avançado** do **Editor da Transformação Pesquisa**, essa instrução SQL vai sobrescrever e substituir o nome da tabela selecionada aqui. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;Página Avançado&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md).  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
 **Usar resultados de uma consulta SQL**  
 Escolha esta opção para navegar até uma consulta preexistente, criar uma nova consulta, verificar a sintaxe da consulta e visualizar os resultados da consulta.  
  
 **Construir consulta**  
 Crie a instrução Transact-SQL a ser executada usando o **Construtor de Consultas**, uma ferramenta gráfica que é usada para criar consultas navegando pelos dados.  
  
 **Procurar**  
 Use esta opção para navegar até uma consulta preexistente salva como um arquivo.  
  
 **Analisar Consulta**  
 Verifique a sintaxe da consulta.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . Esta opção exibe até 200 linhas.  
  
### <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Lookup cache modes](https://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## <a name="lookup-transformation-editor-columns-page"></a>Editor da Transformação Pesquisa (página Colunas)
  Use a página **Colunas** da caixa de diálogo **Editor da Transformação Pesquisa** para especificar a junção entre a tabela de origem e a tabela de referência, e para selecionar as colunas de pesquisa a partir da tabela de referência.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. As colunas de entrada são as colunas no fluxo de dados de uma origem conectada. As colunas de entrada e de pesquisa devem ter tipos de dados correspondentes.  
  
 Use uma operação arrastar e soltar para mapear as colunas de entrada disponíveis para as colunas de pesquisa.  
  
 Você também pode mapear as colunas de entrada para as colunas de pesquisa usando o teclado, destacando a coluna na tabela **Colunas de Entrada Disponíveis** , pressionando a tecla Aplicativo e clicando em **Editar Mapeamentos**.  
  
 **Colunas de Pesquisa Disponíveis**  
 Exiba a lista de colunas de pesquisa. As colunas de pesquisa são as colunas na tabela de referência que permitem pesquisar os valores que correspondem às colunas de entrada.  
  
 Use uma operação arrastar e soltar para mapear as colunas de pesquisa disponíveis para as colunas de entrada.  
  
 Use as caixas de seleção para selecionar as colunas de pesquisa na tabela de referência nas quais serão executadas as operações de pesquisa.  
  
 Você também pode mapear as colunas de pesquisa para as colunas de entrada usando o teclado, destacando a coluna na tabela **Colunas de Pesquisa Disponíveis** , pressionando a tecla Aplicativo e clicando em **Editar Mapeamentos**.  
  
 **coluna de pesquisa**  
 Exiba as colunas de pesquisa selecionadas. As escolhas são refletidas nas caixas de seleção da tabela **Colunas de Pesquisa Disponíveis** .  
  
 **Operação de Pesquisa**  
 Selecione uma operação de pesquisa da lista a ser executada na coluna de pesquisa.  
  
 **Alias de Saída**  
 Digite um alias para a saída de cada coluna de pesquisa. O padrão é o nome da coluna de pesquisa; entretanto, é possível selecionar qualquer nome descritivo exclusivo.  
  
## <a name="lookup-transformation-editor-advanced-page"></a>Editor da Transformação Pesquisa (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor da Transformação Pesquisa** para configurar o cache parcial e para modificar a instrução SQL da transformação Pesquisa.  
  
### <a name="options"></a>Opções  
 **Tamanho de cache (32 bits)**  
 Ajuste o tamanho de cache (em megabytes) para computadores de 32 bits. O valor padrão é 5 megabytes.  
  
 **Tamanho de cache (64 bits)**  
 Ajuste o tamanho de cache (em megabytes) para computadores de 64 bits. O valor padrão é 5 megabytes.  
  
 **Ativar cache para linhas com entradas sem-correspondência**  
 Linhas de cache com entradas sem-correspondência no conjunto de dados de referência.  
  
 **Alocação de cache**  
 Especifique o percentual de cache a ser alocado para as linhas com entradas sem-correspondência no conjunto de dados de referência.  
  
 **Modificar instrução SQL**  
 Modifique a instrução SQL usada para gerar o conjunto de dados de referência.  
  
> [!NOTE]  
>  A instrução SQL opcional especificada nesta página substituirá o nome da tabela especificado na página **Conexão** do **Editor da Transformação Pesquisa**. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;Página Conexão&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md).  
  
 **Definir Parâmetros**  
 Mapeie colunas de entrada para parâmetros usando a caixa de diálogo **Definir Parâmetros da Consulta** .  
  
### <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Lookup cache modes](https://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## <a name="see-also"></a>Consulte Também  
 [Transformação Pesquisa Difusa](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Transformação Pesquisa de Termo](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)   
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
