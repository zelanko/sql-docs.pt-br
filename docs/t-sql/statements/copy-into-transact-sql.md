---
title: COPY INTO (Transact-SQL) (versão prévia)
titleSuffix: (SQL Data Warehouse) - SQL Server
description: Use a instrução COPY no SQL Data Warehouse do Azure para carregar de contas de armazenamento externo.
ms.date: 11/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COPY_TSQL
- COPY INTO
- COPY
- LOAD
dev_langs:
- TSQL
author: kevinvngo
ms.author: kevin
monikerRange: =sqlallproducts-allversions||=azure-sqldw-latest
ms.openlocfilehash: fc26cc0862c7dfb02276738d9424b860d98644e7
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882411"
---
# <a name="copy-transact-sql-preview"></a>COPY (Transact-SQL) (versão prévia)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Este artigo explica como usar a instrução COPY no SQL Data Warehouse do Azure para carregar de contas de armazenamento externo. A instrução COPY fornece a maior flexibilidade para a ingestão de dados com alta taxa de transferência no SQL Data Warehouse.

> [!NOTE]  
> Atualmente, a instrução COPY está em visualização pública.

## <a name="syntax"></a>Sintaxe  

```
COPY INTO [schema.]table_name
[(Column_list)] 
FROM ‘<external_location>’ [,...n]
WITH  
 ( 
 [FILE_TYPE = {'CSV' | 'PARQUET' | 'ORC'} ]
 [,FILE_FORMAT = EXTERNAL FILE FORMAT OBJECT ]  
 [,CREDENTIAL = (AZURE CREDENTIAL) ]
 [,ERRORFILE = '[http(s)://storageaccount/container]/errorfile_directory[/]] 
 [,ERRORFILE_CREDENTIAL = (AZURE CREDENTIAL) ]
 [,MAXERRORS = max_errors ] 
 [,COMPRESSION = { 'Gzip' | 'DefaultCodec'|’Snappy’}] 
 [,FIELDQUOTE = ‘string_delimiter’] 
 [,FIELDTERMINATOR =  ‘field_terminator’]  
 [,ROWTERMINATOR = ‘row_terminator’]
 [,FIRSTROW = first_row]
 [,DATEFORMAT = ‘date_format’] 
 [,ENCODING = {'UTF8'|'UTF16'}] 
 [,IDENTITY_INSERT = {‘ON’ | ‘OFF’}]
)
```

## <a name="arguments"></a>Argumentos  

*schema_name*  
Será opcional se o esquema padrão do usuário que está executando a operação for o esquema da tabela especificada. Se o *esquema* não for especificado e o esquema padrão do usuário que está executando a operação COPY for diferente da tabela especificada, COPY será cancelada e uma mensagem de erro será retornada.  

*table_name*  
É o nome da tabela para a qual os dados serão copiados por meio da operação COPY. A tabela de destino pode ser uma tabela temporária ou permanente.

*(column_list)*  
É uma lista opcional de uma ou mais colunas usadas para mapear campos de dados de origem para colunas da tabela de destino para carregar dados. *column_list* deve ser colocada entre parênteses e separada por vírgulas. A lista de colunas tem o formato a seguir:

[(Column_name [Default_value] [Field_number] [,...n])]

- *Column_name* – é o nome da coluna na tabela de destino.
- *Default_value* – o valor padrão que substituirá qualquer valor nulo no arquivo de entrada. O valor padrão se aplica a todos os formatos de arquivo. COPY tentará carregar NULL do arquivo de entrada quando uma coluna for omitida da lista de colunas ou quando houver um campo de arquivo de entrada vazio.
- *Field_number* – o número do campo do arquivo de entrada que será mapeado para o nome da coluna de destino.
- A indexação de campos começa em 1.

Quando uma lista de colunas não for especificada, COPY mapeará as colunas com base na ordinalidade da origem e do destino: O campo de entrada 1 vai para a coluna de destino 1, o campo 2 vai para a coluna 2 etc.

*Locais externos*</br>
É onde os arquivos que contêm os dados são preparados. Atualmente, o ADLS (Azure Data Lake Storage) Gen2 e o Armazenamento de Blobs do Azure têm suporte:

- *Local externo* para o Armazenamento de Blobs: https://<account>.blob.core.windows.net/<container>/<path>
- *Local externo* para o ADLS Gen2: https://<account>. dfs.core.windows.net/<container>/<path>

> [!NOTE]  
> O ponto de extremidade do blob está disponível para o ADLS Gen2 e é destinado apenas a compatibilidade com versões anteriores. Use o ponto de extremidade **dfs** para o ADLS Gen2 para obter um melhor desempenho.

- *Conta* – o nome da conta de armazenamento

- *Contêiner* – o nome do contêiner de blobs

- *Caminho* – a pasta ou o caminho do arquivo para os dados. O local inicia do contêiner. Se uma pasta for especificada, COPY recuperará todos os arquivos da pasta e de todas as suas subpastas. COPY ignora pastas ocultas e não retorna arquivos que começam com um sublinhado (_) ou um ponto final (.), a menos que especificado explicitamente no caminho. Esse comportamento permanece mesmo quando é especificado um caminho com um curinga.

Cartões curingas podem ser incluídos no caminho em que

- A correspondência do nome de caminho curinga diferencia maiúsculas de minúsculas
- É possível efetuar o escape do curinga usando o caractere de barra invertida (\\)
- A expansão do curinga é aplicada recursivamente. Por exemplo, todos os arquivos CSV em Customer1 (incluindo subdiretórios de Customer1) serão carregados no exemplo a seguir: ‘Account/Container/Customer1/*.csv’

> [!NOTE]  
> Para obter o melhor desempenho, evite especificar curingas que se expandiriam em um número maior de arquivos. Se possível, liste vários locais de arquivo em vez de especificar curingas.

Vários locais de arquivo só podem ser especificados na mesma conta de armazenamento e contêiner por meio de uma lista separada por vírgulas, como:

- ‘ https://<account>.blob.core.windows.net/<container>/<path>’, ‘ https://<account>.blob.core.windows.net/<container>/<path>’…

*FILE_TYPE = { ‘CSV’ | ‘PARQUET’ | ‘ORC’ }*</br>
*FILE_TYPE* especifica o formato dos dados externos.

- CSV: especifica um arquivo de valores separados por vírgula em conformidade com o padrão [RFC 4180](https://tools.ietf.org/html/rfc4180).
- PARQUET: especifica um formato Parquet.
- ORC: Especifica um formato ORC (Optimized Row Columnar).

>[!NOTE]  
> O tipo de arquivo “ Texto Delimitado” no Polybase é substituído pelo formato de arquivo “CSV”, no qual o delimitador de vírgula padrão pode ser configurado por meio do parâmetro FIELDTERMINATOR. 

*FILE_FORMAT = external_file_format_name*</br>
*FILE_FORMAT* aplica-se somente a arquivos Parquet e ORC e especifica o nome do objeto de formato de arquivo externo que armazena o tipo de arquivo e o método de compactação dos dados externos. Para criar um formato de arquivo externo, use [CREATE EXTERNAL FILE FORMAT](create-external-file-format-transact-sql.md?view=azure-sqldw-latest).

*CREDENTIAL (IDENTITY = ‘’, SECRET = ‘’)*</br>
*CREDENTIAL* especifica o mecanismo de autenticação para acessar a conta de armazenamento externo. Os métodos de autenticação são:

|                          |                CSV                |              Parquet              |                ORC                |
| :----------------------: | :-------------------------------: | :-------------------------------: | :-------------------------------: |
|  **Armazenamento de Blobs do Azure**  | SAS/MSI/SERVICE PRINCIPAL/KEY/AAD |              SAS/KEY              |              SAS/KEY              |
| **Azure Data Lake Gen2** | SAS/MSI/SERVICE PRINCIPAL/KEY/AAD | SAS/MSI/SERVICE PRINCIPAL/KEY/AAD | SAS/MSI/SERVICE PRINCIPAL/KEY/AAD |

Ao autenticar usando o AAD ou uma conta de armazenamento pública, o valor de CREDENTIAL não precisa ser especificado. 

- Autenticação com SAS (Assinaturas de Acesso Compartilhado) *IDENTITY: Uma constante com um valor de “Assinatura de Acesso Compartilhado”* 
  *SECRET: A *[*assinatura de acesso compartilhado*](/azure/storage/common/storage-sas-overview#what-is-a-shared-access-signature)* fornece acesso delegado aos recursos em sua conta de armazenamento.*
  Permissões mínimas necessárias: READ e LIST

- Autenticação com [*Entidades de Serviço*](/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store#create-a-credential)

  *IDENTITY: <ClientID>@<OAuth_2.0_Token_EndPoint>* 
  *SECRET: Chave de Entidade de Serviço de Aplicativo do AAD* Funções de RBAC mínimas necessárias: Colaborador de dados do blob de armazenamento, colaborador de dados do blob de armazenamento, proprietário de dados do blob de armazenamento ou leitor de dados do blob de armazenamento

  > [!NOTE]  
  > Use o ponto de extremidade do token OAuth 2.0 **V1**

- Autenticação com a chave da conta de armazenamento *IDENTITY: Uma constante com o valor da “Chave de Conta de Armazenamento*
  *SECRET: Chave de conta de armazenamento*
  
- Autenticação com [Identidade Gerenciada](/azure/sql-data-warehouse/load-data-from-azure-blob-storage-using-polybase#authenticate-using-managed-identities-to-load-optional) (Pontos de Extremidade de Serviço de VNet) *IDENTITY: Uma constante com um valor de "Identidade Gerenciada"* Funções de RBAC mínimas necessárias: colaborador de dados do blob de armazenamento, proprietário de dados do blob de armazenamento ou leitor de dados do blob de armazenamento para o Servidor do banco de dados SQL registrado no AAD 
  
- Autenticação com um usuário do AAD *CREDENTIAL não é necessária* Funções de RBAC mínimas necessárias: colaborador de dados do blob de armazenamento, proprietário de dados do blob de armazenamento ou leitor de dados do blob de armazenamento para o usuário do AAD

*ERRORFILE = local do diretório*</br>
*ERRORFILE* aplica-se somente ao CSV. Especifica o diretório na instrução COPY em que as linhas rejeitadas e o arquivo de erro correspondente devem ser gravados. O caminho completo da conta de armazenamento ou o caminho relativo do contêiner pode ser especificado. Se o caminho especificado não existir, um será criado em seu nome. Um diretório filho é criado com o nome "_rejectedrows". O caractere "_ " garante que o diretório tenha escape para outro processamento de dados, a menos que explicitamente nomeado no parâmetro de localização. 

Dentro desse diretório, há uma pasta criada com base na hora do envio do carregamento no formato YearMonthDay – HourMinuteSecond (por exemplo, 20180330-173205). Nessa pasta, dois tipos de arquivos são gravados, o arquivo de motivo (erro) e o arquivo de dados (linha), cada um anexado previamente com o queryID, o distributionID e um GUID do arquivo. Já que os dados e o motivo estão em arquivos separados, arquivos correspondentes têm um prefixo correspondente.

Se ERRORFILE tiver o caminho completo da conta de armazenamento definido, a ERRORFILE_CREDENTIAL será usada para se conectar a esse armazenamento. Caso contrário, o valor mencionado para CREDENTIAL será usado.

*ERRORFILE_CREDENTIAL = (IDENTITY= ‘’, SECRET = ‘’)*</br>
*ERRORFILE_CREDENTIAL* aplica-se somente a arquivos CSV. As fontes de dados e os métodos de autenticação com suporte são:

- Armazenamento de Blobs do Azure – SAS/SERVICE PRINCIPAL/KEY/AAD
- Azure Data Lake Gen2 – SAS/MSI/SERVICE PRINCIPAL/KEY/AAD
  
- Autenticação com SAS (Assinaturas de Acesso Compartilhado)
  - *IDENTITY: uma constante com um valor de “Assinatura de Acesso Compartilhado”*
  - *SECRET: A* [*assinatura de acesso compartilhado*](/azure/storage/common/storage-dotnet-shared-access-signature-part-1#what-is-a-shared-access-signature) *fornece acesso delegado aos recursos em sua conta de armazenamento.*
  - Permissões mínimas necessárias: READ, LIST, WRITE, CREATE, DELETE
  
- Autenticação com [*Entidades de Serviço*](/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store#create-a-credential)
  - *IDENTITY: <ClientID>@<OAuth_2.0_Token_EndPoint>*
  - *SECRET: chave da Entidade de Serviço de Aplicativo do AAD*
  - Funções de RBAC mínimas necessárias: colaborador de dados do blob de armazenamento ou proprietário de dados do blob de armazenamento
  
> [!NOTE]  
> Use o ponto de extremidade do token OAuth 2.0 **V1**

- Autenticação com a chave da conta de armazenamento
  - *IDENTITY: uma constante com o valor da “Chave de Conta de Armazenamento”*
  - *SECRET: Chave de conta de armazenamento*
  
- Autenticação com [Identidade Gerenciada](/azure/sql-data-warehouse/load-data-from-azure-blob-storage-using-polybase#authenticate-using-managed-identities-to-load-optional) (Pontos de Extremidade de Serviço de VNet)
  - *IDENTITY: uma constante com um valor de “Identidade Gerenciada”*
  - Funções de RBAC mínimas necessárias: colaborador de dados do blob de armazenamento ou proprietário de dados do blob de armazenamento para o Servidor do banco de dados SQL registrado no AAD
  
- Autenticação com um usuário do AAD
  - *CREDENTIAL não é necessária*
  - Funções de RBAC mínimas necessárias: colaborador de dados do blob de armazenamento ou proprietário de dados do blob de armazenamento para o usuário do AAD

> [!NOTE]  
> Se estiver usando a mesma conta de armazenamento para ERRORFILE e especificando o caminho de ERRORFILE relativo à raiz do contêiner, você não precisará especificar a ERROR_CREDENTIAL.

*MAXERRORS = max_errors*</br>
*MAXERRORS* especifica o número máximo de linhas rejeitadas permitido nos carregamento antes que a operação COPY seja cancelada. Cada linha que não pode ser importada pela operação COPY é ignorada e contada como um erro. Se max_errors não for especificado, o padrão será 0.

*COMPRESSION = { 'DefaultCodec '| ’Snappy’ | ‘GZIP’ | ‘NONE’}*</br>
*COMPRESSION* é opcional e especifica o método de compactação de dados para os dados externos.

- CSV dá suporte a GZIP
- Parquet dá suporte a GZIP e Snappy
- ORC dá suporte a DefaultCodec e Snappy.
- Zlib é a compactação padrão do ORC

O comando COPY detectará automaticamente o tipo de compactação com base na extensão do arquivo quando esse parâmetro não for especificado:

- .gz  – **GZIP**
- .snappy – **Snappy**
- .deflate – **DefaultCodec**

 *FIELDQUOTE = 'field_quote'*</br>
*FIELDQUOTE* aplica-se a CSV e especifica um único caractere que será usado como o caractere de aspas (delimitador de cadeia de caracteres) no arquivo CSV. Se não for especificado, o caractere de aspas (") será usado como o caractere de aspas, conforme definido no padrão RFC 4180. Não há suporte para caracteres ASCII estendidos com UTF-8 para FIELDQUOTE.

> [!NOTE]  
> O escape dos caracteres FIELDQUOTE é efetuado em colunas de cadeia de caracteres em que há a presença de um FIELDQUOTE (delimitador) duplo. 

*FIELDTERMINATOR = 'field_terminator’*</br>
*FIELDTERMINATOR* aplica-se somente ao CSV. Especifica o terminador de campo que será usado no arquivo CSV. O terminador de campo pode ter vários caracteres. O terminador de campo padrão é um (,).
Para obter mais informações, confira [Especificar terminadores de campo e linha (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md?view=sql-server-2017).

ROW TERMINATOR = 'row_terminator'</br>
*ROW TERMINATOR* aplica-se somente ao CSV. Especifica o terminador de linha que será usado no arquivo CSV. O terminador de linha pode ter vários caracteres. Por padrão, o terminador de linha é \r\n. 

O comando COPY prefixa o caractere \r ao especificar \n (nova linha), resultando em \r\n. Para especificar apenas o caractere \n, use o formato hexadecimal (0x0A). Ao especificar terminadores de linha de vários caracteres em formato hexadecimal, não especifique 0x entre cada caractere.

Consulte a [documentação](https://docs.microsoft.com/sql/relational-databases/import-export/specify-field-and-row-terminators-sql-server?view=sql-server-2017#using-row-terminators) a seguir para obter diretrizes adicionais sobre como especificar terminadores de linha.

*FIRSTROW  = First_row_int*</br>
*FIRSTROW* aplica-se a CSV e especifica o número da linha que é lida primeiro em todos os arquivos para o comando COPY. Os valores começam com 1, que é o valor padrão. Se o valor for definido como dois, a primeira linha em todos os arquivos (linha de cabeçalho) será ignorada quando os dados forem carregados. As linhas são ignoradas com base na existência de terminadores de linhas.

*DATEFORMAT = { ‘mdy’ | ‘dmy’ | ‘ymd’ | ‘ydm’ | ‘myd’ | ‘dym’ }*</br>
DATEFORMAT aplica-se somente ao CSV e especifica o formato de data do mapeamento de data dos formatos de data do SQL Server. Para ter uma visão geral de todas as funções e tipos de dados de data e hora do Transact-SQL, confira [Funções e tipos de dados de data e hora (Transact-SQL)](../functions/date-and-time-data-types-and-functions-transact-sql.md?view=sql-server-ver15). DATEFORMAT no comando COPY tem precedência sobre [DATEFORMAT configurado no nível da sessão](set-dateformat-transact-sql.md?view=sql-server-ver15).

*ENCODING = ‘UTF8’ | ‘UTF16’*</br>
*ENCODING* aplica-se somente ao CSV. O padrão é UTF8. Especifica o padrão da codificação de dados para os arquivos carregados pelo comando COPY. 

*IDENTITY_INSERT = ‘ON’ | ‘OFF’*</br>
IDENTITY_INSERT especifica se os valores de identidade no arquivo de dados importado devem ser usados para a coluna de identidade. Se o valor de IDENTITY_INSERT for OFF (padrão), os valores de identidade para essa coluna serão verificados, mas não importados. O SQL DW atribuirá automaticamente valores exclusivos com base nos valores de semente e incremento especificados durante a criação da tabela. Observe o seguinte comportamento com o comando COPY:

- Se o valor de IDENTITY_INSERT for OFF e a tabela tiver uma coluna de identidade
  - Deverá ser especificada uma lista de colunas que não mapeia um campo de entrada para a coluna de identidade.
- Se o valor de IDENTITY_INSERT for ON e a tabela tiver uma coluna de identidade
  - Se uma lista de colunas for passada, ela deverá mapear um campo de entrada para a coluna de identidade.
- O valor padrão não tem suporte para IDENTITY COLUMN na lista de colunas.
- IDENTITY_INSERT só pode ser definida para uma tabela por vez.

### <a name="permissions"></a>Permissões  

O usuário que executa o comando de cópia deve ter as seguintes permissões: 

- [ADMINISTER DATABASE BULK OPERATIONS](grant-database-permissions-transact-sql.md?view=azure-sqldw-latest#remarks)
- [INSERT ](grant-database-permissions-transact-sql.md?view=azure-sqldw-latest#remarks)

Requer as permissões INSERT e ADMINISTER BULK OPERATIONS. No SQL Data Warehouse do Azure, são necessárias permissões INSERT e ADMINISTER DATABASE BULK OPERATIONS.

## <a name="examples"></a>Exemplos  

### <a name="a-load-from-a-public-storage-account"></a>A. Carregar de uma conta de armazenamento público

O exemplo a seguir é a forma mais simples do comando COPY, que carrega dados de uma conta de armazenamento público. Para este exemplo, os padrões da instrução COPY correspondem ao formato do arquivo CSV de item de linha.

```sql
COPY INTO dbo.[lineitem] FROM 'https://unsecureaccount.blob.core.windows.net/customerdatasets/folder1/lineitem.csv’
```

Os valores padrão do comando COPY são:

- DATEFORMAT = DATEFORMAT da sessão 

- MAXERRORS = 0

- O padrão de COMPRESSION é descompactado

- FIELDQUOTE = “” 

- FIELDTERMINATOR = “,” 

- ROWTERMINATOR = ‘\n'

> [!IMPORTANT]
> COPY trata '\n' como '\r\n' internamente. Para obter mais informações, confira a seção [ROWTERMINATOR]().

- FIRSTROW = 1

- ENCODING = ‘UTF8’

- FILE_TYPE = ‘CSV’

- IDENTITY_INSERT = ‘OFF’

### <a name="b-load-authenticating-via-share-access-signature-sas"></a>B. Autenticação de carga via SAS (Assinatura de Acesso Compartilhado)

O exemplo a seguir carrega arquivos que usam a alimentação de linha como um terminador de linha, como uma saída UNIX. Este exemplo também usa uma chave de SAS para autenticação no Armazenamento de Blobs do Azure.

```sql
COPY INTO test_1
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/'
WITH (
    FILE_TYPE = 'CSV',
    CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='<Your_SAS_Token>'),
    --CREDENTIAL should look something like this:
    --CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='?sv=2018-03-28&ss=bfqt&srt=sco&sp=rl&st=2016-10-17T20%3A14%3A55Z&se=2021-10-18T20%3A19%3A00Z&sig=IEoOdmeYnE9%2FKiJDSHFSYsz4AkNa%2F%2BTx61FuQ%2FfKHefqoBE%3D'),
    FIELDQUOTE = '"',
    FIELDTERMINATOR=';',
    ROWTERMINATOR='0X0A',
    ENCODING = 'UTF8',
    DATEFORMAT = 'ymd',
    MAXERRORS = 10,
    ERRORFILE = '/errorsfolder/',--path starting from the storage container
    IDENTITY_INSERT = ‘ON’
)
```

### <a name="c-load-with-a-column-list-with-default-values-authenticating-via-storage-account-key"></a>C. Carregar com uma lista de colunas com valores padrão, autenticando por meio da Chave da Conta de Armazenamento

Este exemplo carrega arquivos especificando uma lista de colunas com valores padrão. 

```sql
--Note when specifying the column list, input field numbers start from 1
COPY INTO test_1 (Col_one default 'myStringDefault' 1, Col_two default 1 3)
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/'
WITH (
    FILE_TYPE = 'CSV',
    CREDENTIAL=(IDENTITY= 'Storage Account Key', SECRET='<Your_Account_Key>'),
    --CREDENTIAL should look something like this:
    --CREDENTIAL=(IDENTITY= 'Storage Account Key', SECRET='x6RWv4It5F2msnjelv3H4DA80n0PQW0daPdw43jM0nyetx4c6CpDkdj3986DX5AHFMIf/YN4y6kkCnU8lb+Wx0Pj+6MDw=='),
    FIELDQUOTE = '"',
    FIELDTERMINATOR=',',
    ROWTERMINATOR='0x0A',
    ENCODING = 'UTF8',
    FIRSTROW = 2
)
```

### <a name="d-load-parquet-or-orc-using-existing-file-format-object"></a>D. Carregar Parquet ou ORC usando o objeto de formato de arquivo existente

 Este exemplo usa um curinga para carregar todos os arquivos parquet em uma pasta. 

```sql
COPY INTO test_parquet
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/*.parquet'
WITH (
    FILE_FORMAT = myFileFormat
    CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='<Your_SAS_Token>')
)
```

### <a name="e-load-specifying-wild-cards-and-multiple-files"></a>E. Carga especificando curingas e vários arquivos

```sql
COPY INTO t1
FROM 
'https://myaccount.blob.core.windows.net/myblobcontainer/folder0/*.txt', 
    'https://myaccount.blob.core.windows.net/myblobcontainer/folder1'
WITH ( 
    FILE_TYPE = 'CSV'
    CREDENTIAL=(IDENTITY= '<client_id>@<OAuth_2.0_Token_EndPoint>',SECRET='<key>'),
    FIELDTERMINATOR = '|'
)
```

## <a name="see-also"></a>Confira também  

 [Visão geral do carregamento com o SQL Data Warehouse](/azure/sql-data-warehouse/design-elt-data-loading>) 
