---
title: Importar dados do Excel para o SQL | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 09/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77572a417836683e10ba3c7736fe4cdd0db4e129
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708148"
---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>Importar dados do Excel para o SQL Server ou Banco de Dados SQL do Azure

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Há várias maneiras de importar dados de arquivos do Excel para o SQL Server ou para o Banco de Dados SQL do Azure. Alguns métodos permitem que você importe dados em uma única etapa diretamente de arquivos do Excel; outros métodos exigem que você exporte os dados do Excel como texto (arquivo CSV) antes de importá-los. Este artigo resume os métodos usados com frequência e fornece links para informações mais detalhadas.

## <a name="list-of-methods"></a>Lista de métodos

É possível usar as seguintes ferramentas para importar dados do Excel:

| Exportar para texto primeiro (SQL Server e Banco de Dados SQL) | Diretamente do Excel (somente SQL Server local) |
| :------------------------------------------------- |:------------------------------------------------- |
| [Assistente de Importação de Arquivo Simples](#import-wiz)             |[Assistente de Importação e Exportação do SQL Server](#wiz)        |
| Instrução [BULK INSERT](#bulk-insert)              |[SQL Server Integration Services (SSIS)](#ssis)    |
| [BCP](#bcp)                                        |Função [OPENROWSET](#openrowset) <br>            |
| [Assistente de Cópia (Azure Data Factory)](#adf-wiz)       |                                                   |
| [Azure Data Factory](#adf)                         |                                                   |
| &nbsp; | &nbsp; |

Se você quiser importar várias planilhas de uma pasta de trabalho do Excel, normalmente precisará executar cada uma dessas ferramentas uma vez para cada planilha.

Uma descrição completa das ferramentas e serviços complexos, como SSIS ou Azure Data Factory, está além do escopo desta lista. Para saber mais sobre a solução que lhe interessa, siga os links fornecidos.

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../../integration-services/load-data-to-from-excel-with-ssis.md).

Se você não tem o SQL Server instalado, ou se tem o SQL Server, mas não tem o SQL Server Management Studio instalado, consulte [Baixar o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md).

## <a name="wiz"></a> Assistente de Importação e Exportação do SQL Server

Importe dados diretamente de arquivos do Excel percorrendo as páginas do Assistente de importação e exportação do SQL Server. Como opção, salve as configurações como um pacote SSIS (SQL Server Integration Services) que você pode personalizar e reutilizar mais tarde.

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)].

2. Expanda os **Bancos de dados**.
3. Clique com o botão direito do mouse em um banco de dados.
4. Aponte para **Tarefas**.
5. Clique em uma das opções a seguir.

  - **Importar dados**
  - **Exportar dados**

    ![Inicie o Assistente SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg)

![Conectar-se a uma fonte de dados do Excel](media/excel-connection.png)

Para obter um exemplo de como usar o assistente para importar do Excel para o SQL Server, veja [Introdução a esse exemplo simples do Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

Para saber outras formas de iniciar o assistente de Importação e Exportação, confira [Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

## <a name="ssis"></a> SQL Server Integration Services (SSIS)

Se você estiver familiarizado com o SSIS e não quiser executar o Assistente de Importação e Exportação do SQL Server, crie um pacote do SSIS que usa a origem do Excel e o destino do SQL Server no fluxo de dados.

Para obter mais informações sobre esses componentes de SSIS, veja os tópicos a seguir:

- [Origem do Excel](../../integration-services/data-flow/excel-source.md)
- [Destino do SQL Server](../../integration-services/data-flow/sql-server-destination.md)

Para aprender a compilar pacotes do SSIS, veja o tutorial [Como criar um pacote do ETL](../../integration-services/ssis-how-to-create-an-etl-package.md).

![Componentes no fluxo de dados](media/excel-to-sql-data-flow.png)

## <a name="openrowset"></a> OPENROWSET e servidores vinculados

> [!IMPORTANT]
> No Banco de Dados SQL do Azure, não é possível fazer uma importação diretamente no Excel. Primeiro, é necessário exportar os dados para um arquivo de texto (CSV). Para obter exemplos, confira [Exemplo](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

> [!NOTE]
> O provedor ACE (anteriormente provedor Jet) que se conecta a fontes de dados do Excel é destinado ao uso interativo do lado do cliente. Se você usar o provedor ACE no SQL Server, especialmente em processos automatizados ou processos em execução em paralelo, poderá ver resultados inesperados.

### <a name="distributed-queries"></a>Consultas distribuídas

Importe dados diretamente para o SQL Server de arquivos do Excel usando a função `OPENROWSET` ou `OPENDATASOURCE` do Transact-SQL. Esse uso é chamado de *consulta distribuída*.

> [!IMPORTANT]
> No Banco de Dados SQL do Azure, não é possível fazer uma importação diretamente no Excel. Primeiro, é necessário exportar os dados para um arquivo de texto (CSV). Para obter exemplos, confira [Exemplo](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

Antes de executar uma consulta distribuída, você precisa habilitar a opção de configuração do servidor `ad hoc distributed queries`, conforme mostra o exemplo a seguir. Para saber mais, confira [Opção de Configuração do Servidor de consultas distribuídas ad hoc](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md).

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

O exemplo de código a seguir usa o `OPENROWSET` para importar os dados da planilha `Sheet1` do Excel para uma nova tabela do banco de dados.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=C:\Temp\Data.xlsx', [Sheet1$]);
GO
```

Este é o mesmo exemplo com `OPENDATASOURCE`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=C:\Temp\Data.xlsx;Extended Properties=Excel 12.0')...[Sheet1$];
GO
```

Para *acrescentar* os dados importados a uma tabela *existente* em vez de criar uma nova tabela, use a sintaxe `INSERT INTO ... SELECT ... FROM ...`, em vez da sintaxe `SELECT ... INTO ... FROM ...` usada nos exemplos anteriores.

Para consultar os dados do Excel sem importá-los, basta usar a sintaxe `SELECT ... FROM ...` padrão.

Para obter mais informações sobre consultas distribuídas, veja os tópicos a seguir:

- [Consultas Distribuídas](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx) (As consultas distribuídas ainda são compatíveis com o SQL Server 2016, mas a documentação desse recurso não foi atualizada.)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
- [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>Servidores vinculados

Configure também uma conexão persistente do SQL Server com o arquivo do Excel como um *servidor vinculado*. O exemplo a seguir importa os dados da planilha `Data` no servidor vinculado existente `EXCELLINK` do Excel para uma nova tabela de banco de dados do SQL Server chamada `Data_ls`.

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
SET @datasrc =    'C:\Temp\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

Para obter mais informações sobre servidores vinculados, consulte os tópicos a seguir:

- [Criar servidores vinculados](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
- [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

Para obter exemplos e informações sobre servidores vinculados e consultas distribuídas, veja os tópicos a seguir:

- [Como usar o Excel com servidores vinculados e consultas distribuídas do SQL Server](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
- [Como importar dados do Excel para o SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prereq"></a> Pré-requisito – salvar os dados do Excel como texto

Para usar o restante dos métodos descritos nesta página, a instrução BULK INSERT, a ferramenta BCP ou o Azure Data Factory – primeiro você precisa exportar os dados do Excel para um arquivo de texto.

No Excel, clique em **Arquivo | Salvar como** e **Texto (Delimitado por tabulação) (\*.txt)** ou **CSV (Delimitado por vírgula) (\*.csv)** como o tipo de arquivo de destino.

Se você quiser exportar várias planilhas da pasta de trabalho, selecione cada uma e repita este procedimento. O comando **Salvar como** exporta apenas a planilha ativa.

> [!TIP]
> Para obter melhores resultados com as ferramentas de importação de dados, salve as planilhas que contêm os cabeçalhos de coluna e as linhas de dados. Se os dados salvos contiverem títulos de página, linhas em branco, observações e assim por diante, você poderá ver resultados inesperados ao importar os dados posteriormente.

## <a name="import-wiz"></a> O Assistente Importar Arquivo Simples

Importe dados salvos como arquivos de texto percorrendo as páginas do Assistente Importar Arquivo Simples.

Conforme descrito anteriormente na seção[Pré-requisito](#prereq), você precisa exportar os dados do Excel como texto antes de usar o Assistente de Importação de Arquivo Simples para importá-los.

Para saber mais sobre o Assistente Importar Arquivo Simples, confira [Importação de arquivo simples para o Assistente do SQL](import-flat-file-wizard.md).

## <a name="bulk-insert"></a> Comando BULK INSERT

`BULK INSERT` é um comando do Transact-SQL que você pode executar no SQL Server Management Studio. O exemplo a seguir carrega os dados no arquivo delimitado por vírgulas `Data.csv` para uma tabela de banco de dados existente.

Conforme descrito anteriormente na seção [Pré-requisito](#prereq), você deve exportar os dados do Excel como texto antes que possa usar BULK INSERT para importá-lo. BULK INSERT não pode ler diretamente arquivos do Excel. Com o comando BULK INSERT, você pode importar um arquivo CSV armazenado localmente ou no Armazenamento de Blobs do Azure.

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'C:\Temp\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

Para obter mais informações e exemplos do SQL Server e do Banco de Dados SQL, confira os seguintes tópicos:

- [Importar dados em massa usando BULK INSERT ou OPENROWSET(BULK...)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp"></a> Ferramenta BCP

O BCP é um programa executado no prompt de comando. O exemplo a seguir carrega os dados no arquivo delimitado por vírgulas `Data.csv` para uma tabela de banco de dados do `Data_bcp` existente.

Conforme descrito anteriormente na seção [Pré-requisito](#prereq), você deve exportar os dados do Excel como texto antes que possa usar o BCP para importá-lo. BCP não pode ler diretamente arquivos de Excel. Use-o para fazer uma importação para o SQL Server ou o Banco de Dados SQL de um arquivo de teste (CSV) salvo no armazenamento local.

> [!IMPORTANT]
> Para um arquivo de texto (CSV) armazenado no Armazenamento de Blobs do Azure, use BULK INSERT ou OPENROWSET. Para obter um exemplo, confira [Exemplo](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

```console
bcp.exe ImportFromExcel..Data_bcp in "C:\Temp\data.csv" -T -c -t ,
```

Para obter mais informações sobre BCP, veja os tópicos a seguir:

- [Importar e exportar dados em massa usando o utilitário bcp](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
- [Utilitário bcp](../../tools/bcp-utility.md)
- [Preparar dados para exportar ou importar em massa](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="adf-wiz"></a> Assistente de cópia (Azure Data Factory)

Importe dados salvos como arquivos de texto percorrendo as páginas do Assistente de Cópia do Azure Data Factory.

Conforme descrito anteriormente na seção [Pré-requisito](#prereq), você deve exportar os dados do Excel como texto antes que possa usar o Azure Data Factory para importá-lo. O Data Factory não pode ler arquivos do Excel diretamente.

Para obter mais informações sobre o Assistente de cópia, veja os tópicos a seguir:

- [Assistente de cópia do data factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
- [Tutorial: Criar um pipeline com Atividade de cópia usando o Assistente de cópia do Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial).

## <a name="adf"></a> Azure Data Factory

Se você estiver familiarizado com o Azure Data Factory e não quiser executar o Assistente de cópia, crie um pipeline com uma atividade de cópia que copia do arquivo de texto para o SQL Server ou para o Banco de Dados SQL do Azure.

Conforme descrito anteriormente na seção [Pré-requisito](#prereq), você deve exportar os dados do Excel como texto antes que possa usar o Azure Data Factory para importá-lo. O Data Factory não pode ler arquivos do Excel diretamente.

Para obter mais informações sobre como usar essas fontes e coletores do Data Factory, veja os tópicos a seguir:

- [Sistema de arquivos](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
- [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
- [Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

Para aprender a copiar dados com o Azure Data Factory, veja os tópicos a seguir:

- [Mover dados usando a Atividade de cópia](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
- [Tutorial: Criar um pipeline com Atividade de cópia usando o portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="common-errors"></a>Erros comuns

### <a name="microsoftaceoledb120-has-not-been-registered"></a>O Microsoft.ACE.OLEDB.12.0" não foi registrado

Esse erro ocorre porque o provedor OLEDB não está instalado. Instale-o com os [Pacotes Redistribuíveis do Mecanismo de Banco de Dados do Microsoft Access 2010](https://www.microsoft.com/en-us/download/details.aspx?id=13255). Instale a versão de 64 bits se o Windows e o SQL Server tiverem 64 bits.

O erro completo é:

```
Msg 7403, Level 16, State 1, Line 3
The OLE DB provider "Microsoft.ACE.OLEDB.12.0" has not been registered.
```

## <a name="cannot-create-an-instance-of-ole-db-provider-microsoftaceoledb120-for-linked-server-null"></a>Não é possível criar uma instância do provedor OLE DB "Microsoft.ACE.OLEDB.12.0" para o servidor vinculado "(null)"

Isso indica que o OLEDB da Microsoft não foi configurado corretamente. Execute o seguinte código Transact-SQL para solucionar:

```sql
EXEC sp_MSset_oledb_prop N'Microsoft.ACE.OLEDB.12.0', N'AllowInProcess', 1
EXEC sp_MSset_oledb_prop N'Microsoft.ACE.OLEDB.12.0', N'DynamicParameters', 1
```

O erro completo é:

```
Msg 7302, Level 16, State 1, Line 3
Cannot create an instance of OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)".
```

### <a name="the-32-bit-ole-db-provider-microsoftaceoledb120-cannot-be-loaded-in-process-on-a-64-bit-sql-server"></a>O provedor OLE DB de 32 bits "Microsoft.ACE.OLEDB.12.0" não pode ser carregado em processo em um SQL Server de 64 bits

Isso ocorre quando uma versão de 32 bits do provedor OLE DB está instalada com um SQL Server de 64 bits. Para solucionar esse problema, desinstale a versão de 32 bits e instale a versão de 64 bits do provedor OLE DB.

O erro completo é:

```
Msg 7438, Level 16, State 1, Line 3
The 32-bit OLE DB provider "Microsoft.ACE.OLEDB.12.0" cannot be loaded in-process on a 64-bit SQL Server.
```

### <a name="the-ole-db-provider-microsoftaceoledb120-for-linked-server-null-reported-an-error-the-provider-did-not-give-any-information-about-the-error"></a>O provedor OLE DB "Microsoft.ACE.OLEDB.12.0" para o servidor vinculado "(null)" relatou um erro. O provedor não forneceu nenhuma informação sobre o erro

### <a name="cannot-initialize-the-data-source-object-of-ole-db-provider-microsoftaceoledb120-for-linked-server-null"></a>Não é possível inicializar o objeto de fonte de dados do provedor OLE DB "Microsoft.ACE.OLEDB.12.0" para o servidor vinculado "(null)"

Ambos esses erros normalmente indicam um problema de permissões entre o processo do SQL Server e o arquivo. Verifique se a conta em execução no serviço SQL Server tem permissão de acesso completo ao arquivo. Não é recomendável tentar importar arquivos da área de trabalho.

Os erros completos são:

```
Msg 7399, Level 16, State 1, Line 3
The OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)" reported an error. The provider did not give any information about the error.
```

```
Msg 7303, Level 16, State 1, Line 3
Cannot initialize the data source object of OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)".
```

## <a name="see-also"></a>Consulte Também

[Importar dados do Excel ou exportar dados para o Excel com o SSIS (SQL Server Integration Services)](../../integration-services/load-data-to-from-excel-with-ssis.md)
