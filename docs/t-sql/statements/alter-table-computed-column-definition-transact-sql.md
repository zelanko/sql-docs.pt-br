---
description: ALTER TABLE computed_column_definition (Transact-SQL)
title: computed_column_definition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER TABLE statement
ms.assetid: 746eabda-3b4f-4940-b0b5-1c379f5cf7a5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 06ce56d0e4a25f4e28c1ded6c0dc246a0ee3b730
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549433"
---
# <a name="alter-table-computed_column_definition-transact-sql"></a>ALTER TABLE computed_column_definition (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Especifica as propriedades de uma coluna computada que são adicionadas a uma tabela usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
column_name AS computed_column_expression  
[ PERSISTED [ NOT NULL ] ]  
[   
    [ CONSTRAINT constraint_name ]  
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [ WITH FILLFACTOR = fillfactor ]  
        [ WITH ( <index_option> [, ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ) | filegroup   
            | "default" } ]  
    | [ FOREIGN KEY ]   
        REFERENCES ref_table [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE } ]   
        [ ON UPDATE { NO ACTION } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*column_name*  
 É o nome da coluna a ser alterada, adicionada ou removida. *column_name* pode ter de 1 a 128 caracteres. Para novas colunas, *column_name* pode ser omitido para colunas criadas com um tipo de dados **timestamp**. Se nenhum *column_name* é especificado para uma coluna do tipo de dados **timestamp**, o nome **timestamp** é usado.  
  
*computed_column_expression*  
 É uma expressão que define o valor de uma coluna computada. Uma coluna computada é uma coluna virtual que não está fisicamente armazenada na tabela, mas é computada a partir de uma expressão que usa outras colunas da mesma tabela. Uma expressão deve produzir um valor. Por exemplo, uma coluna computada pode ter a definição: cost AS price * qty. Outro exemplo com operadores de bit a bit: is_finalised como is_checked | is_approved. A expressão pode ser o nome de uma coluna não computada, constante, função, variável e qualquer combinação dessas, conectada por um ou mais operadores. A expressão não pode ser uma condição de pesquisa ou subconsulta nem incluir um tipo de dados de alias.  
  
 As colunas computadas podem ser usadas em listas de seleção, cláusulas WHERE, cláusulas ORDER BY, ou qualquer outro local no qual expressões regulares podem ser usadas, mas com as seguintes exceções:  
  
-   Uma coluna computada não pode ser usada como uma definição de restrição DEFAULT ou FOREIGN KEY ou com uma definição de restrição NOT NULL. Entretanto, se o valor da coluna computada for definido por uma expressão determinística e o tipo de dados do resultado for permitido em colunas de índice, uma coluna computada poderá ser usada como uma coluna de chave em um índice ou como parte de qualquer restrição PRIMARY KEY ou UNIQUE.  
  
     Por exemplo, se a tabela tiver colunas de inteiros a e b, a coluna computada a + b poderá ser indexada, mas a coluna computada a +DATEPART(dd, GETDATE()) não poderá ser indexada, pois o valor pode ser alterado em invocações subsequentes.  
  
-   Uma coluna computada não pode ser o destino de uma instrução INSERT ou UPDATE.  
  
    > [!NOTE]  
    >  Como cada linha de uma tabela pode ter valores diferentes para as colunas envolvidas em uma coluna computada, a coluna computada poderá não ter o mesmo resultado para cada linha.  
  
PERSISTED  
 Especifica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazenará fisicamente os valores computados na tabela e atualizará os valores quando for atualizada qualquer outra coluna da qual a coluna computada depende. Marcar uma coluna computada como PERSISTED permite que um índice seja criado em uma coluna computada que é determinística, mas não precisa. Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md). Qualquer coluna computada usada como coluna de particionamento de uma tabela particionada deve ser marcada explicitamente PERSISTED. *computed_column_expression* deve ser determinística quando PERSISTED é especificado. 

NULL | NOT NULL  
 Especifica se são permitidos valores nulos na coluna. NULL não é estritamente uma restrição, mas pode ser especificado como NOT NULL. NOT NULL poderá ser especificado para colunas computadas somente se PERSISTED também for especificado.  
  
CONSTRAINT  
 Especifica o início da definição de uma restrição PRIMARY KEY ou UNIQUE.  
  
*constraint_name*  
 É a nova restrição. Os nomes de restrição devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md), a não ser que o nome não possa começar com uma tecla jogo da velha (#). Se *constraint_name* não for fornecido, um nome gerado pelo sistema será atribuído à restrição.  
  
PRIMARY KEY  
 É uma restrição que impõe a integridade de entidade para uma coluna ou colunas especificadas usando um índice exclusivo. Somente uma restrição PRIMARY KEY pode ser criada para cada tabela.  
  
UNIQUE  
 É uma restrição que fornece a integridade de entidade para uma coluna ou colunas específicas usando um índice exclusivo.  
  
CLUSTERED | NONCLUSTERED  
 Especifica que um índice clusterizado ou não clusterizado é criado para a restrição PRIMARY KEY ou UNIQUE. As restrições PRIMARY KEY usam como padrão CLUSTERED. As restrições UNIQUE usam como padrão NONCLUSTERED.  
  
 Se uma restrição ou índice clusterizado já existir em uma tabela, CLUSTERED não poderá ser especificado. Se uma restrição ou índice clusterizado já existir em uma tabela, as restrições PRIMARY KEY usam como padrão NONCLUSTERED.  
  
WITH FILLFACTOR =*fillfactor*  
 Especifica o quanto o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] deve preencher cada página de índice usada para armazenar os dados de índice. Os valores de *fillfactor* especificados pelo usuário podem ser de 1 a 100. Se um valor não for especificado, o padrão será 0.  
  
