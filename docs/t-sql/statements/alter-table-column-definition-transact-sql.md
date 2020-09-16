---
description: ALTER TABLE column_definition (Transact-SQL)
title: column_definition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 28472efd6747239910630388133bdfe3ca95a6a0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547778"
---
# <a name="alter-table-column_definition-transact-sql"></a>ALTER TABLE column_definition (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Especifica as propriedades de uma coluna adicionadas a uma tabela com [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
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
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *column_name*  
 É o nome da coluna a ser alterada, adicionada ou removida. *column_name* pode consistir em 1 a 128 caracteres. Para novas colunas, criadas com um tipo de dados timestamp, *column_name* pode ser omitido. Se nenhum *column_name* é especificado para uma coluna do tipo de dados **timestamp**, o nome **timestamp** é usado.  
  
 [ _type_schema_name_ **.** ] *type_name*  
 É o tipo de dados para a coluna adicionada e o esquema ao qual ela pertence.  
  
 *type_name* pode ser:  
  
-   Um tipo de dados do sistema do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Um tipo de dados do alias com base em um tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os tipos de dados de alias precisam ser criados usando CREATE TYPE antes que eles possam ser usados em uma definição de tabela.  
  
-   Um tipo definido pelo usuário [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e o esquema ao qual ele pertence. Um tipo definido pelo usuário [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] precisa ser criado usando CREATE TYPE antes que ele possa ser usado em uma definição de tabela.  
  
 Se *type_schema_name* não for especificado, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] referenciará *type_name* na seguinte ordem:  
  
-   O tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O esquema padrão do usuário atual no banco de dados atual.  
  
-   O esquema **dbo** no banco de dados atual.  
  
