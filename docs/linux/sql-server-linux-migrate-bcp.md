---
title: Dados de cópia em massa para o SQL Server no Linux
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: b611ef63532dd855648354bb85fc96f7cb52bd60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127318"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>Dados de cópia em massa com bcp para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo mostra como usar o [bcp](../tools/bcp-utility.md) utilitário de linha de comando para copiar os dados em massa entre uma instância do SQL Server no Linux e um arquivo de dados em um formato especificado pelo usuário.

Você pode usar `bcp` para importar grandes números de linhas em tabelas do SQL Server ou para exportar dados de tabelas do SQL Server para arquivos de dados. Exceto quando usado com a opção queryout, `bcp` não requer conhecimento de Transact-SQL. O `bcp` utilitário de linha de comando funciona com o Microsoft SQL Server em execução localmente ou na nuvem, no Linux, Windows ou Docker e Azure SQL Database e Azure SQL Data Warehouse.

Este artigo mostra como:
- Importar dados para uma tabela usando o `bcp in` comando
- Exportar dados de uma tabela usando o `bcp out` comando

## <a name="install-the-sql-server-command-line-tools"></a>Instalar as ferramentas de linha de comando do SQL Server

`bcp` faz parte das ferramentas de linha de comando do SQL Server, que não são instaladas automaticamente com o SQL Server no Linux. Se você ainda não instalou as ferramentas de linha de comando do SQL Server no computador Linux, você deve instalá-los. Para obter mais informações sobre como instalar as ferramentas, selecione sua distribuição do Linux na lista a seguir:

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>Importar dados com bcp

Neste tutorial, você cria um banco de dados de exemplo e uma tabela na instância do SQL Server local (**localhost**) e, em seguida, usar `bcp` para carregar na tabela de exemplo de um arquivo de texto no disco.

### <a name="create-a-sample-database-and-table"></a>Criar um banco de dados de exemplo e uma tabela

Vamos começar criando um banco de dados de exemplo com uma tabela simple que é usada no restante deste tutorial.

1. Na caixa de Linux, abra um terminal de comando.

2. Copie e cole os comandos a seguir na janela de terminal. Esses comandos usam o **sqlcmd** utilitário de linha de comando para criar um banco de dados de exemplo (**BcpSampleDB**) e uma tabela (**TestEmployees**) na instância do SQL Server local (**localhost**). Lembre-se de substituir os `username` e `<your_password>` conforme necessário antes de executar os comandos.

Criar o banco de dados **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
Criar a tabela **TestEmployees** no banco de dados **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>Criar o arquivo de dados de origem
Copie e cole o seguinte comando na janela de terminal. Podemos usar interno `cat` comando para criar um arquivo de dados de texto de exemplo com três registros salvá-lo em seu diretório base como **~/test_data.txt**. Os campos em registros são delimitados por uma vírgula.

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

Você pode verificar que o arquivo de dados foi criado corretamente executando o seguinte comando na janela do terminal:
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
Copie e cole os comandos a seguir na janela de terminal. Esse comando usa `bcp` para se conectar à instância do SQL Server local (**localhost**) e importar os dados do arquivo de dados ( **~/test_data.txt**) na tabela (**TestEmployees** ) no banco de dados (**BcpSampleDB**). Lembre-se de substituir o nome de usuário e `<your_password>` conforme necessário antes de executar os comandos.

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

Aqui está uma breve visão geral dos parâmetros de linha de comando, usamos com `bcp` neste exemplo:
- `-S`: Especifica a instância do SQL Server ao qual se conectar
- `-U`: Especifica a ID de logon usada para se conectar ao SQL Server
- `-P`: Especifica a senha para a ID de logon
- `-d`: Especifica o banco de dados para se conectar ao
- `-c`: executa operações usando um tipo de dados de caractere
- `-t`: Especifica o terminador de campo. Estamos usando `comma` como terminador de campo para os registros em nosso arquivo de dados

> [!NOTE]
> Não estamos especificando um terminador de linha personalizado neste exemplo. Linhas no arquivo de dados de texto foram encerradas corretamente com `newline` quando usamos o `cat` comando para criar o arquivo de dados anteriormente.

Você pode verificar que os dados foi importados com êxito, executando o seguinte comando na janela do terminal. Lembre-se de substituir os `username` e `<your_password>` conforme necessário antes de executar o comando.
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

## <a name="export-data-with-bcp"></a>Exportar dados com bcp

Neste tutorial, você usará `bcp` para exportar dados da tabela de exemplo que criamos anteriormente para um novo arquivo de dados.

Copie e cole os comandos a seguir na janela de terminal. Esses comandos usam o `bcp` utilitário de linha de comando para exportar dados da tabela **TestEmployees** no banco de dados **BcpSampleDB** para um novo arquivo de dados chamado **~/test_export.txt** .  Lembre-se de substituir o nome de usuário e `<your_password>` conforme necessário antes de executar o comando.

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

Você pode verificar se os dados foram exportados corretamente executando o seguinte comando na janela do terminal:
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
- [Formatos de dados para compatibilidade usando bcp](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [Importar dados em massa usando BULK INSERT](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [INSERÇÃO em MASSA (Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
