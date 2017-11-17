---
title: column_definition (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- column_definition
- column_definition_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column_definition
- ALTER TABLE statement
- column properties [SQL Server]
- column definitions [SQL Server]
ms.assetid: a1742649-ca29-4d9b-9975-661cdbf18f78
caps.latest.revision: 78
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c63dcea3473198ded46ebf84053fa9d8b36330f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-columndefinition-transact-sql"></a>ALTER TABLE column_definition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica as propriedades de uma coluna que são adicionadas a uma tabela usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
column_name <data_type>  
[ FILESTREAM ]  
[ COLLATE collation_name ]   
[ NULL | NOT NULL ]  
[   
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression [ WITH VALUES ]   
    | IDENTITY [ ( seed , increment ) ] [ NOT FOR REPLICATION ]   
]  
[ ROWGUIDCOL ]   
[ SPARSE ]   
[ ENCRYPTED WITH  
  ( COLUMN_ENCRYPTION_KEY = key_name ,  
      ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,   
      ALGORITHM =  'AEAD_AES_256_CBC_HMAC_SHA_256'   
  ) ]  
[ MASKED WITH ( FUNCTION = ' mask_function ') ]  
[ <column_constraint> [ ...n ] ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
[ CONSTRAINT constraint_name ]   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH FILLFACTOR = fillfactor    
          | WITH ( < index_option > [ , ...n ] )   
        ]   
        [ ON { partition_scheme_name ( partition_column_name )   
            | filegroup | "default" } ]  
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome da coluna*  
 É o nome da coluna a ser alterada, adicionada ou removida. *nome da coluna* pode consistir de 1 a 128 caracteres. Para novas colunas, criadas com um tipo de dados timestamp *column_name* pode ser omitido. Se nenhum *column_name* é especificado para um **timestamp** coluna de tipo de dados, o nome **timestamp** é usado.  
  
 [ *type_schema_name***.** ] *type_name*  
 É o tipo de dados para a coluna adicionada e o esquema ao qual ela pertence.  
  
 *type_name* pode ser:  
  
-   Um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados do sistema.  
  
-   Um tipo de dados do alias com base em um tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os tipos de dados de alias precisam ser criados usando CREATE TYPE antes que eles possam ser usados em uma definição de tabela.  
  
-   Um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipo definido pelo usuário e o esquema ao qual ele pertence. Um tipo definido pelo usuário [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] precisa ser criado usando CREATE TYPE antes que ele possa ser usado em uma definição de tabela.  
  
 Se *type_schema_name* não for especificado, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] referências *type_name* na seguinte ordem:  
  
-   O tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O esquema padrão do usuário atual no banco de dados atual.  
  
-   O esquema **dbo** no banco de dados atual.  
  
