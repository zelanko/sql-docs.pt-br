---
title: Copiar dados em massa para o SQL Server em Linux
description: Este artigo descreve o utilitário bcp. Use bcp para importar grandes números de linhas para tabelas do SQL Server ou para exportar dados de tabelas do SQL Server para arquivos de dados.
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: 447304bf0927b08e76a668e93ca750f3f8bfc779
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896283"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>Copiar dados em massa com bcp para o SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo mostra como usar o utilitário de linha de comando [bcp](../tools/bcp-utility.md) para copiar dados em massa entre uma instância do SQL Server em Linux e um arquivo de dados em um formato especificado pelo usuário.

Você pode usar `bcp` para importar grande número de linhas em tabelas do SQL Server ou para exportar dados de tabelas do SQL Server para arquivos de dados. Exceto quando usado com a opção queryout, `bcp` não requer conhecimento do Transact-SQL. O utilitário de linha de comando `bcp` funciona com o Microsoft SQL Server em execução local ou na nuvem, no Linux, no Windows ou no Docker e no Banco de Dados SQL do Azure e no SQL Data Warehouse do Azure.

Este artigo mostra como:
- importar dados para uma tabela usando o comando `bcp in`
- exportar dados de uma tabela usando o comando `bcp out`

## <a name="install-the-sql-server-command-line-tools"></a>instalar as ferramentas de linha de comando SQL Server

`bcp` faz parte das ferramentas de linha de comando do SQL Server, que não são instaladas automaticamente com o SQL Server em Linux. Se ainda não tiver instalado as ferramentas de linha de comando do SQL Server em seu computador Linux, você deverá instalá-las. Para obter mais informações sobre como instalar as ferramentas, selecione sua distribuição do Linux na lista a seguir:

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>Importar dados com o bcp

Neste tutorial, você cria um banco de dados de exemplo e uma tabela na instância do SQL Server local (**localhost**) e, em seguida, usa `bcp` para carregar na tabela de exemplo de um arquivo de texto em disco.

### <a name="create-a-sample-database-and-table"></a>Criar uma tabela e um banco de dados de exemplo

Vamos começar criando um banco de dados de exemplo com uma tabela simples que é usada no restante deste tutorial.

1. Na caixa do Linux, abra um terminal de comando.

2. Copie e cole os comandos a seguir na janela do terminal. Esses comandos usam o utilitário de linha de comando **sqlcmd** para criar um banco de dados de exemplo (**BcpSampleDB**) e uma tabela (**TestEmployees**) na instância do SQL Server local (**localhost**). Lembre-se de substituir o `username` e o `<your_password>` conforme necessário antes de executar os comandos.

Crie o banco de dados **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
Crie a tabela **TestEmployees** no banco de dados **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>Criar o arquivo de dados de origem
Copie e cole os comandos a seguir na janela do terminal. Usamos o comando interno `cat` para criar um arquivo de dados de texto de exemplo com três registros e salvar o arquivo no diretório base como **~/test_data.txt**. Os campos nos registros são delimitados por uma vírgula.

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

Executando o seguinte comando na janela do terminal, você pode verificar se o arquivo de dados foi criado corretamente:
```bash 
cat ~/test_data.txt
```

Isso deve exibir o seguinte na janela do terminal:
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>Importar dados do arquivo de dados de origem
Copie e cole os comandos a seguir na janela do terminal. Esse comando usa `bcp` para conectar-se à instância do SQL Server local (**localhost**) e importar os dados do arquivo de dados ( **~/test_data.txt**) para a tabela (**TestEmployees**) no banco de dados (**BcpSampleDB**). Lembre-se de substituir o nome de usuário e `<your_password>` conforme necessário antes de executar os comandos.

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

Aqui está uma breve visão geral dos parâmetros de linha de comando que usamos com `bcp` neste exemplo:
- `-S`: especifica a instância do SQL Server à qual você deseja se conectar
- `-U`: especifica a ID de logon usada para conectar-se ao SQL Server
- `-P`: especifica a senha para a ID de logon
- `-d`: especifica o banco de dados ao qual se conectar
- `-c`: executa operações usando um tipo de dados de caractere
- `-t`: especifica o terminador de campo. Estamos usando `comma` como terminador de campo para os registros em nosso arquivo de dados

> [!NOTE]
> Não estamos especificando um terminador de linha personalizado neste exemplo. As linhas no arquivo de dados de texto foram finalizadas corretamente com `newline` quando usamos o comando `cat` para criar o arquivo de dados anteriormente.

Executando o seguinte comando na janela do terminal, você pode verificar se os dados foram importados com êxito. Lembre-se de substituir o `username` e o `<your_password>` conforme necessário antes de executar o comando.
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

Isso deve exibir os seguintes resultados:
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>Exportar dados com o bcp

Neste tutorial, você usará `bcp` para exportar dados da tabela de exemplo que criamos anteriormente para um novo arquivo de dados.

Copie e cole os comandos a seguir na janela do terminal. Esses comandos usam o utilitário de linha de comando `bcp` para exportar dados da tabela **TestEmployees** no banco de dados **BcpSampleDB** para um novo arquivo de dados chamado **~/test_export.txt**.  Lembre-se de substituir o nome de usuário e `<your_password>` conforme necessário antes de executar o comando.

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

Executando o seguinte comando na janela do terminal, você pode verificar se os dados foram exportados corretamente:
```bash 
cat ~/test_export.txt
```

Isso deve exibir o seguinte na janela do terminal:
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>Confira também
- [utilitário bcp](../tools/bcp-utility.md)
- [Formatos de dados para compatibilidade ao usar o bcp](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [Importar dados em massa usando BULK INSERT](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
