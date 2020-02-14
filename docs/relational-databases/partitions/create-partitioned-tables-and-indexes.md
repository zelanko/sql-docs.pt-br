---
title: Criar tabelas e índices particionados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.createpartition.progress.f1
- sql13.swb.createpartition.partitioncolumn.f1
- sql13.swb.createpartition.createjob.f1
- sql13.swb.createpartition.finish.f1
- sql13.swb.createpartition.selectoutput.f1
- sql13.swb.createpartition.partitionfunction.f1
- sql13.swb.createpartition.partitionscheme.f1
- sql13.swb.createpartition.getstart.f1
- sql13.swb.createpartition.mappartition.f1
- sql13.swb.createpartition.summary.f1
helpviewer_keywords:
- partitioned indexes [SQL Server], creating
- partition schemes [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], creating
- partition functions [SQL Server]
- partition schemes [SQL Server]
ms.assetid: 7641df10-1921-42a7-ba6e-4cb03b3ba9c8
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 046ce79c989fdfb24c6615968e6bad951aeb7280
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68024906"
---
# <a name="create-partitioned-tables-and-indexes"></a>Criar tabelas e índices particionados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Você pode criar uma tabela ou um índice particionado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Os dados das tabelas e dos índices particionados são divididos horizontalmente em unidades que podem ser disseminadas por mais de um grupo de arquivos em um banco de dados. O particionamento pode tornar as tabelas e os índices grandes mais gerenciáveis e escalonáveis.  
  
 A criação de uma tabela ou um índice particionado ocorre normalmente em quatro partes:  
  
1.  Crie um grupo ou grupos de arquivos e os arquivos correspondentes que terão as partições especificadas pelo esquema de partição.  
  
2.  Cria uma função de partição que mapeia as linhas de uma tabela ou de um índice em partições com base nos valores de uma coluna especificada.  
  
3.  Cria um esquema de partição que mapeia as partições de uma tabela particionada ou índice para os novos grupos de arquivos.  
  
4.  Crie ou modifique uma tabela ou um índice e especifique o esquema de partição como local de armazenamento.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma tabela ou um índice particionado usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O escopo de uma função e de um esquema de partição é limitado ao banco de dados em que foram criados. No banco de dados, as funções de partição residem em um namespace separado das outras funções.  
  
-   Se alguma linha dentro de uma função de partição tiver colunas de particionamento com valores nulos, essas linhas serão alocadas para a partição à extrema esquerda. No entanto, se NULL for especificado como valor de limite e RIGHT for indicado, a partição extrema esquerda permanecerá vazia e os valores NULL serão colocados na segunda partição.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A criação de uma tabela particionada requer a permissão CREATE TABLE no banco de dados e a permissão ALTER no esquema no qual a tabela está sendo criada. A criação de um índice particionado requer a permissão ALTER na tabela ou exibição onde o índice está sendo criado. A criação de uma tabela ou um índice particionado requer uma das permissões adicionais a seguir:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   Permissão CONTROL ou ALTER no banco de dados no qual a função e o esquema de partição estão sendo criados.  
  
-   Permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual a função e o esquema de partição estão sendo criados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Siga as etapas deste procedimento para criar um ou mais grupos de arquivos, arquivos correspondentes e uma tabela. Você fará referência a esses objetos no próximo procedimento quando criar a tabela particionada.  
  
#### <a name="to-create-new-filegroups-for-a-partitioned-table"></a>Para criar novos grupos de arquivos para uma tabela particionada  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados no qual você deseja criar uma tabela particionada e selecione **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades do Banco de Dados –** *nome_do_banco_de_dados*, em **Selecionar uma página**, selecione **Grupos de arquivos**.  
  
3.  Em **Linhas**, clique em **Adicionar**. Na nova linha, digite o nome do grupo de arquivos.  
  
    > [!WARNING]  
    >  Você deve sempre ter um grupo de arquivos extra, além do número de grupos de arquivos especificado para os valores de limite durante a criação de partições.  
  
4.  Continue adicionando linhas até que você tenha criado todos os grupos de arquivos para a tabela particionada.  
  
5.  Clique em **OK**.  
  
6.  Em **Selecione uma página**, selecione **Arquivos**.  
  
7.  Em **Linhas**, clique em **Adicionar**. Na nova linha, digite um nome de arquivo e selecione um grupo de arquivos.  
  
8.  Continue adicionando linhas até que tenha criado ao menos um arquivo para cada grupo de arquivos.  
  
