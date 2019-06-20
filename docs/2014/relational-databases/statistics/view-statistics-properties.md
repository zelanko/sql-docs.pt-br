---
title: Exibir propriedades de estatísticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.statistics.details.f1
helpviewer_keywords:
- viewing statistics properties
- statistics [SQL Server], viewing properties
ms.assetid: 0eaa2101-006e-4015-9979-3468b50e0aaa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8db42e567b80ca282b89d9be29fffff3e643ea7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015643"
---
# <a name="view-statistics-properties"></a>Exibir propriedades de estatísticas
  Você pode exibir estatísticas de otimização de consulta atuais para uma tabela ou exibição indexada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Os objetos de estatísticas incluem um cabeçalho com metadados sobre as estatísticas, um histograma com a distribuição de valores na primeira coluna de chave do objeto de estatísticas e um vetor de densidade para medir a correlação entre colunas. Para obter mais informações sobre histogramas e vetores de densidade, consulte [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql)  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir propriedades de estatísticas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para exibir o objeto de estatísticas, o usuário deve ser proprietário da tabela ou deve ser membro da função de servidor fixa `sysadmin` ou das funções de banco de dados fixas `db_owner` ou `db_ddladmin`.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-statistics-properties"></a>Para exibir propriedades de estatísticas  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o banco de dados no qual você deseja criar uma nova estatística.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja exibir as propriedades de estatísticas.  
  
4.  Clique no sinal de adição para expandir a pasta **Estatísticas** .  
  
5.  Clique com o botão direito do mouse no objeto de Estatísticas do qual você deseja exibir as propriedades e selecione **Propriedades**.  
  