*precisão*  
 É a precisão do tipo de dados especificado. Para obter mais informações sobre valores de precisão válidos, consulte [precisão, escala e comprimento &#40; Transact-SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
*scale*  
 É a escala do tipo de dados especificado. Para obter mais informações sobre valores de escala válidos, consulte [precisão, escala e comprimento &#40; Transact-SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
**Max**  
 Só é aplicável a **varchar**, **nvarchar**, e **varbinary** tipos de dados. São usados para armazenar 2^31 bytes de caractere e dados binários e 2^30 bytes de dados Unicode.  
  
**CONTEÚDO**  
 Especifica que cada instância do **xml** tipo de dados na *column_name* pode incluir vários elementos de nível superior. CONTEÚDO só é aplicável a **xml** dados tipo e pode ser especificado somente se *xml_schema_collection* também for especificado. Caso não seja especificado, CONTENT será o comportamento padrão.  
  
DOCUMENT  
 Especifica que cada instância do **xml** tipo de dados na *column_name* pode incluir apenas um elemento de nível superior. DOCUMENTO aplica-se somente ao **xml** dados de tipo e pode ser especificado somente se *xml_schema_collection* também for especificado.  
  
 *xml_schema_collection*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Só é aplicável a **xml** tipo de dados para associar uma coleção de esquemas XML com o tipo. Antes de digitar um **xml** coluna a um esquema, o esquema deve primeiro ser criado no banco de dados usando [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
FILESTREAM  
 Opcionalmente, especifica o atributo de armazenamento FILESTREAM para a coluna que tem um *type_name* de **varbinary (max)**.  
  
 Quando FILESTREAM é especificado para uma coluna, a tabela também deve ter uma coluna do **uniqueidentifier** tipo de dados que tem o atributo ROWGUIDCOL. Essa coluna não deve permitir valores nulos e deve ter uma restrição de coluna única UNIQUE ou PRIMARY KEY. O valor GUID da coluna deve ser fornecido por um aplicativo durante a inserção de dados, ou por uma restrição DEFAULT que utilize a função NEWID ().  
  
 A coluna ROWGUIDCOL não pode ser descartada e as restrições relacionadas não podem ser alteradas enquanto houver uma coluna FILESTREAM definida para a tabela. A coluna ROWGUIDCOL poderá ser descartada somente depois que a última coluna FILESTREAM for descartada.  
  
 Quando o atributo de armazenamento FILESTREAM é especificado para uma coluna, todos os valores da coluna são armazenados em um contêiner de dados FILESTREAM no sistema de arquivos.  
  
 Para obter um exemplo que mostra como usar a definição de coluna, consulte [FILESTREAM &#40; SQL Server &#41; ](../../relational-databases/blob/filestream-sql-server.md).  
  
COLLATE *collation_name*  
 Especifica o agrupamento da coluna. Se não for especificado, a coluna será atribuída ao agrupamento padrão do banco de dados. O nome do agrupamento tanto pode ser um nome de agrupamento do Windows como um nome de agrupamento SQL. Para obter uma lista e mais informações, consulte [nome de agrupamento do Windows &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) e [SQL nome de agrupamento do servidor &#40; Transact-SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 A cláusula COLLATE pode ser usada para especificar os agrupamentos somente de colunas do **char**, **varchar**, **nchar**, e **nvarchar** tipos de dados .  
  
 Para obter mais informações sobre a cláusula COLLATE, consulte [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
 NULL | NOT NULL  
 Determina se são permitidos valores nulos na coluna. NULL não é estritamente uma restrição, mas pode ser especificado simplesmente como NOT NULL.  
  
[Restrição *constraint_name* ]  
 Especifica o início de uma definição de valor DEFAULT. Para manter a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um nome de restrição pode ser atribuído a um DEFAULT. *constraint_name* devem seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md), exceto que o nome não pode começar com um sinal numérico (#). Se *constraint_name* não for especificado, um nome gerado pelo sistema será atribuído à definição padrão.  
  
DEFAULT  
 É uma palavra-chave que especifica o valor padrão para a coluna. Podem ser usadas definições DEFAULT para fornecer valores para uma coluna nova nas linhas existentes de dados. Definições DEFAULT não podem ser aplicadas a **timestamp** colunas ou colunas com uma propriedade de identidade. Se um valor padrão é especificado para uma coluna de tipo definido pelo usuário, o tipo deve oferecer suporte a uma conversão implícita de *constant_expression* para o tipo definido pelo usuário.  
  
*constant_expression*  
 É um valor literal, um NULL ou uma função de sistema usado como valor de coluna padrão. Se usado em conjunto com uma coluna definida como um [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipo definido pelo usuário, a implementação do tipo deve dar suporte a uma conversão implícita do *constant_expression* para o tipo definido pelo usuário.  
  
WITH VALUES  
 Especifica que o valor padrão fornecido *constant_expression* é armazenado em uma nova coluna adicionada a linhas existentes. Se a coluna adicionada permitir valores nulos e WITH VALUES estiver especificado, o valor padrão será armazenado na coluna nova adicionada a linhas existentes. Se WITH VALUES não estiver especificado para colunas que permitem nulos, o valor NULL será armazenado na nova coluna nas linhas existentes. Se a nova coluna não permitir nulos, o valor padrão será armazenado em linhas novas, independentemente de WITH VALUES ser especificado.  
  
IDENTITY  
 Especifica que a coluna nova é uma coluna de identidade. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] fornece um valor exclusivo e de incremento para a coluna. Quando você adiciona colunas de identificador a tabelas existentes, os números de identidade são adicionados às linhas existentes da tabela, com os valores de semente e de incremento. A ordem em que as linhas são atualizadas não é garantida. Os números de identidade também são gerados para todas as linhas adicionadas.  
  
 As colunas de identidade, em geral, são usadas juntamente com restrições PRIMARY KEY para servir de identificador exclusivo de linha para a tabela. A propriedade de identidade pode ser atribuída a um **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)**, ou **numeric(p,0)** coluna. Apenas uma coluna de identidade pode ser criada por tabela. A palavra-chave DEFAULT e os padrões associados não podem ser usados com uma coluna de identidade. Ambos os valores de semente e de incremento devem ser identificados, ou nenhum dos dois. Se nenhum dos dois for especificado, o padrão será (1,1).  
  
> [!NOTE]  
>  Você não pode modificar uma coluna de tabela existente para adicionar a propriedade IDENTITY.  
  
 Não há suporte para a adição de uma coluna de identidade a uma tabela publicada porque pode resultar em não convergência quando a coluna for replicada ao Assinante. Os valores na coluna de identidade no Publicador dependerão da ordem em que as linhas para a tabela afetada forem armazenadas fisicamente. As linhas poderiam ser armazenadas diferentemente no Assinante; por isso, o valor para a coluna de identidade pode ser diferente para as mesmas linhas.  
  
 Para desabilitar a propriedade de identidade de uma coluna, permitindo que os valores a serem inseridos explicitamente, use [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md).  
  
*semente*  
 O valor usado para a primeira linha é carregado na tabela.  
  
*incremento*  
 É o valor de incremento adicionado ao valor de identidade da linha anterior que é carregada.  
  
NOT FOR REPLICATION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Pode ser especificado para a propriedade IDENTITY. Se essa cláusula for especificada para a propriedade IDENTITY, os valores não serão incrementados em colunas de identidade quando os agentes de replicação executarem operações insert.  
  
ROWGUIDCOL  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica se a coluna é uma linha de coluna de identificador global exclusivo. ROWGUIDCOL só pode ser atribuída a um **uniqueidentifier** coluna e apenas um **uniqueidentifier** coluna por tabela pode ser designada como a coluna ROWGUIDCOL. ROWGUIDCOL não pode ser atribuído a colunas de tipos de dados definidos pelo usuário.  
  
 ROWGUIDCOL não obriga exclusividade dos valores armazenados na coluna. Da mesma forma, ROWGUIDCOL não gera automaticamente valores para as novas linhas inseridas na tabela. Para gerar valores exclusivos para cada coluna, use a função NEWID em instruções INSERT ou especifique a função NEWID como o padrão para a coluna. Para obter mais informações, consulte [NEWID &#40; Transact-SQL &#41; ](../../t-sql/functions/newid-transact-sql.md)e [INSERT &#40; Transact-SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
SPARSE  
 Indica que a coluna é uma coluna esparsa. O armazenamento de colunas esparsas é otimizado para obter valores nulos. Colunas esparsas não podem ser designadas como NOT NULL. Para restrições adicionais e obter mais informações sobre colunas esparsas, consulte [usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).  
  
\<column_constraint >  
 As definições dos argumentos de restrição de coluna, consulte [column_constraint &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-column-constraint-transact-sql.md).  
  
 CRIPTOGRAFADO COM  
 Especifica as colunas de criptografia usando o [sempre criptografado](../../relational-databases/security/encryption/always-encrypted-database-engine.md) recurso.  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 Especifica a chave de criptografia de coluna. Para obter mais informações, consulte [CREATE COLUMN ENCRYPTION KEY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
ENCRYPTION_TYPE = {DETERMINÍSTICA | ALEATÓRIA}  
 **Criptografia determinística** usa um método que sempre gera o mesmo valor criptografado para qualquer valor de texto não criptografado. Usando a criptografia determinística permite pesquisar usando uma comparação de igualdade, agrupamento e junção de tabelas usando junções de igualdade com base em valores criptografados, mas também pode permitir que usuários não autorizados estimar informações sobre valores criptografados examinando padrões na a coluna criptografada. Associação de duas tabelas em colunas criptografadas de forma determinista só é possível se ambas as colunas são criptografadas usando a mesma chave de criptografia de coluna. A criptografia determinística deve usar um agrupamento de colunas com uma ordem de classificação binary2 para as colunas de caracteres.  
  
 **Criptografia aleatória** usa um método que criptografa os dados de uma maneira menos previsível. A criptografia aleatória é mais segura, mas impede pesquisas de igualdade, agrupamento e junção em colunas criptografadas. Colunas usando criptografia aleatória não podem ser indexadas.  
  
 Use a criptografia determinística para colunas que serão parâmetros de pesquisa ou parâmetros de agrupamento, por exemplo um número de identificação do governo. Use a criptografia aleatória, para dados como um número de cartão de crédito, que não é agrupado com outros registros ou usado para unir tabelas e que não é pesquisado porque você usar outras colunas (como um número de transações) para localizar a linha que contém o criptografado colunas de interesse.  
  
 Colunas devem ser de um tipo de dados qualificado.  
  
ALGORITMO  
**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
Deve ser **'AEAD_AES_256_CBC_HMAC_SHA_256'**.  
  
 Para mais informações, inclusive restrições de recursos, consulte [sempre criptografado &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
   
Adicionar MASCARADOS com (função = ' *mask_function* ')  
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica uma máscara de dados dinâmicos. *mask_function* é o nome da função de mascaramento com os parâmetros apropriados. As funções a seguir estão disponíveis:  
  
-   Default()  
  
-   email()  
  
-   Partial()  
  
-   Random()  
  
 Para parâmetros de função, consulte [mascaramento de dados dinâmicos](../../relational-databases/security/dynamic-data-masking.md).  
  
## <a name="remarks"></a>Comentários  
 Se uma coluna é adicionada a ter um **uniqueidentifier** tipo de dados, ela pode ser definida com um padrão que usa a função NEWID () para fornecer os valores de identificador exclusivo na nova coluna para cada linha existente na tabela.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não impõe uma ordem para especificar DEFAULT, IDENTITY, ROWGUIDCOL nem restrições de coluna em uma definição de coluna.  
  
 A instrução ALTER TABLE falhará se a adição da coluna fizer com que o tamanho da linha de dados exceda 8060 bytes.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos, consulte [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  