> [!IMPORTANT]  
>  A documentação de WITH FILLFACTOR = *fillfactor* como a única opção de índice aplicável às restrições PRIMARY KEY ou UNIQUE é mantida para fins de compatibilidade com versões anteriores, mas não será documentada dessa maneira em versões futuras. Outras opções de índice podem ser especificadas na cláusula [index_option &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md) de ALTER TABLE.  
  
FOREIGN KEY REFERENCES  
 É uma restrição que fornece integridade referencial para os dados na coluna ou colunas. As restrições FOREIGN KEY requerem que cada valor na coluna exista na coluna ou colunas referenciadas correspondentes na tabela referenciada. As restrições FOREIGN KEY podem fazer referência somente a colunas que sejam restrições PRIMARY KEY ou UNIQUE na tabela ou colunas referenciadas em um UNIQUE INDEX na tabela referenciada. As chaves estrangeiras em colunas computadas também devem ser marcadas como PERSISTED.  
  
*ref_table*  
 É o nome da tabela referenciada pela restrição FOREIGN KEY.  
  
(*ref_column* )  
 É uma coluna da tabela referenciada pela restrição FOREIGN KEY.  
  
ON DELETE { **NO ACTION** | CASCADE }  
 Especifica a ação que acontece nas linhas da tabela, se essas linhas tiverem uma relação referencial e a linha referenciada for excluída da tabela pai. O padrão é NO ACTION.  
  
NO ACTION  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro e a ação de excluir na linha da tabela pai é revertida.

CASCADE  
 As linhas correspondentes serão excluídas da tabela de referência se aquela linha for excluída da tabela pai.  
  
 Por exemplo, no banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], a tabela ProductVendor tem uma relação referencial com a tabela Vendor. A chave estrangeira ProductVendor.BusinessEntityID referencia a chave primária Vendor.BusinessEntityID.  
  
 Se uma instrução DELETE for executada em uma linha da tabela Vendor e uma ação ON DELETE CASCADE for especificada para ProductVendor.BusinessEntityID, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificará se há uma ou mais linhas dependentes na tabela ProductVendor. Se existir alguma, as linhas dependentes na tabela ProductVendor serão excluídas, além da linha referenciada na tabela Vendor.  
  
 Entretanto, se NO ACTION for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerará um erro e reverterá a ação de exclusão da linha Vendor quando houver pelo menos uma linha da tabela ProductVendor que a referencie.  
  
 Não especifique CASCADE se a tabela for incluída em uma publicação de mesclagem que usa registros lógicos. Para obter mais informações sobre registros lógicos, consulte [Agrupar alterações em linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
ON UPDATE { **NO ACTION** }  
 Especifica a ação que acontece nas linhas da tabela criada, quando essas linhas têm uma relação referencial e a linha referenciada for atualizada na tabela pai. Quando NO ACTION for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerará um erro e reverterá a ação de atualização da linha Vendor se houver pelo menos uma linha da tabela ProductVendor que a referencie.  
  
NOT FOR REPLICATION  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Pode ser especificado para restrições FOREIGN KEY e instruções CHECK. Se essa cláusula for especificada para uma restrição, ela não será aplicada quando os agentes de replicação executarem operações insert, update ou delete.  
  
CHECK  
 É uma restrição que impõe a integridade de domínio limitando os possíveis valores que podem ser inseridos em uma ou mais colunas. As restrições CHECK em colunas computadas também devem ser marcadas como PERSISTED.  
  
*logical_expression*  
 É uma expressão lógica que retorna TRUE ou FALSE. A expressão não pode conter uma referência a um tipo de dados de alias.  
  
ON { *partition_scheme_name*(*partition_column_name*) | *filegroup*| "default"}  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Especifica o local de armazenamento do índice criado para a restrição. Se *partition_scheme_name* for especificado, o índice será particionado e as partições serão mapeadas para os grupos de arquivos especificados pelo *partition_scheme_name*. Se *filegroup* for especificado, o índice será criado no grupo de arquivos nomeado. Se "default" for especificado ou se ON não for especificado, o índice será criado no mesmo grupo de arquivos que a tabela. Se ON for especificado quando um índice clusterizado for adicionado a uma restrição PRIMARY KEY ou UNIQUE, a tabela inteira será movida para o grupo de arquivos especificado quando o índice clusterizado for criado.  
  
> [!NOTE]  
>  Nesse contexto, default não é uma palavra-chave. É um identificador para o grupo de arquivos padrão e deve ser delimitado, como em ON "default" ou ON [default]. Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. Essa é a configuração padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Cada restrição PRIMARY KEY e UNIQUE gera um índice. O número de restrições UNIQUE e PRIMARY KEY não pode fazer com que o número de índices na tabela exceda 999 índices não clusterizados e 1 índice clusterizado.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