*precisão*  
 É a precisão do tipo de dados especificado. Para obter mais informações sobre valores de precisão válidos, veja [Precisão, escala e tamanho &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
*scale*  
 É a escala do tipo de dados especificado. Para obter mais informações sobre valores de escala válidos, veja [Precisão, escala e tamanho &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
**max**  
 Aplica-se apenas aos tipos de dados **varchar**, **nvarchar** e **varbinary**. São usados para armazenar 2^31 bytes de caractere e dados binários e 2^30 bytes de dados Unicode.  
  
**CONTENT**  
 Especifica que cada instância do tipo de dados **xml** em *column_name* pode abranger vários elementos de nível superior. CONTENT aplica-se apenas a tipo de dados **xml** e poderá ser especificado somente se *xml_schema_collection* também for especificado. Caso não seja especificado, CONTENT será o comportamento padrão.  
  
DOCUMENT  
 Especifica que cada instância do tipo de dados **xml** em *column_name* pode abranger apenas um elemento de nível superior. DOCUMENT aplica-se apenas a tipo de dados **xml** e poderá ser especificado somente se *xml_schema_collection* também for especificado.  
  
 *xml_schema_collection*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Aplica-se apenas ao tipo de dados **xml** para associar uma coleção de esquemas XML ao tipo. Antes de digitar uma coluna **xml** em um esquema, o esquema deve ser criado primeiramente no banco de dados com [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
FILESTREAM  
 Especifica, opcionalmente, o atributo de armazenamento FILESTREAM para a coluna que tem um *type_name* igual a **varbinary(max)** .  
  
 Quando FILESTREAM é especificado para uma coluna, a tabela também deve ter uma coluna do tipo de dados **uniqueidentifier** que tem o atributo ROWGUIDCOL. Essa coluna não deve permitir valores nulos e deve ter uma restrição de coluna única UNIQUE ou PRIMARY KEY. O valor GUID da coluna deve ser fornecido por um aplicativo durante a inserção de dados, ou por uma restrição DEFAULT que utilize a função NEWID ().  
  
 A coluna ROWGUIDCOL não pode ser descartada e as restrições relacionadas não podem ser alteradas enquanto houver uma coluna FILESTREAM definida para a tabela. A coluna ROWGUIDCOL poderá ser descartada somente depois que a última coluna FILESTREAM for descartada.  
  
 Quando o atributo de armazenamento FILESTREAM é especificado para uma coluna, todos os valores da coluna são armazenados em um contêiner de dados FILESTREAM no sistema de arquivos.  
  
 Para obter um exemplo que mostra como usar a definição de coluna, consulte [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
COLLATE *collation_name*  
 Especifica a ordenação da coluna. Se não for especificado, à coluna será atribuída a ordenação padrão do banco de dados. O nome da ordenação tanto pode ser um nome de ordenação do Windows como um nome de ordenação SQL. Para obter uma lista e mais informações, veja [Nome da ordenação do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) e [Nome de ordenação do SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 A cláusula COLLATE pode ser usada para especificar as ordenações somente de colunas dos tipos de dados **char**, **varchar**, **nchar** e **nvarchar**.  
  
 Para obter mais informações sobre a cláusula COLLATE, veja [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).  
  
 NULL | NOT NULL  
 Determina se são permitidos valores nulos na coluna. NULL não é estritamente uma restrição, mas pode ser especificado simplesmente como NOT NULL.  
  
[ CONSTRAINT *constraint_name* ]  
 Especifica o início de uma definição de valor DEFAULT. Para manter a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um nome de restrição pode ser atribuído a um DEFAULT. *constraint_name* deve seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md), a menos que o nome não possa começar com uma tecla jogo da velha (#). Se *constraint_name* não for especificado, um nome gerado pelo sistema será atribuído à definição DEFAULT.  
  
DEFAULT  
 É uma palavra-chave que especifica o valor padrão para a coluna. Podem ser usadas definições DEFAULT para fornecer valores para uma coluna nova nas linhas existentes de dados. As definições de DEFAULT não podem ser aplicadas a colunas **timestamp** nem a colunas com uma propriedade IDENTITY. Se um valor padrão for especificado para uma coluna de tipo definido pelo usuário, o tipo deverá dar suporte a uma conversão implícita de *constant_expression* no tipo definido pelo usuário.  
  
*constant_expression*  
 É um valor literal, um NULL ou uma função de sistema usado como valor de coluna padrão. Se for usado em conjunto com uma coluna definida para ser de um tipo definido pelo usuário do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], a implementação do tipo deverá dar suporte a uma conversão implícita da *constant_expression* no tipo definido pelo usuário.  
  
WITH VALUES   
 Ao adicionar uma coluna E uma restrição DEFAULT, se a coluna permitir valores NULLS o uso de WITH VALUES definirá, para as linhas existentes, o valor da nova coluna como o valor fornecido em *constant_expression* DEFAULT. Se a coluna que está sendo adicionada não permitir valores NULLS, o valor da coluna sempre será definido, para as linhas existentes, como o valor fornecido na *expressão constante* DEFAULT. A partir do SQL Server 2012, essa pode ser uma operação de metadados [adicionando colunas não nulas como uma operação online](alter-table-transact-sql.md?view=sql-server-2017#adding-not-null-columns-as-an-online-operation).
Se isso for usado quando a coluna relacionada também não estiver sendo adicionada, não terá qualquer efeito.
 
 Especifica que o valor fornecido em DEFAULT *constant_expression* seja armazenado em uma nova coluna adicionada às linhas existentes. Se a coluna adicionada permitir valores nulos e WITH VALUES for especificado, o valor padrão será armazenado na nova coluna adicionada a linhas existentes. Se WITH VALUES não estiver especificado para colunas que permitem nulos, o valor NULL será armazenado na nova coluna nas linhas existentes. Se a nova coluna não permitir nulos, o valor padrão será armazenado em linhas novas, independentemente de WITH VALUES ser especificado.  
  
IDENTITY  
 Especifica que a coluna nova é uma coluna de identidade. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] fornece um valor exclusivo e de incremento para a coluna. Quando você adiciona colunas de identificador a tabelas existentes, os números de identidade são adicionados às linhas existentes da tabela, com os valores de semente e de incremento. A ordem em que as linhas são atualizadas não é garantida. Os números de identidade também são gerados para todas as linhas adicionadas.  
  
 As colunas de identidade, em geral, são usadas juntamente com restrições PRIMARY KEY para servir de identificador exclusivo de linha para a tabela. A propriedade IDENTITY pode ser atribuída a uma coluna **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)** ou **numeric(p,0)** . Apenas uma coluna de identidade pode ser criada por tabela. A palavra-chave DEFAULT e os padrões associados não podem ser usados com uma coluna de identidade. Ambos os valores de semente e de incremento devem ser identificados, ou nenhum dos dois. Se nenhum dos dois for especificado, o padrão será (1,1).  
  
> [!NOTE]  
>  Você não pode modificar uma coluna de tabela existente para adicionar a propriedade IDENTITY.  
  
 Não há suporte para a adição de uma coluna de identidade a uma tabela publicada porque pode resultar em não convergência quando a coluna for replicada ao Assinante. Os valores na coluna de identidade no Publicador dependerão da ordem em que as linhas para a tabela afetada forem armazenadas fisicamente. As linhas poderiam ser armazenadas diferentemente no Assinante; por isso, o valor para a coluna de identidade pode ser diferente para as mesmas linhas.  
  
 Para desabilitar a propriedade IDENTITY de uma coluna, permitindo a inserção explícita de valores, use [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md).  
  
*seed*  
 É o valor usado para a primeira linha carregada na tabela.  
  
*increment*  
 É o valor de incremento adicionado ao valor de identidade da linha anterior que é carregada.  
  
NOT FOR REPLICATION  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Pode ser especificado para a propriedade IDENTITY. Se essa cláusula for especificada para a propriedade IDENTITY, os valores não serão incrementados em colunas de identidade quando os agentes de replicação executarem operações insert.  
  
ROWGUIDCOL  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Especifica se a coluna é uma linha de coluna de identificador global exclusivo. ROWGUIDCOL pode ser atribuído somente a uma coluna **uniqueidentifier**, e somente uma coluna **uniqueidentifier** por tabela pode ser atribuída como a coluna ROWGUIDCOL. ROWGUIDCOL não pode ser atribuído a colunas de tipos de dados definidos pelo usuário.  
  
 ROWGUIDCOL não obriga exclusividade dos valores armazenados na coluna. Da mesma forma, ROWGUIDCOL não gera automaticamente valores para as novas linhas inseridas na tabela. Para gerar valores exclusivos para cada coluna, use a função NEWID em instruções INSERT ou especifique a função NEWID como o padrão para a coluna. Para obter mais informações, consulte [NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md) e [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
SPARSE  
 Indica que a coluna é uma coluna esparsa. O armazenamento de colunas esparsas é otimizado para obter valores nulos. Colunas esparsas não podem ser designadas como NOT NULL. Para obter restrições adicionais e mais informações sobre colunas esparsas, consulte [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).  
  
\<column_constraint>  
 Para obter as definições dos argumentos de restrição de coluna, consulte [column_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md).  
  
 ENCRYPTED WITH  
 Especifica as colunas de criptografia usando o recurso [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 Especifica a chave de criptografia de coluna. Para obter mais informações, veja [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED }  
 **Criptografia determinística** usa um método que sempre gera o mesmo valor criptografado para qualquer valor de texto não criptografado. Usar criptografia determinística permite pesquisar usando comparação de igualdade, agrupamento e junção de tabelas usando junções de igualdade baseadas em valores criptografados, mas também pode permitir que usuários não autorizados adivinhem informações sobre valores criptografados examinando padrões na coluna criptografada. A união de duas tabelas em colunas criptografadas de maneira determinística só é possível se ambas as colunas são criptografadas com a mesma chave de criptografia de coluna. A criptografia determinística deve usar uma ordenação de colunas com uma ordem de classificação binary2 para as colunas de caracteres.  
  
 **Criptografia aleatória** usa um método que criptografa os dados de uma maneira menos previsível. A criptografia aleatória é mais segura, mas impede que cálculos e indexação sejam feitos em colunas criptografadas, a menos que sua instância do SQL Server tenha suporte para [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).
  
 Se você estiver usando o Always Encrypted (sem enclaves seguros), use a criptografia determinística para que as colunas sejam pesquisadas com parâmetros ou com parâmetros de agrupamento, por exemplo, um número de identificação do governo. Use criptografia randomizada para dados como número de cartão de crédito, que não são agrupados a outros registros nem usados para unir tabelas e que não são pesquisados porque você usa outras colunas (como número de transações) para localizar a linha que contém a coluna criptografada de interesse.  

 Se você está usando o Always Encrypted com enclaves seguros, a criptografia aleatória é um tipo de criptografia recomendado.  
  
 As colunas devem ser de um tipo de dados qualificado.  
  
ALGORITHM  
**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
Deve ser **'AEAD_AES_256_CBC_HMAC_SHA_256'** .  
  
 Para mais informações, incluindo restrições de recursos, veja [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
   
ADD MASKED WITH ( FUNCTION = ' *mask_function* ')  
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica uma máscara de dados dinâmicos. *mask_function* é o nome da função de mascaramento com os parâmetros apropriados. As seguintes opções estão disponíveis:  
  
-   default()  
  
-   email()  
  
-   partial()  
  
-   random()  
  
 Para parâmetros de função, consulte [Máscara de Dados Dinâmicos](../../relational-databases/security/dynamic-data-masking.md).  
  
## <a name="remarks"></a>Comentários  
 Se a coluna adicionada tiver um tipo de dados **uniqueidentifier**, ela poderá ser definida com um padrão que usa a função NEWID() para fornecer os valores de identificador exclusivo na nova coluna para cada linha existente da tabela.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não impõe uma ordem para especificar DEFAULT, IDENTITY, ROWGUIDCOL nem restrições de coluna em uma definição de coluna.  
  
 A instrução ALTER TABLE falhará se a adição da coluna fizer com que o tamanho da linha de dados exceda 8060 bytes.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos, consulte [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