9. Expanda a pasta **Tabelas** e crie uma tabela como você faz normalmente. Para obter mais informações, veja [Criar tabelas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/create-tables-database-engine.md). Opcionalmente, você pode especificar uma tabela existente no próximo procedimento.  
  
#### <a name="to-create-a-partitioned-table"></a>Para criar uma tabela particionada  
  
1.  Clique com o botão direito do mouse na tabela que você deseja particionar, aponte para **Armazenamento**e clique em **Criar Partição...** .  
  
2.  No **Assistente para Criar Partição**, na página **Bem-vindo ao Assistente para Criar Partição** , clique em **Avançar**.  
  
3.  Na página **Selecione uma Coluna de Particionamento** , na grade **Colunas de particionamento disponíveis** , selecione a coluna em que deseja particionar sua tabela. Somente colunas com tipos de dados que possam ser usados para particionar dados serão exibidas na grade **Colunas de particionamento disponíveis** . Se você selecionar uma coluna computada como a coluna de particionamento, a coluna deverá ser designada como persistente.  
  
     As opções que você tem para as colunas de particionamento e o intervalo de valores são determinadas, basicamente, pela extensão na qual seus dados podem ser agrupados de forma lógica. Por exemplo, você pode optar por dividir seus dados em agrupamentos lógicos por meses ou trimestres de um ano. As consultas que você planejar fazer nos seus dados determinarão se o agrupamento lógico é adequado para o gerenciamento de suas partições de tabela. Todos os tipos de dados são válidos para uso como colunas de particionamento, exceto **text**, **ntext**, **image**, **xml**, **timestamp**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , tipos de dados de alias ou tipos de dados CLR definidos pelo usuário.  
  
     As opções adicionais a seguir estão disponíveis nessa página:  
  
     **Colocar essa tabela na tabela particionada selecionada**  
     Permite selecionar uma tabela particionada que contenha dados relacionados para unir a essa tabela na coluna de particionamento. Tabelas com partições unidas nas colunas de particionamento costumam ser consultadas de forma mais eficiente.  
  
     **Alinhamento de armazenamento de índices não exclusivos e índices exclusivos com uma coluna de partição indexada**  
     Alinha todos os índices da tabela que são particionados com o mesmo esquema de partição. Quando uma tabela e seus índices são alinhados, você pode mover partições para dentro e fora de tabelas particionadas com mais eficiência, pois seus dados são particionados com o mesmo algoritmo.  
  
     Depois de selecionar a coluna de particionamento e as outras opções, clique em **Avançar**.  
  
4.  Na página **Selecione uma Função de Partição** , em **Selecione uma função de partição**, clique em **Nova função de partição** ou em **Função de partição existente**. Se você escolher **Nova função de partição**, digite o nome da função. Se você escolher **Função de partição existente**, selecione o nome da função que você gostaria de usar na lista. A opção **Função de partição existente** não estará disponível se não houver outra função de partição no banco de dados.  
  
     Depois de concluir essa página, clique em **Avançar**.  
  
5.  Na página **Selecione um Esquema de Partição** , em **Selecione um esquema de partição**, clique em **Novo esquema de partição** ou em **Esquema de partição existente**. Se você escolher **Novo esquema de partição**, digite o nome do esquema. Se você escolher **Esquema de partição existente**, selecione o nome do esquema que você gostaria de usar na lista. A opção **Esquema de partição existente** não estará disponível se não houver outro esquema de partição no banco de dados.  
  
     Depois de concluir essa página, clique em **Avançar**.  
  
