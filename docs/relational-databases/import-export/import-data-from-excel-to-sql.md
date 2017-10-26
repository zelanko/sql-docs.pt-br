---
title: Importar dados do Excel para o SQL | Microsoft Docs
ms.custom: 
ms.date: 08/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: ab792aed71ab2e7837da9cf0073d4ff191ce5184
ms.openlocfilehash: ce462c238c81a4a9fc82869a856ac13e9f112aee
ms.contentlocale: pt-br
ms.lasthandoff: 08/05/2017

---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>Importar dados do Excel para o SQL Server ou Banco de Dados SQL do Azure
Há várias maneiras de importar dados de arquivos do Excel para o SQL Server ou para o Banco de Dados SQL do Azure. Este artigo resume cada uma dessas opções e fornece links para instruções mais detalhadas.
-   Você pode importar dados em uma única etapa do Excel para SQL, usando uma das ferramentas a seguir:
    -   O Assistente de importação e exportação do SQL Server
    -   SQL Server Integration Services (SSIS)
    -   A função OPENROWSET
-   É possível importar dados em duas etapas, salvando seus dados como texto e, em seguida, usando uma das ferramentas a seguir:
    -   A instrução BULK INSERT
    -   BCP
    -   Azure Data Factory

> [!IMPORTANT]
> Uma descrição completa das ferramentas e serviços complexos, como SSIS ou Azure Data Factory, está além do escopo deste artigo de visão geral. Para saber mais sobre a solução que lhe interessa, siga os links fornecidos para obter mais informações.

## <a name="sql-server-import-and-export-wizard"></a>Assistente de Importação e Exportação do SQL Server

Importe dados diretamente de arquivos do Excel percorrendo as páginas do Assistente de importação e exportação do SQL Server. Como opção, salve as configurações de importação/exportação como um pacote SSIS (SQL Server Integration Services) que você pode personalizar e reutilizar.

![Conectar-se a uma fonte de dados do Excel](media/excel-connection.png)