6.  Na caixa de diálogo **Propriedades de Estatísticas -** _statistics_name_ , no painel **Selecionar uma página** , selecione **Detalhes**.  
  
     As propriedades a seguir são mostradas na página **Detalhes** na caixa de diálogo **Propriedades de Estatísticas -** _statistics_name_ .  
  
     **Nome da tabela**  
     Exibe o nome da tabela descrito pelas estatísticas.  
  
     **Nome das Estatísticas**  
     Exibe o nome do objeto de banco de dados onde as estatísticas são armazenadas.  
  
     **Estatísticas para INDEXstatistics_name**  
     Esta caixa de texto mostra as propriedades retornadas do objeto de estatísticas. Essas propriedades são divididas em três seções: Cabeçalho de Estatísticas, Vetor de Densidade e Histograma.  
  
     As informações a seguir descrevem as colunas retornadas no conjunto de resultados do Cabeçalho de Estatísticas.  
  
     **Nome**  
     O nome do objeto de estatísticas.  
  
     **Atualizado**  
     Data e hora da última atualização de estatísticas.  
  
     **Linhas**  
     O número total de linhas na tabela ou exibição indexada quando as estatísticas foram atualizadas pela última vez. Se as estatísticas forem filtradas ou corresponderem a um índice filtrado, o número de linhas talvez seja menor do que o número de linhas na tabela.  
  
     **Linhas Amostradas**  
     O número total de linhas amostradas para cálculos de estatísticas. Se Linhas Amostradas < Linhas, o histograma e os resultados de densidade exibidos serão estimativas com base nas linhas amostradas.  
  
     **Etapas**  
     O número de etapas no histograma. Cada etapa abrange uma gama de valores de colunas seguidos por um valor de coluna associada superior. As etapas do histograma são definidas na primeira coluna de chave nas estatísticas. O número máximo de etapas é 200.  
  
     **Densidade**  
     Calculado como 1 / *valores distintos* para todos os valores na primeira coluna de chave do objeto de estatísticas, excluindo os valores de limite de histograma. Esse valor de Densidade não é usado pelo otimizador de consulta e é exibido para fins de compatibilidade com versões anteriores ao SQL Server 2008.  
  
     **Comprimento Médio de Chave**  
     O número médio de bytes por valor para todas as colunas de chave do objeto de estatísticas.  
  
     **Índice de Cadeia de Caracteres**  
     Sim indica que o objeto de estatísticas contém estatísticas do resumo da cadeia de caracteres para melhorar a estimativa de cardinalidade para predicados de consulta que usam o operador LIKE; por exemplo, `WHERE ProductName LIKE '%Bike'`. As estatísticas de resumo da cadeia de caracteres são armazenadas separadamente do histograma e são criadas na primeira coluna de chave do objeto de estatísticas quando ele é do tipo **char**, **varchar**, **nchar**, **nvarchar**, **varchar(max)**, **nvarchar(max)**, **text**ou **ntext**.  
  
     **Expressão de filtro**  
     Predicado do subconjunto de linhas de tabela incluído no objeto de estatísticas. NULL = estatísticas não filtradas.  
  
     **Linhas não filtradas**  
     O número total de linhas na tabela antes da aplicação da expressão de filtro. Se o valor da Expressão de Filtro for NULL, as Linhas Não Filtradas serão iguais a Linhas.  
  
     As informações a seguir descrevem as colunas retornadas no conjunto de resultados do Vetor de Densidade.  
  
     **Toda Densidade**  
     A densidade é 1 / *valores distintos*. Os resultados exibem a densidade de cada prefixo de colunas no objeto de estatísticas, uma linha por densidade. Um valor distinto é uma lista distinta dos valores de coluna por linha e por prefixo de colunas. Por exemplo, se o objeto de estatísticas contiver colunas de chave (A, B, C), os resultados reportarão a densidade de listas distintas de valores em cada um desses prefixos de colunas: (A), (A, B) e (A, B, C). Usando o prefixo (A, B, C), cada uma dessas listas é uma lista de valores distintos: (3, 5, 6), (4, 4, 6), (4, 5, 6), (4, 5, 7). Usando o prefixo (A, B) os mesmos valores de coluna têm estas listas de valores distintos: (3, 5), (4, 4) e (4, 5).  
  
     **Comprimento Médio**  
     O comprimento médio, em bytes, para armazenar uma lista dos valores das colunas para o prefixo da coluna. Por exemplo, se os valores na lista (3, 5, 6) exigirem cada um 4 bytes, o comprimento será de 12 bytes.  
  
     **Colunas**  
     Os nomes das colunas no prefixo para o qual as opções Toda a densidade e Comprimento médio são exibidos.  
  
     As informações a seguir descrevem as colunas retornadas no conjunto de resultados do Histograma.  
  
     **RANGE_HI_KEY**  
     Valor da coluna associada superior de uma etapa do histograma. O valor da coluna também será denominado um valor de chave.  
  
     **RANGE_ROWS**  
     Número estimado de linhas cujo valor de coluna fica dentro de uma etapa do histograma, excluindo-se o limite superior.  
  
     **EQ_ROWS**  
     Número estimado de linhas cujo valor de coluna é igual ao limite superior da etapa do histograma.  
  
     **DISTINCT_RANGE_ROWS**  
     Número estimado de linhas com um valor de coluna distinto dentro de uma etapa do histograma, excluindo-se o limite superior.  
  
     **AVG_RANGE_ROWS**  
     Número médio de linhas com valores de colunas duplicados em uma etapa do histograma, excluindo o limite superior (RANGE_ROWS / DISTINCT_RANGE_ROWS para DISTINCT_RANGE_ROWS > 0).  
  
7.  Clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-statistics-properties"></a>Para exibir propriedades de estatísticas  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example displays all statistics information for the AK_Address_rowguid index of the Person.Address table.   
    DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid);   
    GO  
    ```  
  
 Para obter mais informações, veja [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql).  
  
#### <a name="to-find-all-of-the-statistics-on-a-table-or-view"></a>Para localizar todas as estatísticas em uma tabela ou exibição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Gets the following information: name and ID of the statistics, whether the statistics were created automatically or by the user, whether the statistics were created with the NORECOMPUTE option, and whether the statistics have a filter and, if so, what that filter is.  
    */  
    SELECT name AS statistics_name  
        ,stats_id  
        ,auto_created  
        ,user_created  
        ,no_recompute  
        ,has_filter  
        ,filter_definition  
    -- using the sys.stats catalog view  
    FROM sys.stats  
    -- for the Sales.SpecialOffer table  
    WHERE object_id = OBJECT_ID('Sales.SpecialOffer');  
    GO  
    ```  
  
 Para obter mais informações, veja [sys.stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-stats-transact-sql).  
  
  
