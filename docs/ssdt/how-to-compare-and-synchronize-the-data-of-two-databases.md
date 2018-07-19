---
title: Como comparar e sincronizar os dados de dois bancos de dados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.data.tools.datacompare.connection.datasources.f1
- sql.data.tools.datacompare.watermark.f1
- sql.data.tools.datacompare.connection.objectselection.f1
ms.assetid: 2148e517-ed42-41c6-b753-1ac625f594c8
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3243a55b0b2897504dbc3d8fd42f94a7ad7f3c95
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093653"
---
# <a name="how-to-compare-and-synchronize-the-data-of-two-databases"></a>Como comparar e sincronizar os dados de dois bancos de dados
Você pode comparar os dados contidos em dois bancos de dados. Os bancos de dados que você compara são conhecidos como *origem* e *destino*.  
  
> [!NOTE]  
> Os *projetos de banco de dados* e os pacotes .dacpac ou .bacpac não podem ser origem ou destino em uma comparação de dados.  
  
À medida que os dados são comparados, um script de DML *(linguagem de manipulação de dados)* é gerado, que você pode usar para sincronizar os bancos de dados diferentes atualizando alguns ou todos os dados no banco de dados de destino. Quando a comparação dos dados terminar, seus resultados aparecerão na janela Comparação de Dados do Visual Studio.  
  
Depois que a comparação tiver sido concluída, você poderá executar outras etapas:  
  
