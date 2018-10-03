---
title: Exportar e importar um banco de dados no Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.custom: sql-linux
ms.openlocfilehash: ca8a5f92c3ee4c9ee1e9e45ec7fd23b8a3341835
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742384"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>Exportar e importar um banco de dados no Linux com o SSMS ou SqlPackage.exe no Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo mostra como usar [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) e [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) para exportar e importar um banco de dados do SQL Server no Linux. O SSMS e SqlPackage.exe são aplicativos do Windows, então, usar essa técnica quando você tiver um computador Windows que pode se conectar a uma instância remota do SQL Server no Linux.

Você sempre deve instalar e usar a versão mais recente do SQL Server Management Studio (SSMS), conforme descrito em [usar SSMS no Windows para se conectar ao SQL Server no Linux](sql-server-linux-manage-ssms.md)

> [!NOTE]
> Se você estiver migrando um banco de dados de uma instância do SQL Server para outra, a recomendação é usar [Backup e restauração](sql-server-linux-migrate-restore-database.md).

## <a name="export-a-database-with-ssms"></a>Exportar um banco de dados com o SSMS

1. Inicie o SSMS ao digitar **Microsoft SQL Server Management Studio** caixa de pesquisa no Windows e, em seguida, clique no aplicativo de área de trabalho.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Conecte-se ao seu banco de dados de origem no Pesquisador de objetos. O banco de dados de origem pode ser no Microsoft SQL Server em execução localmente ou na nuvem, no Linux, Windows ou Docker e o banco de dados do Azure SQL ou SQL Data Warehouse do Azure.

3. O banco de dados de origem no Pesquisador de objetos com o botão direito, aponte para **tarefas**e clique em **Exportar aplicativo da camada de dados...**

4. No Assistente de exportação, clique em **próxima**e, em seguida, o **configurações** guia, configure a exportação para salvar o arquivo BACPAC para um local de disco local ou em um blob do Azure.

5. Por padrão, todos os objetos no banco de dados são exportados. Clique o **guia Avançado** e escolha os objetos de banco de dados que você deseja exportar.

6. Clique em **Avançar** e em **Concluir**.

O *. Arquivo BACPAC é criado com êxito no local escolhido e você está pronto para importá-lo para um banco de dados de destino.

## <a name="import-a-database-with-ssms"></a>Importar um banco de dados com o SSMS

1. Inicie o SSMS ao digitar **Microsoft SQL Server Management Studio** caixa de pesquisa no Windows e, em seguida, clique no aplicativo de área de trabalho.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Conecte-se ao servidor de destino no Pesquisador de objetos. O servidor de destino pode ser o Microsoft SQL Server em execução localmente ou na nuvem, no Linux, Windows ou Docker e o banco de dados do Azure SQL ou SQL Data Warehouse do Azure.

3. Clique com botão direito do **bancos de dados** pasta no Pesquisador de objetos e clique **importar aplicativo da camada de dados...**

4. Para criar o banco de dados no seu servidor de destino, especifique um arquivo BACPAC no seu disco local ou selecione a conta de armazenamento do Azure e o contêiner ao qual você carregou o arquivo BACPAC.

5. Forneça o novo nome de banco de dados para o banco de dados. Se você estiver importando um banco de dados no banco de dados SQL, defina a edição do Microsoft Azure SQL Database (camada de serviço), o tamanho máximo do banco de dados e o objetivo de serviço (nível de desempenho).

6. Clique em **próxima** e, em seguida, clique em **concluir** para importar o arquivo BACPAC para um novo banco de dados em seu servidor de destino.

O *. Arquivo BACPAC é importado para criar um novo banco de dados no servidor de destino especificado.

## <a id="sqlpackage"></a> Opção de linha de comando SqlPackage

Também é possível usar a ferramenta de linha de comando do SQL Server Data Tools (SSDT), [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx), para exportar e importar arquivos BACPAC.

O comando de exemplo a seguir exporta um arquivo BACPAC:

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

Use o seguinte comando para importar dados de esquema e de usuário de banco de dados de um. Arquivo BACPAC:

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>Confira também
Para obter mais informações sobre como usar o SSMS, consulte [usar o SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Para obter mais informações sobre SqlPackage.exe, consulte o [documentação de referência do SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx).
