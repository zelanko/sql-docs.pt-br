---
title: Configurar o PolyBase para acessar dados externos no MongoDB | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c4ccf371cdcac99d50c3142ec42641380623501
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044492"
---
# <a name="configure-polybase-to-access-external-data-in-mongodb"></a>Configurar o PolyBase para acessar dados externos no MongoDB

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos no MongoDB.

## <a name="prerequisites"></a>Prerequisites

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md).

## <a name="configure-an-external-table"></a>Configurar uma tabela externa

Para consultar os dados de uma fonte de dados do MongoDB, você precisa criar tabelas externas para fazer referência aos dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas.

Estes objetos serão criados nesta seção:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)
- CREATE EXTERNAL DATA SOURCE (Transact-SQL)
- CREATE EXTERNAL TABLE (Transact-SQL)
- CREATE STATISTICS (Transact-SQL)

1. Crie uma chave mestra no banco de dados, caso ainda não exista. Isso é necessário para criptografar o segredo da credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>Argumentos
    PASSWORD ='password'

    É a senha usada para criptografar a chave mestra no banco de dados. password precisa atender aos requisitos da política de senha do Windows do computador que está hospedando a instância do SQL Server.

1.   Crie uma credencial no escopo do banco de dados para acessar a origem do MongoDB.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name 
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1.  Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

     ```sql
     /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (
    LOCATION = mongodb://<server>[:<port>],
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = credential_name
    );
     ```

1.  Crie tabelas externas que representem os dados armazenados no sistema do MongoDB externo [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).

     ```sql
     /*  LOCATION: MongoDB table/view in '<database_name>.<schema_name>.<object_name>' format
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE customers(
     [O_ORDERKEY] DECIMAL(38) NOT NULL,
     [O_CUSTKEY] DECIMAL(38) NOT NULL,
     [O_ORDERSTATUS] CHAR COLLATE Latin1_General_BIN NOT NULL,
     [O_TOTALPRICE] DECIMAL(15,2) NOT NULL,
     [O_ORDERDATE] DATETIME2(0) NOT NULL,
     [O_COMMENT] VARCHAR(79) COLLATE Latin1_General_BIN NOT NULL
     )
     WITH (
     LOCATION='customer',
     DATA_SOURCE= external_data_source_name
     );
     ```

1. **Opcional:** Crie estatísticas em uma tabela externa.

    É recomendável criar estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações, a fim de ter o desempenho de consulta ideal.

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```


## <a name="flattening"></a>Nivelamento
 O nivelamento é habilitado para os dados aninhados e repetidos das coleções de documentos do MongoDB. O usuário precisa habilitar `create an external table` e especificar explicitamente um esquema relacional nas coleções de documentos do MongoDB que possam ter dados repetidos e/ou aninhados. Habilitaremos a detecção de esquema automático em coleções de documentos do mongo em etapas futuras.
Os tipos de dados repetidos/aninhados do JSON serão nivelados da seguinte forma

* Objetos: coleção de chave-valor não ordenada entre chaves (aninhada)

   - Criaremos uma coluna de tabela para cada chave de objeto

     * Nome da coluna: objectname_keyname

* Matriz: valores ordenados, separados por vírgulas, entre colchetes (repetidos)

   - Adicionaremos uma nova linha da tabela para cada item da matriz

   - Criaremos uma coluna por matriz para armazenar o índice do item da matriz

     * Nome da coluna: arrayname_index

     * Tipo de dados: bigint

Há vários possíveis problemas com essa técnica, dois deles sendo:

* um campo repetido vazio mascarará efetivamente os dados contidos nos campos nivelados no mesmo registro

* a presença de vários campos repetidos pode resultar em uma explosão do número de linhas produzidas

Como exemplo, avaliamos a coleção do restaurante do conjunto de dados de amostra do MongoDB armazenada no formato JSON não relacional. Cada restaurante tem um campo de endereço aninhado e uma matriz de classificações atribuídas a ele em dias diferentes. A figura a seguir ilustra um restaurante típico com o endereço aninhado e notas aninhadas repetidas.

![Nivelamento do MongoDB](../../relational-databases/polybase/media/mongo-flattening.png "Nivelamento de restaurante do MongoDB")

O endereço do objeto será nivelado conforme abaixo:

* O campo aninhado restaurant.address.building se torna restaurant.address_building
* O campo aninhado restaurant.address.coord se torna restaurant.address_coord
* O campo aninhado restaurant.address.street se torna restaurant.address_street
* O campo aninhado restaurant.address.zipcode se torna restaurant.address_zipcode

As classificações da matriz serão niveladas conforme abaixo:

| grades_date | grades_grade  | games_score | 
| ------------- | ------------------------- | -------------- |
|1393804800000 |Um |2|
|1378857600000|Um |6|
|135898560000 |Um |10|
|1322006400000|Um |9|
|1299715200000 |B |14|

## <a name="cosmos-db-connection"></a>Conexão do Cosmos DB

Usando a API do mongo do Cosmos DB e o conector do PolyBase do Mongo DB, você pode criar uma tabela externa de uma **instância do Cosmos DB**. Isso pode ser feito seguindo as mesmas etapas listadas acima. Verifique se as credenciais, o endereço do servidor, a porta e a cadeia de caracteres de localização no escopo do banco de dados refletem os do servidor do Cosmos DB. 

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