6.  Na página **Mapear Partições** , em **Intervalo**, selecione **Limite esquerdo** ou **Limite direito** para especificar se é para incluir o maior ou o menor valor de limite dentro de cada grupo de arquivos criado. Você deve sempre inserir um grupo de arquivos extra, além do número de grupos de arquivos especificado para os valores de limite durante a criação de partições.  
  
     Na grade **Selecione os grupos de arquivos e especifique os valores de limite** , em **Grupo de arquivos**, selecione um grupo de arquivos no qual deseja particionar seus dados. Em **Limite**, digite o valor de limite para cada grupo de arquivos. Se o valor de limite ficar em branco, a função de partição mapeará a tabela inteira ou o índice em uma única partição usando o nome da função de partição.  
  
     As opções adicionais a seguir estão disponíveis nessa página:  
  
     **Definir Limites...**  
     Abre a caixa de diálogo **Definir Valores de Limite** para selecionar os valores de limite e os intervalos de datas que deseja para suas partições. Essa opção estará disponível somente quando você tiver selecionado uma coluna de particionamento que contenha um dos seguintes tipos de dados: **date**, **datetime**, **smalldatetime**, **datetime2**ou **datetimeoffset**.  
  
     **Estimar armazenamento**  
     Calcula o número de linhas, o espaço necessário e o espaço disponível para armazenamento para cada grupo de arquivos especificado para as partições. Esses valores são exibidos na grade como valores somente leitura.  
  
     A caixa de diálogo **Definir Valores de Limite** permite as opções adicionais a seguir:  
  
     **Data de início**  
     Seleciona a data inicial para obter os valores de intervalo de suas partições.  
  
     **Data de término**  
     Seleciona a data de término para obter os valores de intervalo de suas partições. Se você selecionar **Limite esquerdo** na página **Mapear Partições** , essa data será o último valor de cada grupo de arquivos/partição. Se você selecionar **Limite direito** na página **Mapear Partições** , essa data será o primeiro valor do próximo ao último grupo de arquivos.  
  
     **Intervalo de datas**  
     Seleciona a granularidade de data ou incremento de valor de intervalo desejado para cada partição.  
  
     Depois de concluir essa página, clique em **Avançar**.  
  
7.  Na página **Selecione uma Opção de Saída** , especifique como você deseja preencher sua tabela particionada. Selecione **Criar Script** para criar um script SQL baseado nas páginas anteriores no assistente. Selecione **Executar imediatamente** para criar a nova tabela particionada depois de concluir todas as páginas restantes no assistente. Selecione **Agenda** para criar uma nova tabela particionada em um momento predeterminado no futuro.  
  
     Se você selecionar **Criar script**, as opções a seguir estarão disponíveis em **Opções de script**:  
  
     **Script para arquivo**  
     Gera o script como um arquivo .sql. Digite um nome de arquivo e o local na caixa **Nome do arquivo** ou clique em **Procurar** para abrir a caixa de diálogo **Local do Arquivo de Script** . Em **Salvar Como**, selecione **Texto Unicode** ou **Texto ANSI**.  
  
     **Script para Área de Transferência**  
     Salva o script na área de transferência.  
  
     **Script para Nova Janela de Consulta**  
     Gera o script para uma nova janela do Editor de Consultas. Essa é a seleção padrão.  
  
     Se você selecionar **Agenda**, clique em **Alterar agenda**.  
  
    1.  Na caixa de diálogo **Nova Agenda de Trabalho**, na caixa **Nome**, digite o nome da agenda de trabalho.  
  
    2.  Na lista **Tipo de Agenda** , selecione o tipo de agenda:  
  
        -   **Iniciar automaticamente quando o SQL Server Agent for iniciado**  
  
        -   **Iniciar sempre que as CPUs estiverem ociosas**  
  
        -   **Recorrente**. Selecione essa opção se sua nova tabela particionada for atualizada com novas informações regularmente.  
  
        -   **Uma vez**. Essa é a seleção padrão.  
  
    3.  Marque ou desmarque a caixa de seleção **Habilitado** para habilitar ou desabilitar a agenda.  
  
    4.  Se você selecionar **Recorrente**:  
  
        1.  Em **Frequência**, na lista **Ocorre** , especifique a frequência de ocorrência:  
  
            -   Se você selecionar **Diário**, na caixa **Ocorre periodicamente a cada** , digite a frequência com que a agenda de trabalho se repete em dias.  
  
            -   Se você selecionar **Semanal**, na caixa **Ocorre periodicamente a cada** , digite a frequência com que a agenda de trabalho se repete em semanas. Selecione o dia ou os dias da semana em que a agenda de trabalho é executada.  
  
            -   Se você selecionar **Mensalmente**, selecione **Dia** ou **O**.  
  
                -   Se você selecionar **Dia**, digite o dia do mês que você deseja que a agenda de trabalho seja executada e a frequência com que a agenda de trabalho se repete em meses. Por exemplo, se desejar que a agenda de trabalho seja executada no 15º dia do mês a cada dois meses, selecione **Dia** e digite "15" na primeira caixa e "2" na segunda caixa. Observe que o maior número permitido na segunda caixa é "99".  
  
                -   Se você selecionar **O**, selecione o dia específico da semana no mês que você deseja que a agenda de trabalho seja executada e a frequência com que a agenda de trabalho se repete em meses. Por exemplo, se você desejar que a agenda de trabalho seja executada no último dia da semana do mês a cada dois meses, selecione **Dia**, selecione **último** na primeira lista e **dia da semana** na segunda lista e depois digite “2” na última caixa. Você também pode selecionar **primeiro**, **segundo**, **terceiro** ou **quarto**, bem como dias específicos da semana (por exemplo: domingo ou quarta-feira) nas primeiras duas listas. Observe que o maior número permitido na última caixa é "99".  
  
        2.  Em **Frequência diária**, especifique a frequência com que a agenda de trabalho se repete no dia da execução da agenda de trabalho:  
  
            -   Se você selecionar **Ocorre uma vez às**, digite a hora específica do dia em que a agenda de trabalho deve ser executada na caixa **Ocorre uma vez às** . Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
            -   Se você selecionar **Ocorre a cada**, especifique a frequência com que a agenda de trabalho é executada durante o dia escolhido em **Frequência**. Por exemplo, se você desejar que o agendamento de trabalho se repita a cada 2 horas durante o dia em que é executado, selecione **Ocorre a cada**, digite "2" na primeira caixa e selecione **hora(s)** na lista. Nessa lista, você pode selecionar também **minuto(s)** e **segundo(s)** . Observe que o maior número permitido na primeira caixa é "100".  
  
                 Na caixa **Iniciando às** , digite a hora em que a agenda de trabalho deve começar a ser executada. Na caixa **Terminando às** , digite a hora em que a agenda de trabalho deve parar de se repetir. Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
        3.  Em **Duração**, em **Data de início**, digite a data que você deseja que a agenda de trabalho inicie a execução. Selecione **Data de término** ou **Nenhuma data de término** para indicar quando a execução da agenda de trabalho deve parar. Se você selecionar **Data de término**, digite a data em que você deseja que a execução da agenda de trabalho pare.  
  
    5.  Se você selecionar **Uma Vez**, em **Ocorrência única**, na caixa **Data** , insira a data em que o agendamento de trabalho será executado. Na caixa **Hora** , digite a hora em que a agenda de trabalho será executada. Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
    6.  Em **Resumo**, em **Descrição**, verifique se todas as configurações da agenda de trabalho estão corretas.  
  
    7.  Clique em **OK**.  
  
     Depois de concluir essa página, clique em **Avançar**.  
  