Para obter um exemplo de como usar o assistente para importar do Excel para o SQL Server, veja [Introdução a esse exemplo simples do Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

Se você estiver familiarizado com o SSIS e não quiser executar o Assistente de Importação e Exportação do SQL Server, crie um pacote do SSIS que usa a origem do Excel e o destino do SQL Server no fluxo de dados.

![Componentes no fluxo de dados](media/excel-to-sql-data-flow.png)

Para obter mais informações sobre esses componentes de SSIS, veja os tópicos a seguir:
-   [Origem do Excel](../../integration-services/data-flow/excel-source.md)
-   [Destino do SQL Server](../../integration-services/data-flow/sql-server-destination.md)

Para aprender a compilar pacotes do SSIS, veja o tutorial [Como criar um pacote do ETL](../../integration-services/ssis-how-to-create-an-etl-package.md).

## <a name="openrowset-and-linked-servers"></a>OPENROWSET e servidores vinculados
> [!NOTE]
> O provedor ACE (anteriormente provedor Jet) que se conecta a fontes de dados do Excel é destinado ao uso interativo do lado do cliente. Se você usar o provedor ACE no servidor, especialmente em processos automatizados ou processos em execução em paralelo, você poderá ver resultados inesperados.

### <a name="distributed-queries"></a>Consultas distribuídas

Importe dados diretamente de arquivos do Excel usando a função `OPENROWSET` ou `OPENDATASOURCE` do Transact-SQL. Esse uso é chamado de *consulta distribuída*.

Antes de executar uma consulta distribuída, você precisa habilitar a opção de configuração do servidor `ad hoc distributed queries`, conforme mostra o exemplo a seguir. Para saber mais, confira [Opção de Configuração do Servidor de consultas distribuídas ad hoc](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md).

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

O exemplo de código a seguir usa o `OPENROWSET` para importar os dados da planilha `Data` do Excel para uma nova tabela do banco de dados.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=D:\Desktop\Data.xlsx', [Data$]);
GO
```

Este é o mesmo exemplo com `OPENDATASOURCE`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=D:\Desktop\Data.xlsx;Extended Properties=Excel 12.0')...[Data$];
GO
```

Para *acrescentar* os dados importados a uma tabela *existente* em vez de criar uma nova tabela, use a sintaxe `INSERT INTO ... SELECT ... FROM ...`, em vez da sintaxe `SELECT ... INTO ... FROM ...` usada nos exemplos anteriores.

Para consultar os dados do Excel sem importá-los, basta usar a sintaxe `SELECT ... FROM ...` padrão.

Para obter mais informações sobre consultas distribuídas, veja os tópicos a seguir:
-   [Consultas Distribuídas](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx). (As consultas distribuídas ainda têm suporte no SQL Server 2016, mas a documentação desse recurso não foi atualizada.)
-   [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
-   [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>Servidores vinculados

Você também pode configurar uma conexão persistente para o arquivo do Excel como um *servidor vinculado*. O exemplo a seguir importa os dados da planilha `Data` no servidor vinculado do Excel existente `EXCELLINK` para uma nova tabela de banco de dados denominada `Data_ls`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_ls FROM EXCELLINK...[Data$];
GO
```

Você pode criar um servidor vinculado no SQL Server Management Studio ou executando o procedimento armazenado do sistema `sp_addlinkedserver`, conforme mostra o exemplo a seguir.

```sql
DECLARE @RC int

DECLARE @server     nvarchar(128)
DECLARE @srvproduct nvarchar(128)
DECLARE @provider   nvarchar(128)
DECLARE @datasrc    nvarchar(4000)
DECLARE @location   nvarchar(4000)
DECLARE @provstr    nvarchar(4000)
DECLARE @catalog    nvarchar(128)

-- Set parameter values
SET @server =     'EXCELLINK'
SET @srvproduct = 'Excel'
SET @provider =   'Microsoft.ACE.OLEDB.12.0'
SET @datasrc =    'D:\Desktop\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

Para obter mais informações sobre servidores vinculados, consulte os tópicos a seguir:
-   [Criar servidores vinculados](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
-   [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

Para obter exemplos e informações sobre servidores vinculados e consultas distribuídas, veja os tópicos a seguir:
-   [Como usar o Excel com servidores vinculados e consultas distribuídas do SQL Server](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
-   [Como importar dados do Excel para o SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prerequisite---save-excel-data-as-text"></a>Pré-requisito – salvar os dados do Excel como texto
Para usar o restante dos métodos descritos nesta página, a instrução BULK INSERT, a ferramenta BCP ou o Azure Data Factory – primeiro você precisa exportar os dados do Excel para um arquivo de texto.

No Excel, selecione **Arquivo | Salvar como** e selecione **Texto (Delimitado por tabulação) (\*.txt)** ou **CSV (Delimitado por vírgula) (\*.csv)** como o tipo de arquivo de destino.

> [!TIP]
> Para obter melhores resultados com as ferramentas de importação de dados, salve as planilhas que contêm os cabeçalhos de coluna e as linhas de dados. Se os dados salvos contiverem títulos de página, linhas em branco, observações e assim por diante, você poderá ver resultados inesperados ao importar os dados posteriormente.

## <a name="bulk-insert-command"></a>Comando BULK INSERT

`BULK INSERT` é um comando do Transact-SQL que você pode executar no SQL Server Management Studio. O exemplo a seguir carrega os dados no arquivo delimitado por vírgulas `Data.csv` para uma tabela de banco de dados existente.

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'D:\Desktop\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

Para obter mais informações, veja os tópicos a seguir:
-   [Importar dados em massa usando BULK INSERT ou OPENROWSET(BULK...)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
-   [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp-tool"></a>Ferramenta BCP

O BCP é um programa executado no prompt de comando. O exemplo a seguir carrega os dados no arquivo delimitado por vírgulas `Data.csv` para uma tabela de banco de dados do `Data_bcp` existente.

```sql
bcp.exe ImportFromExcel..Data_bcp in "D:\Desktop\data.csv" -T -c -t ,
```

Para obter mais informações sobre BCP, veja os tópicos a seguir:
-   [Importar e exportar dados em massa usando o utilitário bcp](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
-   [Utilitário bcp](../../tools/bcp-utility.md)
-   [Preparar dados para exportar ou importar em massa](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="copy-wizard-azure-data-factory"></a>Assistente de cópia (Azure Data Factory)
Importe dados salvos como arquivos de texto percorrendo as páginas do Assistente de cópia.

Para obter mais informações sobre o Assistente de cópia, veja os tópicos a seguir:
-   [Assistente de cópia do data factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
-   [Tutorial: Criar um pipeline com Atividade de cópia usando o Assistente de cópia do data factory](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial).

## <a name="azure-data-factory"></a>Azure Data Factory
Se você estiver familiarizado com o Azure Data Factory e não quiser executar o Assistente de cópia, crie um pipeline com uma atividade de cópia que copia do arquivo de texto para o SQL Server ou para o Banco de Dados SQL do Azure.

Para obter mais informações sobre como usar essas fontes e coletores do Data Factory, veja os tópicos a seguir:
-   [Sistema de arquivos](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
-   [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
-   [Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

Para aprender a copiar dados com o Azure Data Factory, veja os tópicos a seguir:
-   [Mover dados usando a Atividade de cópia](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
-   [Tutorial: Criar um pipeline com Atividade de cópia usando o Portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a solução que lhe interessa, siga os links fornecidos para obter mais informações.

