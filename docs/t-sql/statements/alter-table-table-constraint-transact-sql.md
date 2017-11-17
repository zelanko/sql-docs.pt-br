---
title: table_constraint (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table_constraint
ms.assetid: ac2a11e0-cc77-4e27-b107-4fe5bc6f5195
caps.latest.revision: 59
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f5265366f28f302e69a178f45baa4464efa1bfd
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-tableconstraint-transact-sql"></a>ALTER TABLE table_constraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica as propriedades de uma chave primária, UNIQUE, FOREIGN KEY, uma restrição de verificação ou uma definição DEFAULT adicionada a uma tabela usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        [ WITH ( <index_option>[ , ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ... )  
          | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )  
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | DEFAULT constant_expression FOR column [ WITH VALUES ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 CONSTRAINT  
 Especifica o início de uma definição para uma restrição PRIMARY KEY, UNIQUE, FOREIGN KEY ou CHECK, ou um DEFAULT.  
  
 *constraint_name*  
 É o nome da restrição. Nomes de restrição devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md), exceto que o nome não pode começar com um sinal numérico (#). Se constraint_name não for fornecido, um nome gerado pelo sistema será atribuído à restrição.  
  
 PRIMARY KEY  
 É uma restrição que impõe a integridade de entidade para uma coluna ou colunas especificadas usando um índice exclusivo. Somente uma restrição PRIMARY KEY pode ser criada para cada tabela.  
  
 UNIQUE  
 É uma restrição que fornece a integridade de entidade para uma coluna ou colunas especificadas usando um índice exclusivo.  
  
 CLUSTERED | NONCLUSTERED  
 Especifica que um índice clusterizado ou não clusterizado é criado para a restrição PRIMARY KEY ou UNIQUE. As restrições PRIMARY KEY usam como padrão CLUSTERED. As restrições UNIQUE usam como padrão NONCLUSTERED.  
  
 Se uma restrição ou índice clusterizado já existir em uma tabela, CLUSTERED não poderá ser especificado. Se uma restrição ou índice clusterizado já existir em uma tabela, as restrições PRIMARY KEY usam como padrão NONCLUSTERED.  
  
 Colunas de **ntext**, **texto**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, ou **imagem** tipos de dados não podem ser especificados como colunas de um índice.  
  
 *coluna*  
 É uma coluna ou lista de colunas especificadas entre parênteses que são usadas em uma nova restrição.  
  
 [ **ASC** | DESC]  
 Especifica a ordem na qual a coluna ou colunas que participam de restrições de tabela são classificadas. O padrão é ASC.  
  
 COM o fator de preenchimento  **=**  *fator de preenchimento*  
 Especifica o quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher cada página de índice usada para armazenar os dados de índice. Especificado pelo usuário *fillfactor* valores podem ser de 1 a 100. Se um valor não for especificado, o padrão será 0.  
  
> [!IMPORTANT]  
>  Documentação de WITH FILLFACTOR = *fillfactor* como a única opção de índice que se aplica a restrições PRIMARY KEY ou UNIQUE é mantida para compatibilidade com versões anteriores, mas não será documentada dessa maneira em futuras versões. Outras opções de índice podem ser especificadas no [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md) cláusula de ALTER TABLE.  
  
 ON { *partition_scheme_name***(***partition_column_name***)** | *arquivos* |  **"**padrão**"** }  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o local de armazenamento do índice criado para a restrição. Se *partition_scheme_name* for especificado, o índice é particionado e as partições são mapeadas para os grupos de arquivos que são especificados pelo *partition_scheme_name*. Se *arquivos* for especificado, o índice é criado no grupo de arquivos nomeado. Se **"**padrão**"** for especificado ou se ON não for especificado, o índice é criado no mesmo grupo de arquivos da tabela. Se ON for especificado quando um índice clusterizado for adicionado a uma restrição PRIMARY KEY ou UNIQUE, a tabela inteira será movida para o grupo de arquivos especificado quando o índice clusterizado for criado.  
  
 Nesse contexto, o padrão não é uma palavra-chave; ele é um identificador para o grupo de arquivos padrão e deve ser delimitado, como em ON **"**padrão**"** ou ON **[**padrão**]**. Se **"**padrão**"** for especificado, a opção QUOTED_IDENTIFIER deve estar ON para a sessão atual. Essa é a configuração padrão.  
  
 FOREIGN KEY REFERENCES  
 É uma restrição que fornece integridade referencial para obter dados na coluna. Restrições FOREIGN KEY requerem que cada valor na coluna exista na coluna especificada na tabela referenciada.  
  
 *referenced_table_name*  
 É a tabela referenciada pela restrição FOREIGN KEY.  
  
 *ref_column*  
 É uma coluna ou lista de colunas entre parênteses referenciadas pela nova restrição FOREIGN KEY.  
  
 ON DELETE { **NENHUMA AÇÃO** | CASCADE | SET NULL | SET DEFAULT}  
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
  
 ON DELETE CASCADE não poderá ser definido se um disparador INSTEAD OF ON DELETE já existir na tabela que está sendo alterada.  
  
 Por exemplo, no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados, o **ProductVendor** tabela tem uma relação referencial com a **fornecedor** tabela. O **productvendor. VendorID** referências de chave estrangeira a **VendorID** chave primária.  
  
 Se uma instrução DELETE é executada em uma linha de **fornecedor** tabela e uma ação ON DELETE CASCADE for especificada para **productvendor. VendorID**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se há uma ou mais linhas dependentes no **ProductVendor** tabela. Se existir alguma, as linhas dependentes no **ProductVendor** tabela será excluída, além da linha referenciada no **fornecedor** tabela.  
  
 Por outro lado, se NO ACTION for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro e reverterá a ação de exclusão de **fornecedor** linha quando há pelo menos uma linha no **ProductVendor** tabela que faz referência a ele.  
  
 AO ATUALIZAR { **NENHUMA AÇÃO** | CASCADE | SET NULL | SET DEFAULT}  
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
  
 Por exemplo, no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados, o **ProductVendor** tabela tem uma relação referencial com a **fornecedor** tabela. O **productvendor. VendorID** referências de chave estrangeira a **VendorID** chave primária.  
  
 Se uma instrução UPDATE é executada em uma linha de **fornecedor** tabela e uma ação ON UPDATE CASCADE for especificada para **productvendor. VendorID**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se há uma ou mais linhas dependentes no **ProductVendor** tabela. Se existir alguma, a linha dependente no **ProductVendor** tabela será atualizada, bem como a linha referenciada no **fornecedor** tabela.  
  
 Por outro lado, se NO ACTION for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro e reverterá a ação de atualização a **fornecedor** linha quando houver pelo menos uma linha a **ProductVendor** tabela que faz referência a ele.  
  
 NOT FOR REPLICATION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Pode ser especificado para restrições FOREIGN KEY e instruções CHECK. Se essa cláusula for especificada para uma restrição, ela não será aplicada quando os agentes de replicação executarem operações insert, update ou delete.  
  
 DEFAULT  
 Especifica o valor padrão para a coluna. Podem ser usadas definições DEFAULT para fornecer valores para uma coluna nova nas linhas existentes de dados. Definições DEFAULT não podem ser adicionadas a colunas que têm um **timestamp** tipo de dados, uma propriedade IDENTITY, uma definição DEFAULT existente ou um padrão associado. Se a coluna tiver um padrão existente, o padrão deve ser descartado antes de o novo padrão ser adicionado. Se um valor padrão é especificado para uma coluna de tipo definido pelo usuário, o tipo deverá oferecer suporte a uma conversão implícita de *constant_expression* para o tipo definido pelo usuário. Para manter a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um nome de restrição pode ser atribuído a um DEFAULT.  
  
 *constant_expression*  
 É um valor literal, um NULL ou uma função de sistema usados como valor de coluna padrão. Se *constant_expression* é usada em conjunto com uma coluna definida como um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipo definido pelo usuário, a implementação do tipo deve dar suporte a uma conversão implícita da *constant_ expressão* para o tipo definido pelo usuário.  
  
 PARA *coluna*  
 Especifica a coluna associada a uma definição de DEFAULT em nível de tabela.  
  
 WITH VALUES  
 Especifica que o valor padrão fornecido *constant_expression* é armazenado em uma nova coluna é adicionada a linhas existentes. WITH VALUES pode ser especificado somente quando DEFAULT é especificado em uma cláusula de coluna ADD. Se a coluna adicionada permitir valores nulos e WITH VALUES for especificado, o valor padrão será armazenado na nova coluna adicionada a linhas existentes. Se WITH VALUES não for especificado para colunas que permitem nulos, o valor NULL será armazenado na nova coluna em linhas existentes. Se a nova coluna não permitir nulos, o valor padrão será armazenado em linhas novas, independentemente de WITH VALUES ser especificado.  
  
 CHECK  
 É uma restrição que impõe a integridade de domínio limitando os possíveis valores que podem ser inseridos em uma ou mais colunas.  
  
 *Logical_Expression*  
 É uma expressão lógica usada em uma restrição CHECK e retorna TRUE ou FALSE. *Logical_Expression* usado com a verificação de restrições não podem fazer referência a outra tabela mas pode fazer referência a outras colunas na mesma tabela para a mesma linha. A expressão não pode referenciar um tipo de dados de alias.  
  
## <a name="remarks"></a>Comentários  
 Quando restrições FOREIGN KEY ou CHECK são adicionadas, todos os dados existentes são verificados quanto a violações de restrição, a menos que a opção WITH NOCHECK seja especificada. Se qualquer violação ocorrer, ALTER TABLE falhará e um erro será retornado. Quando uma nova restrição PRIMARY KEY ou UNIQUE for adicionada a uma coluna existente, os dados na coluna ou colunas deverão ser exclusivos. Se forem encontrados valores duplicados, ALTER TABLE falhará. A opção WITH NOCHECK não tem nenhum efeito quando as restrições PRIMARY KEY ou UNIQUE são adicionadas.  
  
 Cada restrição PRIMARY KEY e UNIQUE gera um índice. O número de restrições UNIQUE e PRIMARY KEY não pode fazer com que o número de índices na tabela exceda 999 índices não clusterizados e 1 índice clusterizado. Restrições de chave estrangeira não geram automaticamente um índice. Entretanto, as colunas de chave estrangeira são frequentemente usadas em critérios de junção de consultas, correspondendo as colunas na restrição de chave estrangeira de uma tabela com as colunas de chave exclusiva ou primária em outra tabela. Um índice nas colunas de chave estrangeira habilita o [!INCLUDE[ssDE](../../includes/ssde-md.md)] a localizar rapidamente dados relacionados na tabela de chave estrangeira.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos, consulte [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

