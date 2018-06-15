---
title: column_constraint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- column_constraint
- column_constraint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER TABLE statement
- constraints [SQL Server], properties
- constraints [SQL Server], definitions
- column_constraint
ms.assetid: 8119b7c7-e93b-4de5-8f71-c3b7c70b993c
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8684085fd99d2f3f9189c90577934314d55e4047
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33072773"
---
# <a name="alter-table-columnconstraint-transact-sql"></a>ALTER TABLE column_constraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica as propriedades de uma restrição PRIMARY KEY, FOREIGN KEY, UNIQUE ou CHECK que faz parte da definição de uma nova coluna adicionada a uma tabela usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [ WITH FILLFACTOR = fillfactor ]   
        [ WITH ( index_option [, ...n ] ) ]  
        [ ON { partition_scheme_name (partition_column_name)   
            | filegroup | "default" } ]   
    | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name   
            [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 CONSTRAINT  
 Especifica o início da definição para uma restrição PRIMARY KEY, UNIQUE, FOREIGN KEY ou CHECK.  
  
 *constraint_name*  
 É o nome da restrição. Os nomes de restrição devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md), a não ser que o nome não possa começar com uma tecla jogo da velha (#). Se *constraint_name* não for fornecido, um nome gerado pelo sistema será atribuído à restrição.  
  
 NULL | NOT NULL  
 Especifica se a coluna pode aceitar valores nulos. Colunas que não aceitam valores nulos podem ser adicionadas somente se tiverem um padrão especificado. Se a nova coluna permitir valores nulos e nenhum padrão for especificado, ela será NULL para cada linha da tabela. Se a nova coluna permitir valores nulos e uma definição padrão for adicionada com a nova coluna, a opção WITH VALUES poderá ser usada para armazenar o valor padrão na nova coluna para cada linha existente na tabela.  
  
 Se a nova coluna não permitir valores nulos, uma definição DEFAULT deverá ser adicionada a ela. A nova coluna é carregada automaticamente com o valor padrão nas novas colunas em cada linha existente.  
  
 Quando a adição de uma coluna requer alterações físicas às linhas de dados de uma tabela, tal como adicionar valores DEFAULT a cada linha, bloqueios são mantidos na tabela durante a execução de ALTER TABLE. Isso afeta a capacidade de alterar o conteúdo da tabela enquanto o bloqueio estiver em vigor. Entretanto, a adição de uma coluna que permite valores nulos e não especifica um valor padrão é uma operação de metadados somente e não envolve nenhum bloqueio.  
  
 Quando CREATE TABLE ou ALTER TABLE é usado, a configuração de banco de dados e de sessão influencia e, possivelmente, substitui a nulabilidade do tipo de dados que é usado em uma definição de coluna. Recomendamos que você sempre defina explicitamente colunas não computadas como NULL ou NOT NULL ou, se usar um tipo de dados definido pelo usuário, que permita que a coluna use a nulabilidade padrão do tipo de dados. Para obter mais informações, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 PRIMARY KEY  
 É uma restrição que impõe a integridade de entidade para uma coluna ou colunas especificadas usando um índice exclusivo. Somente uma restrição PRIMARY KEY pode ser criada para cada tabela.  
  
 UNIQUE  
 É uma restrição que fornece a integridade de entidade para uma coluna ou colunas especificadas usando um índice exclusivo.  
  
 CLUSTERED | NONCLUSTERED  
 Especifica que um índice clusterizado ou não clusterizado é criado para a restrição PRIMARY KEY ou UNIQUE. As restrições PRIMARY KEY usam como padrão CLUSTERED. As restrições UNIQUE usam como padrão NONCLUSTERED.  
  
 Se uma restrição ou índice clusterizado já existir em uma tabela, CLUSTERED não poderá ser especificado. Se uma restrição ou índice clusterizado já existir em uma tabela, as restrições PRIMARY KEY usam como padrão NONCLUSTERED.  
  
 Colunas que são dos tipos de dados **ntext**, **text**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **xml** ou **image** não podem ser especificadas como colunas de para índice.  
  
 WITH FILLFACTOR **=***fillfactor*  
 Especifica o quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher cada página de índice usada para armazenar os dados de índice. Os valores de fator de preenchimento especificados pelo usuário podem ser de 1 a 100. Se um valor não for especificado, o padrão será 0.  
  
> [!IMPORTANT]  
>  A documentação de WITH FILLFACTOR = *fillfactor* como a única opção de índice aplicável às restrições PRIMARY KEY ou UNIQUE é mantida para fins de compatibilidade com versões anteriores, mas não será documentada dessa maneira em versões futuras. Outras opções de índice podem ser especificadas na cláusula [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md) de ALTER TABLE.  
  
 ON { *partition_scheme_name ***(*** partition_column_name***)** | *filegroup* | **"** default **"** }  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o local de armazenamento do índice criado para a restrição. Se *partition_scheme_name* for especificado, o índice será particionado e as partições serão mapeadas para os grupos de arquivos especificados pelo *partition_scheme_name*. Se *filegroup* for especificado, o índice será criado no grupo de arquivos nomeado. Se **"** default **"** for especificado ou se ON não for especificado de modo algum, o índice será criado no mesmo grupo de arquivos que a tabela. Se ON for especificado quando um índice clusterizado for adicionado a uma restrição PRIMARY KEY ou UNIQUE, a tabela inteira será movida para o grupo de arquivos especificado quando o índice clusterizado for criado.  
  
 Nesse contexto, default não é uma palavra-chave. É um identificador do grupo de arquivos padrão e precisa ser delimitado, como em ON **"** default **"** ou ON **[** default **]**. Se **"** default **"** for especificado, a opção QUOTED_IDENTIFIER deverá ser ON para a sessão atual. Essa é a configuração padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 FOREIGN KEY REFERENCES  
 É uma restrição que fornece integridade referencial para obter dados na coluna. Restrições FOREIGN KEY requerem que cada valor na coluna exista na coluna especificada na tabela referenciada.  
  
 *schema_name*  
 É o nome do esquema ao qual pertence a tabela referenciada pela restrição FOREIGN KEY.  
  
 *referenced_table_name*  
 É a tabela referenciada pela restrição FOREIGN KEY.  
  
 *ref_column*  
 É uma coluna entre parênteses referenciada pela nova restrição FOREIGN KEY.  
  
 ON DELETE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }  
 Especifica a ação que acontece nas linhas da tabela alterada, se essas linhas tiverem uma relação referencial e a linha referenciada for excluída da tabela pai. O padrão é NO ACTION.  
  
 NO ACTION  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gera um erro e a ação de excluir na linha da tabela pai é revertida.  
  
 CASCADE  
 As linhas correspondentes serão excluídas da tabela de referência se aquela linha for excluída da tabela pai.  
  
 SET NULL  
 Todos os valores que compõem a chave estrangeira são definidos como NULL quando a linha correspondente na tabela pai é excluída. Para que essa restrição seja executada, as colunas de chave estrangeira devem ser anuláveis.  
  
 SET DEFAULT  
 Todos os valores que incluem a chave estrangeira são definidos como seus valores padrão quando a linha correspondente na tabela pai é excluída. Para que essa restrição seja executada, todas as colunas de chave estrangeira devem ter definições padrão. Se a coluna for anulável e não houver nenhum valor padrão explícito definido, NULL se tornará o valor padrão implícito para a coluna.  
  
 Não especifique CASCADE se a tabela for incluída em uma publicação de mesclagem que usa registros lógicos. Para obter mais informações sobre registros lógicos, consulte [Agrupar alterações em linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 ON DELETE CASCADE não poderá ser definido se um disparador INSTEAD OF ON DELETE  já existir na tabela que está sendo alterada.  
  
 Por exemplo, no banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], a tabela **ProductVendor** tem uma relação referencial com a tabela **Vendor**. A chave estrangeira **ProductVendor.VendorID** faz referência à chave primária **Vendor.VendorID**.  
  
 Se uma instrução DELETE for executada em uma linha da tabela **Vendor** e uma ação ON DELETE CASCADE for especificada para **ProductVendor.VendorID**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificará se há uma ou mais linhas dependentes na tabela **ProductVendor**. Se existir alguma, as linhas dependentes na tabela **ProductVendor** serão excluídas, além da linha referenciada na tabela **Vendor**.  
  
 Entretanto, se NO ACTION for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerará um erro e reverterá a ação de exclusão da linha **Vendor** quando houver pelo menos uma linha da tabela **ProductVendor** que a referencie.  
  
 ON UPDATE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }  
 Especifica a ação que ocorre nas linhas da tabela alterada, quando essas linhas têm uma relação referencial e a linha referenciada for atualizada na tabela pai. O padrão é NO ACTION.  
  
 NO ACTION  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro, e a ação de atualizar na linha da tabela pai é revertida.  
  
 CASCADE  
 As linhas correspondentes são atualizadas na tabela de referência quando aquela linha é atualizada na tabela pai.  
  
 SET NULL  
 Todos os valores que compõem a chave estrangeira são definidos como NULL quando a linha correspondente na tabela pai é atualizada. Para que essa restrição seja executada, as colunas de chave estrangeira devem ser anuláveis.  
  
 SET DEFAULT  
 Todos os valores que compõem a chave estrangeira são definidos como seus valores padrão quando a linha correspondente na tabela pai é atualizada. Para que essa restrição seja executada, todas as colunas de chave estrangeira devem ter definições padrão. Se a coluna for anulável e não houver nenhum valor padrão explícito definido, NULL se tornará o valor padrão implícito para a coluna.  
  
 Não especifique CASCADE se a tabela for incluída em uma publicação de mesclagem que usa registros lógicos. Para obter mais informações sobre registros lógicos, consulte [Agrupar alterações em linhas relacionadas com registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 ON UPDATE CASCADE, SET NULL ou SET DEFAULT não poderá ser definido se um gatilho INSTEAD OF de ON UPDATE já existir na tabela que está sendo alterada.  
  
 Por exemplo, no banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], a tabela **ProductVendor** tem uma relação referencial com a tabela **Vendor**. A chave estrangeira **ProductVendor.VendorID** faz referência à chave primária **Vendor.VendorID**.  
  
 Se uma instrução UPDATE for executada em uma linha da tabela **Vendor** e uma ação ON UPDATE CASCADE for especificada para **ProductVendor.VendorID**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificará se há uma ou mais linhas dependentes na tabela **ProductVendor**. Se existir alguma, a linha dependente na tabela **ProductVendor** será atualizada, além da linha referenciada na tabela **Vendor**.  
  
 Entretanto, se NO ACTION for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerará um erro e reverterá a ação de atualização da linha **Vendor** quando houver pelo menos uma linha da tabela **ProductVendor** que a referencie.  
  
 NOT FOR REPLICATION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Pode ser especificado para restrições FOREIGN KEY e instruções CHECK. Se essa cláusula for especificada para uma restrição, ela não será aplicada quando os agentes de replicação executarem operações insert, update ou delete.  
  
 CHECK  
 É uma restrição que impõe a integridade de domínio limitando os possíveis valores que podem ser inseridos em uma ou mais colunas.  
  
 *logical_expression*  
 É uma expressão lógica usada em uma restrição CHECK e retorna TRUE ou FALSE. *logical_expression* usada com restrições CHECK não pode fazer referência a outra tabela, mas pode fazer referência a outras colunas na mesma tabela para a mesma linha. A expressão não pode referenciar um tipo de dados de alias.  
  
