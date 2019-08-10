---
title: Exportar e importar um banco de dados no Linux
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.openlocfilehash: f99ff799ec91ea455cc37bd994c8555330a8ff0f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68105547"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>Exportar e importar um banco de dados no Linux com SSMS ou SqlPackage.exe no Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo mostra como usar o [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) e o [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) para exportar e importar um banco de dados no SQL Server em Linux. O SSMS e o SqlPackage.exe são aplicativos do Windows, portanto, use essa técnica quando você tiver um computador Windows que possa se conectar a uma Instância remota do SQL Server no Linux.

Você deve sempre instalar e usar a versão mais recente do SSMS (SQL Server Management Studio), conforme descrito em [usar o SSMS no Windows para se conectar ao SQL Server em Linux](sql-server-linux-manage-ssms.md)

> [!NOTE]
> Se você estiver migrando um banco de dados de uma instância SQL Server para outra, a recomendação será usar [Backup e restauração](sql-server-linux-migrate-restore-database.md).

## <a name="export-a-database-with-ssms"></a>Exportar um banco de dados com o SSMS

1. Inicie o SSMS digitando **Microsoft SQL Server Management Studio** na caixa de pesquisa do Windows e, em seguida, clique no aplicativo da área de trabalho.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Conecte-se ao banco de dados de origem no Pesquisador de Objetos. O banco de dados de origem pode estar no Microsoft SQL Server em execução local ou na nuvem, no Linux, no Windows ou no Docker e no Banco de Dados SQL do Azure ou no SQL Data Warehouse do Azure.

3. Clique com o botão direito do mouse no banco de dados de origem no Pesquisador de Objetos, aponte para **Tarefas** e clique em **Exportar Aplicativo da Camada de Dados...**

4. No assistente de exportação, clique em **Avançar** e, na guia **Configurações**, configure a exportação para salvar o arquivo BACPAC em uma localização de disco local ou em um blob do Azure.

5. Por padrão, todos os objetos no banco de dados são exportados. Clique na **guia Avançado** e escolha os objetos de banco de dados que você deseja exportar.

6. Clique em **Avançar** e em **Concluir**.

O arquivo *.BACPAC foi criado com êxito na localização escolhida e você está pronto para importá-lo em um banco de dados de destino.

## <a name="import-a-database-with-ssms"></a>Importar um banco de dados com o SSMS

1. Inicie o SSMS digitando **Microsoft SQL Server Management Studio** na caixa de pesquisa do Windows e, em seguida, clique no aplicativo da área de trabalho.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Conecte-se ao servidor de destino no Pesquisador de Objetos. O servidor de destino pode estar no Microsoft SQL Server em execução local ou na nuvem, no Linux, no Windows ou no Docker e no Banco de Dados SQL do Azure ou no SQL Data Warehouse do Azure.

3. Clique com o botão direito do mouse na pasta **Bancos de dados** no Pesquisador de Objetos e clique em **Importar Aplicativo da Camada de Dados...**

4. Para criar o banco de dados no servidor de destino, especifique um arquivo BACPAC do seu disco local ou selecione a conta de Armazenamento do Azure e o contêiner no qual você carregou o arquivo BACPAC.

5. Forneça o nome do novo banco de dados para o banco de dados. Se você estiver importando um banco de dados no Banco de Dados SQL do Azure, defina a edição do Banco de Dados SQL do Microsoft Azure (camada de serviço), o Tamanho máximo do banco de dados e o Objetivo de Serviço (nível de desempenho).

6. Clique em **Avançar** e em seguida **Concluir** para importar o arquivo BACPAC para um novo banco de dados no servidor de destino.

O arquivo *.BACPAC é importado para criar um banco de dados no servidor de destino que você especificou.

## <a id="sqlpackage"></a> Opção de linha de comando SqlPackage

Também é possível usar a ferramenta de linha de comando SSDT (SQL Server Data Tools), [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx), para exportar e importar arquivos BACPAC.

O comando de exemplo a seguir exporta um arquivo BACPAC:

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

Use o comando a seguir para importar o esquema de banco de dados e os dados de usuário de um arquivo .BACPAC:

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>Confira também
Para obter mais informações sobre como usar o SSMS, confira [Usar o SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Para obter mais informações sobre o SqlPackage.exe, confira a [documentação de referência do SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx).
