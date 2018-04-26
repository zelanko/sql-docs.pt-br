---
title: Copiar dados para o SQL Server no Linux em massa | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/30/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.workload: On Demand
ms.openlocfilehash: b5e7b92730582e7657e1ba6be7bbcaeda01dc18f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>Dados de cópia em massa com bcp para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo mostra como usar o [bcp](../tools/bcp-utility.md) utilitário de linha de comando para dados de cópia em massa entre uma instância do SQL Server 2017 no Linux e um arquivo de dados em um formato especificado pelo usuário.

Você pode usar `bcp` para importar grande número de linhas em tabelas do SQL Server ou para exportar dados de tabelas do SQL Server para arquivos de dados. Exceto quando usado com a opção queryout `bcp` não requer conhecimento de Transact-SQL. O `bcp` utilitário de linha de comando funciona com o Microsoft SQL Server em execução no local ou na nuvem, no Linux, Windows ou Docker e banco de dados do SQL Azure e Azure SQL Data Warehouse.

Este artigo mostra como para:
- Importar dados em uma tabela usando o `bcp in` comando
- Exportar dados de uma tabela usando o `bcp out` comando

## <a name="install-the-sql-server-command-line-tools"></a>Instalar as ferramentas de linha de comando do SQL Server

`bcp` faz parte das ferramentas de linha de comando do SQL Server, que não são instaladas automaticamente com o SQL Server no Linux. Se já não tiver instalado as ferramentas de linha de comando do SQL Server no computador Linux, você deve instalá-los. Para obter mais informações sobre como instalar as ferramentas, selecione a distribuição de Linux da lista a seguir:

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>Importar dados com bcp

Neste tutorial, você criará um banco de dados de exemplo e uma tabela na instância local do SQL Server (**localhost**) e, em seguida, usar `bcp` para carregar na tabela de exemplo de um arquivo de texto no disco.

### <a name="create-a-sample-database-and-table"></a>Criar um banco de dados de exemplo e uma tabela

Vamos começar criando um banco de dados de exemplo com uma tabela simple que é usada no restante deste tutorial.

1. Na caixa do Linux, abra um terminal de comando.

2. Copie e cole os comandos a seguir na janela de terminal. Esses comandos usam o **sqlcmd** o utilitário de linha de comando para criar um banco de dados de exemplo (**BcpSampleDB**) e uma tabela (**TestEmployees**) na instância local do SQL Server (**localhost**). Lembre-se de substituir o `username` e `<your_password>` conforme necessário antes de executar os comandos.

Criar o banco de dados **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
Criar a tabela **TestEmployees** no banco de dados **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>Criar o arquivo de dados de origem
Copie e cole o seguinte comando na janela do terminal. Usamos o interno `cat` comando para criar um arquivo de dados de texto de exemplo com três registros salvá-lo em seu diretório base como **~/test_data.txt**. Os campos nos registros são delimitados por uma vírgula.

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

Você pode verificar que o arquivo de dados foi criado corretamente executando o comando a seguir na janela de terminal:
```bash 
cat ~/test_data.txt
```

Isso deve exibir o seguinte na janela de terminal:
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>Importar dados do arquivo de dados de origem
Copie e cole os comandos a seguir na janela de terminal. Esse comando usa `bcp` para conectar-se à instância local do SQL Server (**localhost**) e importar os dados do arquivo de dados (**~/test_data.txt**) na tabela (**TestEmployees**) no banco de dados (**BcpSampleDB**). Lembre-se de substituir o nome de usuário e `<your_password>` conforme necessário antes de executar os comandos.

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

Aqui está uma breve visão geral dos parâmetros de linha de comando usados com `bcp` neste exemplo:
- `-S`: Especifica a instância do SQL Server ao qual se conectar
- `-U`: Especifica a ID de logon usada para se conectar ao SQL Server
- `-P`: Especifica a senha para a ID de logon
- `-d`: Especifica o banco de dados para se conectar ao
- `-c`: executa operações usando um tipo de dados de caractere
- `-t`: Especifica o terminador de campo. Estamos usando `comma` como terminador de campo para os registros em nosso arquivo de dados

> [!NOTE]
> Nós não especificar um terminador de linha personalizado neste exemplo. Linhas no arquivo de dados de texto corretamente encerradas com `newline` quando usamos o `cat` comando para criar o arquivo de dados anterior.

Você pode verificar que os dados foram importados com êxito, executando o comando a seguir na janela de terminal. Lembre-se de substituir o `username` e `<your_password>` conforme necessário antes de executar o comando.
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

Neste tutorial, você deve usar `bcp` para exportar dados da tabela de exemplo criado anteriormente para um novo arquivo de dados.

Copie e cole os comandos followikng na janela de terminal. Esses comandos usam o `bcp` o utilitário de linha de comando para exportar dados da tabela **TestEmployees** no banco de dados **BcpSampleDB** para um novo arquivo de dados chamado **~/test_export.txt** .  Lembre-se de substituir o nome de usuário e `<your_password>` conforme necessário antes de executar o comando.

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

Você pode verificar se os dados foram exportados corretamente executando o comando a seguir na janela de terminal:
```bash 
cat ~/test_export.txt
```

Isso deve exibir o seguinte na janela de terminal:
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>Consulte também
- [utilitário bcp](../tools/bcp-utility.md)
- [Formatos de dados para compatibilidade usando bcp](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [Importação em massa dados usando BULK INSERT](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [INSERÇÃO em MASSA (Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
