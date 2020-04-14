---
title: Acesso a dados em massa no Armazenamento de Blobs do Azure
description: Estes exemplos de Transact-SQL mostram como usar as instruções BULK INSERT e OPENROWSET para acessar diretamente um arquivo em uma conta do Armazenamento de Blobs do Azure.
ms.description: Transact-SQL examples that use BULK INSERT and OPENROWSET to access data in an Azure Blob storage account.
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], from Azure blob storage
- Azure blob storage, bulk import to SQL Server
- BULK INSERT, Azure blob storage
- OPENROWSET, Azure blob storage
ms.assetid: f7d85db3-7a93-400e-87af-f56247319ecd
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 4ed55e856a6a23da04b6f3a2812699c2b457a220
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980449"
---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>Exemplos de acesso a dados em massa no Armazenamento de Blobs do Azure

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

As instruções `BULK INSERT` e `OPENROWSET` podem acessar diretamente um arquivo no armazenamento de blobs do Azure. Os exemplos a seguir usam dados de um arquivo CSV (valores separados por vírgula) (denominado `inv-2017-01-19.csv`), armazenado em um contêiner (chamado `Week3`), armazenado em uma conta de armazenamento (chamada `newinvoices`). O caminho para o arquivo de formato pode ser usado, mas não está incluído nesses exemplos.

O acesso em massa para o armazenamento de blobs do Azure do SQL Server requer, no mínimo, [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.

> [!IMPORTANT]
> Todos os caminhos para o contêiner e os arquivos de blob são `CASE SENSITIVE`. Se não estiver correto, poderá retornar um erro como "Não é possível carregar em massa. O arquivo "file.csv" não existe ou você não tem direitos de acesso ao arquivo".

## <a name="create-the-credential"></a>Criar credencial

Todos os exemplos a seguir exigem uma credencial com escopo de banco de dados fazendo referência a uma assinatura de acesso compartilhado.

> [!IMPORTANT]
> A fonte de dados externa deve ser criada com uma credencial com escopo de banco de dados que usa a identidade `SHARED ACCESS SIGNATURE`. Para criar uma assinatura de acesso compartilhado para sua conta de armazenamento, consulte a propriedade **Assinatura de acesso compartilhado** na página de propriedades da conta de armazenamento, no portal do Azure. Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Para mais informações, consulte [CRIAR CREDENCIAL COM ESCOPO DE BANCO DE DADOS](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

Crie uma credencial com escopo de banco de dados usando o `IDENTITY`, que deve ser `SHARED ACCESS SIGNATURE`. Use o token SAS gerado para a conta de armazenamento de blobs. Verifique se o token SAS não tem um entrelinhamento `?`, se você tem pelo menos permissão de leitura no objeto que deve ser carregado e se o período de expiração é válido (todas as datas estão em UTC).

Por exemplo:

```sql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'sv=2018-03-28&ss=b&srt=sco&sp=rwdlac&se=2019-08-31T02:25:19Z&st=2019-07-30T18:25:19Z&spr=https&sig=KS51p%2BVnfUtLjMZtUTW1siyuyd2nlx294tL0mnmFsOk%3D';
```

## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>Acessando dados em um arquivo CSV que referencia um local de armazenamento de blobs do Azure

O exemplo a seguir usa uma fonte de dados externa apontando para uma conta de armazenamento do Azure, denominada `MyAzureInvoices`.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net',
        CREDENTIAL = UploadInvoices
    );
```

A instrução `OPENROWSET` adiciona o nome do contêiner (`week3`) à descrição do arquivo. O arquivo é denominado `inv-2017-01-19.csv`.

```sql
SELECT * FROM OPENROWSET(
   BULK 'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;   
```

Usando `BULK INSERT`, use o contêiner e a descrição do arquivo:

```sql
BULK INSERT Colors2
FROM 'week3/inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
      FORMAT = 'CSV');
```

## <a name="accessing-data-in-a-csv-file-referencing-a-container-in-an-azure-blob-storage-location"></a>Acessando dados em um arquivo CSV que referencia um contêiner em um local de armazenamento de blobs do Azure

O exemplo a seguir usa uma fonte de dados externa apontando para um contêiner (denominado `week3`) em uma conta de armazenamento do Azure.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoicesContainer
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = UploadInvoices
    );
```

A instrução `OPENROWSET` não adiciona o nome do contêiner à descrição do arquivo:

```sql
SELECT * FROM OPENROWSET(
   BULK 'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;
```

Usando `BULK INSERT`, não use o nome do contêiner na descrição do arquivo:

```sql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV');
```

## <a name="see-also"></a>Consulte Também

- [CRIAR UMA CREDENCIAL NO ESCOPO DO BANCO DE DADOS](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