-   Você pode exibir as diferenças entre os dois bancos de dados. Para saber mais, confira [Exibir diferenças de dados](#ViewDifferences).  
  
-   Você pode atualizar todo ou parte do destino para corresponder à origem. Para saber mais, confira [Sincronizar dados do banco de dados](#Synchronize).  
  
Para saber mais, confira [Comparar e sincronizar dados em uma ou mais tabelas com dados em um banco de dados de referência](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md).  
  
> [!NOTE]  
> Você também pode comparar o *esquema* de dois bancos de dados ou de duas versões do mesmo banco de dados. Para saber mais, confira [Como usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md).  
  
## <a name="CompareDatabaseData"></a>Comparar dados do banco de dados  
  
#### <a name="to-compare-data-by-using-the-new-data-comparison-wizard"></a>Para comparar dados usando o Assistente de Nova Comparação de Dados  
  
1.  No menu **SQL**, aponte para **Comparação de Dados** e clique em **Nova Comparação de Dados**.  
  
    O Assistente de Nova Comparação de Dados é exibido. Além disso, a janela Comparação de Dados é aberta e o Visual Studio automaticamente atribui a ela um nome, como DataCompare1.  
  
2.  Identifique os bancos de dados de origem e destino.  
  
    Se a lista **Banco de Dados de Origem** ou **Banco de Dados de Destino** estiver vazia, clique em **Nova Conexão**. Na caixa de diálogo **Propriedades da Conexão**, identifique o servidor no qual o banco de dados reside e o tipo de autenticação a ser usado ao se conectar ao banco de dados. Em seguida, clique em **OK** para fechar a caixa de diálogo **Propriedades de Conexão** e retornar ao assistente de comparação de dados.  
  
    Na primeira página do assistente de comparação de dados, verifique se as informações para cada banco de dados estão corretas, especifique os registros que você deseja incluir nos resultados e clique em **Avançar**. A segunda página do assistente de comparação de dados aparece e exibe uma lista hierárquica de tabelas e exibições no banco de dados.  
  
3.  Marque as caixas de seleção para as tabelas e exibições que você deseja comparar. Opcionalmente, expanda os nós para os objetos de banco de dados e marque as caixas de seleção para as colunas dentro desses objetos que você deseja comparar.  
  
    > [!NOTE]  
    > As tabelas e as exibições devem atender a dois critérios para aparecer na listagem. Primeiro, os esquemas dos objetos devem corresponder entre os bancos de dados de origem e destino. Segundo, somente tabelas e exibições que têm uma chave primária, uma chave exclusiva, um índice exclusivo ou uma restrição exclusiva aparecem na lista. Se nenhuma tabela ou exibição atender a ambos os critérios, a lista ficará vazia.  
  
4.  Se mais de uma chave estiver presente, você poderá usar a coluna **Chave de Comparação** para especificar a chave na qual basear a comparação de dados. Por exemplo, você pode especificar se deseja basear a comparação na coluna de chave primária ou em outra coluna de chave (identificável exclusivamente).  
  
5.  Clique em **Concluir**.  
  
    A comparação inicia.  
  
    > [!NOTE]  
    > Você pode parar uma operação de comparação de dados que esteja em andamento abrindo o menu **SQL**, clicando em **Comparação de Dados** e clicando em **Parar Comparação de Dados**.  
  
    Quando a comparação for concluída, você poderá exibir as diferenças de dados entre os dois bancos de dados. Você também pode atualizar parte ou todos os dados no banco de dados de destino para corresponder aos dados no banco de dados de origem.  
  
#### <a name="to-compare-data-by-using-the-visual-studio-automation-model"></a>Para comparar dados usando o modelo de automação do Visual Studio  
  
1.  Abra o menu **Exibir**, aponte para **Outras Janelas** e clique em **Janela de Comando**.  
  
2.  Na Janela Comando, digite o seguinte comando:  
  
    ```  
    Sql.NewDataComparison /SrcServerName sServerName /SrcDatabaseName sDatabaseName /SrcUserName sUserName /SrcPassword sPassword /SrcDisplayName sDisplayName /TargetServerName tServerName /TargetDatabaseName tDatabaseName /TargeUserName tUserName /TargetPassword tPassword /TargetDisplayName tDisplayName  
    ```  
  
    Substitua os espaços reservados (*sServerName*, *sDatabaseName*, *sUserName*, *sPassword*, *sDisplayName*, *tServerName*, *tDatabaseName*, *tUserName*, *tPassword* e *tDisplayName*) pelos valores para os bancos de dados de origem e de destino.  
  
    Se você não especificar uma origem e um destino, a caixa de diálogo **Nova Comparação de Dados** será exibida. Para saber mais sobre os parâmetros para o comando Sql.NewDataComparison, confira a [Referência de comandos de automação para os recursos do banco de dados do Visual Studio Team System](https://msdn.microsoft.com/en-us/library/dd470565.aspx).  
  
    Os dados nos bancos de dados de origem e destino especificados são comparados. Os resultados aparecem na sessão Comparação de Dados. Para saber mais sobre como exibir resultados ou sincronizar os dados, confira [Exibir diferenças de dados](#ViewDifferences) e [Sincronizar dados do banco de dados](#Synchronize).  
  
## <a name="ViewDifferences"></a>Exibir diferenças de dados  
Depois que você comparar os dados em dois bancos de dados, a Comparação de Dados lista cada *objeto de banco de dados* que você comparou e seu status. Você também pode exibir os resultados para os registros dentro de cada objeto, agrupados por status. Para saber mais sobre o designações de status, confira [Comparar e sincronizar dados em uma ou mais tabelas com dados em um banco de dados de referência](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md).  
  
Depois que você exibir as diferenças, poderá atualizar o destino para corresponder à origem para alguns ou todos os objetos ou registros que forem diferentes, ausentes ou novos. Para saber mais, confira [Sincronizar dados do banco de dados](#Synchronize).  
  
#### <a name="to-view-data-differences"></a>Para exibir diferenças de dados  
  
1.  Compare os dados em um banco de dados de origem e destino. Para saber mais, confira [Comparar dados do banco de dados](#CompareDatabaseData).  
  
2.  (Opcional) Siga um ou ambos destes procedimentos:  
  
    -   Por padrão, os resultados para todos os objetos aparecem, independentemente de seu status. Para exibir apenas os objetos que tiverem um status específico, clique em uma opção na lista **Filtrar**.  
  
    -   Para exibir resultados para registros dentro de um objeto específico, clique no objeto no painel de resultados principal e clique em uma guia no painel da exibição de registros. Cada guia exibe todos os registros dentro desse objeto que têm um status específico: diferente, somente na origem, somente no destino e idêntico. Os dados são exibidos por registro e coluna.  
  
## <a name="Synchronize"></a>Sincronizar dados de bancos de dados  
Depois de comparar os dados em dois bancos de dados, você poderá sincronizá-los atualizando todo ou parte do destino para corresponder à origem. Você pode comparar os dados em dois tipos de objetos de banco de dados: tabelas e exibições.  
  
#### <a name="to-update-target-data-by-using-the-write-updates-command"></a>Para atualizar os dados de destino usando o comando Escrever Atualizações  
  
1.  Compare os dados em um banco de dados de origem e destino. Para saber mais, confira [Comparar dados do banco de dados](#CompareDatabaseData).  
  
    Depois que a comparação tiver sido concluída, a janela Comparação de Dados listará os resultados para os objetos que foram comparados. Quatro colunas (Registros Diferentes, Somente na Origem, Somente no Destino e Registros Idênticos) exibem informações sobre os objetos que não foram idênticos. Para cada um objeto, essas colunas exibem quantos registros diferentes foram localizados e quantos registros uma operação de atualização alteraria. Esses dois números correspondem inicialmente, mas, na etapa 4, você pode alterar quais objetos serão atualizados.  
  
    Para saber mais, confira [Comparar e sincronizar dados em uma ou mais tabelas com dados em um banco de dados de referência](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md).  
  
2.  Na tabela da janela Comparação de Dados, clique em uma linha.  
  
    O painel de detalhes mostra resultados para os registros no objeto de banco de dados em que você clicou. Os registros são agrupados por status em guias, que você pode usar para especificar os dados que serão propagados da origem para o destino.  
  
3.  No painel de detalhes, clique em uma guia cujo nome contém um número diferente de zero (0).  
  
    A coluna **Atualizar** da tabela **Somente no Destino** contém as caixas de seleção que você pode usar para selecionar as linhas a serem atualizadas. Por padrão, cada caixa de seleção é marcada.  
  
4.  Desmarque as caixas de seleção para registros no destino que você não deseja atualizar com os dados de origem.  
  
    Quando você desmarca uma caixa de seleção, reduz o número de registros para atualizar e a exibição é alterada para refletir as suas ações. Este número é exibido na linha de status do painel de detalhes e na coluna correspondente no painel de resultados principal, conforme descrito na etapa 1.  
  
5.  (Opcional) Clique em **Gerar Script**.  
  
    Uma janela do editor de Transact\-SQL é aberta e mostra o script de DML *(linguagem de manipulação de dados)* que seria usado para atualizar o destino.  
  
6.  Para sincronizar os registros que são diferentes, ausentes ou novos, clique em **Atualizar Destino**.  
  
    > [!NOTE]  
    > Enquanto o banco de dados de destino está sendo atualizado, você poderá cancelar a operação clicando em **Parar Gravação no Destino**.  
  
    Os dados dos registros selecionados no destino são atualizados com os dados dos registros correspondentes na origem.  
  
    > [!NOTE]  
    > Se você quiser atualizar as exibições indexadas, a operação **Atualizar Destino** poderá falhar se essa ação fizer as chaves duplicadas serem inseridas na mesma tabela.  
  
#### <a name="to-update-target-data-by-using-a-transact-sql-script"></a>Para atualizar os dados de destino usando um script de Transact\-SQL  
  
1.  Compare os dados em um banco de dados de origem e destino. Para saber mais, confira [Comparar dados do banco de dados](#CompareDatabaseData).  
  
    Depois que a comparação tiver sido concluída, a janela Comparação de Dados listará os objetos que foram comparados. Para saber mais, confira [Comparar e sincronizar dados em uma ou mais tabelas com dados em um banco de dados de referência](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md).  
  
2.  (Opcional) No painel de detalhes, desmarque as caixas de seleção para os registros no destino que você não deseja atualizar, conforme descrito no procedimento anterior.  
  
3.  Clique em **Gerar Script**.  
  
    Uma nova janela mostra o script de Transact\-SQL que propagaria as alterações necessárias para fazer os dados no destino corresponderem aos dados na origem. A nova janela recebe um nome, por exemplo, **DataUpdate_Database_1.sql**.  
  
    Esse script reflete as alterações feitas no painel de detalhes. Por exemplo, talvez você tenha desmarcado uma caixa de seleção para uma determinada linha na página Somente no Destino para a tabela [dbo].[Shippers]. Nesse caso, o script não atualizaria essa linha.  
  
4.  (Opcional) Edite esse script na janela **DataUpdate_Database_1.sql**.  
  
5.  (Opcional, mas recomendado) Faça o backup do banco de dados de destino.  
  
6.  Clique em **Executar** para atualizar o banco de dados de destino.  
  
    Especifique uma conexão com o banco de dados de destino que você deseja atualizar.  
  
    > [!IMPORTANT]  
    > Por padrão, as atualizações ocorrem dentro do escopo de uma transação. Se ocorrerem erros, você poderá reverter a atualização inteira. É possível alterar esse comportamento.  
  
    Os dados dos registros selecionados no destino são atualizados com os dados dos registros correspondentes na origem.  
  
## <a name="see-also"></a>Consulte Também  
[Comparar e sincronizar dados em uma ou mais tabelas com dados em um banco de dados de referência](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)  
  