## <a name="remarks"></a>Remarks  
 Quando restrições FOREIGN KEY ou CHECK são adicionadas, todos os dados existentes são verificados quanto a violações de restrição, a menos que a opção WITH NOCHECK seja especificada. Se qualquer violação ocorrer, ALTER TABLE falhará e um erro será retornado. Quando uma nova restrição PRIMARY KEY ou UNIQUE for adicionada a uma coluna existente, os dados na coluna ou colunas deverão ser exclusivos. Se forem encontrados valores duplicados, ALTER TABLE falhará. A opção WITH NOCHECK não tem nenhum efeito quando as restrições PRIMARY KEY ou UNIQUE são adicionadas.  
  
 Cada restrição PRIMARY KEY e UNIQUE gera um índice. O número de restrições UNIQUE e PRIMARY KEY não pode fazer com que o número de índices na tabela exceda 999 índices não clusterizados e 1 índice clusterizado. Restrições de chave estrangeira não geram automaticamente um índice. Entretanto, as colunas de chave estrangeira são frequentemente usadas em critérios de junção de consultas, correspondendo as colunas na restrição de chave estrangeira de uma tabela com as colunas de chave exclusiva ou primária em outra tabela. Um índice nas colunas de chave estrangeira habilita o [!INCLUDE[ssDE](../../includes/ssde-md.md)] a localizar rapidamente dados relacionados na tabela de chave estrangeira.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos, consulte [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-definition-transact-sql.md)  
  
  
