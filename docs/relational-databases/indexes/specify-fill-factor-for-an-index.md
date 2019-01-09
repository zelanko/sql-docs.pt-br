---
title: Especificar o fator de preenchimento para um índice | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- fill factor [SQL Server]
- page splits [SQL Server]
ms.assetid: 237a577e-b42b-4adb-90cf-aa7fb174f3ab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ba81029a195bcee0e747bfe517fa5d6b27e4ead1
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588370"
---
# <a name="specify-fill-factor-for-an-index"></a>Especificar fator de preenchimento para um índice
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este tópico descreve o que é fator de preenchimento e como especificar um valor de fator de preenchimento em um índice no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 A opção fator de preenchimento é fornecida para ajustar o armazenamento e o desempenho de dados de índice. Quando um índice é criado ou recriado, o valor de fator de preenchimento determina a porcentagem de espaço em cada página de nível folha a ser preenchida com dados, reservando o restante em cada página como espaço livre para futuro crescimento. Por exemplo, a especificação de um valor de fator de preenchimento de 80 significa que 20 por cento de cada página de nível folha ficará vazio, fornecendo espaço para a expansão do índice à medida que dados forem adicionados à tabela subjacente. O espaço vazio é reservado entre as linhas do índice e não no final do índice.  
  
 O valor de fator de preenchimento é uma porcentagem de 1 a 100 e o padrão para todo o servidor é 0, o que significa que as páginas de nível folha estão totalmente preenchidas.  
  
> [!NOTE]  
>  Os valores de fator de preenchimento 0 e 100 são iguais em todos os aspectos.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Considerações sobre desempenho](#Performance)  
  
     [Segurança](#Security)  
  
-   **Para especificar um fator de preenchimento em um índice usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Performance"></a> Considerações sobre desempenho  
  
#### <a name="page-splits"></a>Divisões de página  
 Um valor de fator de preenchimento corretamente escolhido pode reduzir divisões potenciais de páginas fornecendo espaço suficiente para expansão do índice à medida que são adicionados dados à tabela subjacente. Quando uma nova linha é adicionada a uma página de índice cheia, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] move aproximadamente metade das linhas para uma nova página para fornecer espaço para a nova linha. Essa reorganização é conhecida como divisão de página. Uma divisão de página abre espaço para novos registros, mas pode demorar a ser executada e é uma operação que consome muitos recursos. Além disso, também pode causar fragmentação, o que gera um aumento das operações de E/S. Quando ocorrem divisões de página frequentemente, o índice pode ser recriado usando um valor de fator de preenchimento novo ou existente para redistribuir os dados. Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Embora um valor de fator de preenchimento baixo, diferente de 0, possa reduzir a necessidade de dividir páginas à medida que o índice cresce, o índice precisará de mais espaço de armazenamento e poderá reduzir o desempenho de leitura. Mesmo para um aplicativo orientado para muitas operações de inserção e atualização, o número de leituras de banco de dados normalmente ultrapassa o número de gravações de banco de dados por um fator de 5 a 10. Portanto, especificar um fator de preenchimento diferente do padrão pode reduzir o desempenho de leitura de banco de dados em um valor inversamente proporcional à configuração do fator de preenchimento. Por exemplo, um valor de fator de preenchimento de 50 pode fazer com que o desempenho de leitura do banco de dados seja reduzido em duas vezes. O desempenho de leitura é reduzido porque o índice contém mais páginas, portanto, aumenta as operações de E/S no disco necessárias para recuperar os dados.  
  
#### <a name="adding-data-to-the-end-of-the-table"></a>Adicionando dados ao final da tabela  
 Um fator de preenchimento diferente de zero ou 100 poderá ser bom para o desempenho se os novos dados forem distribuídos uniformemente ao longo da tabela. No entanto, se todos os dados forem adicionados ao final da tabela, o espaço vazio nas páginas do índice não será preenchido. Por exemplo, se a coluna de chave de índice for uma coluna IDENTITY, a chave de novas linhas estará sempre aumentando e as linhas do índice serão adicionadas logicamente no final do índice. Se as linhas existentes serão atualizadas com dados que aumentam o tamanho das linhas, use um fator de preenchimento menor que 100. Os bytes adicionais em cada página ajudarão minimizar divisões de página provocadas pelo comprimento adicional nas linhas.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-specify-a-fill-factor-by-using-table-designer"></a>Para especificar um fator de preenchimento usando o Designer de Tabela  
  
1.  No Pesquisador de Objetos, clique no sinal de adição ao lado do banco de dados que contém a tabela na qual você deseja especificar um fator de preenchimento de índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique com o botão direito do mouse na tabela para a qual você deseja especificar um fator de preenchimento e selecione **Design**.  
  
4.  No menu **Designer de Tabela** , clique em **Índices/Chaves**.  
  
5.  Selecione o índice com o fator de preenchimento que você deseja especificar.  
  
6.  Expanda **Especificação de Preenchimento**, selecione a linha **Fator de Preenchimento** e digite o fator de preenchimento que você deseja na linha.  
  
7.  Clique em **Fechar**.  
  
8.  No menu **Arquivo** , selecione **Salvar**_table_name_.  
  
#### <a name="to-specify-a-fill-factor-in-an-index-by-using-object-explorer"></a>Para especificar um fator de preenchimento em um índice usando o Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, clique no sinal de adição ao lado do banco de dados que contém a tabela na qual você deseja especificar um fator de preenchimento de índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja especificar um fator de preenchimento de índice.  
  
4.  Clique no sinal de adição para expandir a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no fator de preenchimento a ser especificado e selecione **Propriedades**.  
  
6.  Em **Selecione uma página**, selecione **Opções**.  
  
7.  Na linha **Fator de Preenchimento** , digite o fator de preenchimento desejado.  
  
8.  Clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-specify-a-fill-factor-in-an-existing-index"></a>Para especificar um fator de preenchimento em um índice existente  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo recria um índice existente e aplica o fator de preenchimento especificado durante a operação de reconstrução.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Rebuilds the IX_Employee_OrganizationLevel_OrganizationNode index   
    -- with a fill factor of 80 on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD WITH (FILLFACTOR = 80);   
    GO  
    ```  
  
#### <a name="another-way-to-specify-a-fill-factor-in-an-index"></a>Outra maneira de especificar um fator de preenchimento em um índice  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    /* Drops and re-creates the IX_Employee_OrganizationLevel_OrganizationNode index on the HumanResources.Employee table with a fill factor of 80.  
    */  
  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)   
    WITH (DROP_EXISTING = ON, FILLFACTOR = 80);   
    GO  
    ```  
  
 Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
  