8.  Na página **Resumo da Revisão** , em **Examinar as seleções**, expanda todas as opções disponíveis para verificar se todas as configurações de partição estão corretas. Se tudo estiver como esperado, clique em **Concluir**.  
  
9. Na página **Progresso do Assistente para Criar Partição** , monitore as informações de status das ações do Assistente para Criar Partição. Dependendo das opções selecionadas no assistente, a página de progresso pode conter uma ou várias ações. A caixa superior exibe o status geral do assistente e o número de mensagens de status, erro e aviso que ele recebeu.  
  
     As opções a seguir estão disponíveis na página **Progresso do Assistente para Criar Partição** :  
  
     **Detalhes**  
     Fornece a ação, status e qualquer mensagem retornada pela ação executada pelo assistente.  
  
     **Ação**  
     Especifica o tipo e o nome de cada ação.  
  
     **Status**  
     Indica se a ação do assistente retornou como um todo o valor de **Êxito** ou de **Falha**.  
  
     **Mensagem**  
     Fornece qualquer mensagem de aviso ou erro retornada pelo processo.  
  
     **Report**  
     Cria um relatório contendo os resultados do Assistente para Criar Partição. As opções são **Exibir Relatório**, **Salvar Relatório no Arquivo**, **Copiar Relatório na Área de Transferência**e **Enviar Relatório como Email**.  
  
     **Exibir Relatório**  
     Abre a caixa de diálogo **Exibir Relatório** , que contém um relatório de texto do progresso do Assistente para Criar Partições.  
  
     **Salvar Relatório no Arquivo**  
     Abre a caixa de diálogo **Salvar Relatório Como** .  
  
     **Copiar Relatório na Área de Transferência**  
     Copia os resultados do relatório de progresso do assistente na Área de transferência.  
  
     **Enviar Relatório como Email**  
     Copia os resultados do relatório de progresso do assistente para uma mensagem de email.  
  
     Quando terminar, clique em **Fechar**.  
  
 O Assistente para Criar Partição cria a função e o esquema de partição e aplica o particionamento à tabela especificada. Para verificar o particionamento da tabela, no Pesquisador de Objetos, clique com o botão direito do mouse na tabela e selecione **Propriedades**. Clique na página **Armazenamento** . A página exibe informações como o nome da função e do esquema de partição e o número de partições.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-partitioned-table"></a>Para criar uma tabela particionada  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria novos grupos de arquivos, uma função e um esquema de partição. Uma nova tabela é criada com o esquema de partição especificado no local de armazenamento.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Adds four new filegroups to the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test1fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test4fg;   
  
    -- Adds one file for each filegroup.  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test1dat1,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat1.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test1fg;  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test2dat2,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t2dat2.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test3dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t3dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test4dat4,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t4dat4.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test4fg;  
    GO  
    -- Creates a partition function called myRangePF1 that will partition a table into four partitions  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
        AS RANGE LEFT FOR VALUES (1, 100, 1000) ;  
    GO  
    -- Creates a partition scheme called myRangePS1 that applies myRangePF1 to the four filegroups created above  
    CREATE PARTITION SCHEME myRangePS1  
        AS PARTITION myRangePF1  
        TO (test1fg, test2fg, test3fg, test4fg) ;  
    GO  
    -- Creates a partitioned table called PartitionTable that uses myRangePS1 to partition col1  
    CREATE TABLE PartitionTable (col1 int PRIMARY KEY, col2 char(10))  
        ON myRangePS1 (col1) ;  
    GO  
    ```  
  
#### <a name="to-determine-if-a-table-is-partitioned"></a>Para determinar se uma tabela é particionada  
  
1.  A consulta a seguir retornará uma ou mais linhas se a tabela `PartitionTable` for particionada. Se a tabela não for particionada, nenhuma linha será retornada.  
  
    ```  
    SELECT *   
    FROM sys.tables AS t   
    JOIN sys.indexes AS i   
        ON t.[object_id] = i.[object_id]   
        AND i.[type] IN (0,1)   
    JOIN sys.partition_schemes ps   
        ON i.data_space_id = ps.data_space_id   
    WHERE t.name = 'PartitionTable';   
    GO  
    ```  
  
#### <a name="to-determine-the-boundary-values-for-a-partitioned-table"></a>Para determinar os valores de limite para uma tabela particionada  
  
1.  A consulta a seguir retorna os valores de limite para cada partição na tabela `PartitionTable` .  
  
    ```  
    SELECT t.name AS TableName, i.name AS IndexName, p.partition_number, p.partition_id, i.data_space_id, f.function_id, f.type_desc, r.boundary_id, r.value AS BoundaryValue   
    FROM sys.tables AS t  
    JOIN sys.indexes AS i  
        ON t.object_id = i.object_id  
    JOIN sys.partitions AS p  
        ON i.object_id = p.object_id AND i.index_id = p.index_id   
    JOIN  sys.partition_schemes AS s   
        ON i.data_space_id = s.data_space_id  
    JOIN sys.partition_functions AS f   
        ON s.function_id = f.function_id  
    LEFT JOIN sys.partition_range_values AS r   
        ON f.function_id = r.function_id and r.boundary_id = p.partition_number  
    WHERE t.name = 'PartitionTable' AND i.type <= 1  
    ORDER BY p.partition_number;  
    ```  
  
#### <a name="to-determine-the-partition-column-for-a-partitioned-table"></a>Para determinar a coluna de partição para uma tabela particionada  
  
1.  A consulta a seguir retorna o nome da coluna de particionamento para a tabela. `PartitionTable`.  
  
    ```  
    SELECT   
        t.[object_id] AS ObjectID   
        , t.name AS TableName   
        , ic.column_id AS PartitioningColumnID   
        , c.name AS PartitioningColumnName   
    FROM sys.tables AS t   
    JOIN sys.indexes AS i   
        ON t.[object_id] = i.[object_id]   
        AND i.[type] <= 1 -- clustered index or a heap   
    JOIN sys.partition_schemes AS ps   
        ON ps.data_space_id = i.data_space_id   
    JOIN sys.index_columns AS ic   
        ON ic.[object_id] = i.[object_id]   
        AND ic.index_id = i.index_id   
        AND ic.partition_ordinal >= 1 -- because 0 = non-partitioning column   
    JOIN sys.columns AS c   
        ON t.[object_id] = c.[object_id]   
        AND ic.column_id = c.column_id   
    WHERE t.name = 'PartitionTable' ;   
    GO  
    ```  
  
 Para obter mais informações, consulte:  
  
-   [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
-   [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)  
  
-   [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  
