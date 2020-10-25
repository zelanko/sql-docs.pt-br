---
title: Bancos de dados de exemplo do AdventureWorks
description: Siga estas instruções para baixar e instalar bancos de dados de exemplo do AdventureWorks para SQL Server usando Transact-SQL (T-SQL), SQL Server Management Studio (SSMS) ou Azure Data Studio.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/16/2020
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 1482104a0c8ffea7f7f2502b83b9b268b7bb08d2
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523941"
---
# <a name="adventureworks-sample-databases"></a>Bancos de dados de exemplo do AdventureWorks
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Este artigo fornece links diretos para baixar bancos de dados de exemplo do AdventureWorks, bem como instruções para restaurá-los para o SQL Server e o Azure SQL Database. 

Para obter mais informações sobre exemplos, consulte o [repositório GitHub de exemplos](https://github.com/microsoft/sql-server-samples/tree/master/samples/databases). 

## <a name="prerequisites"></a>Pré-requisitos

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019) ou [banco de dados SQL do Azure](https://azure.microsoft.com/services/sql-database/)
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) ou [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)


## <a name="download-backup-files"></a>Baixar arquivos de backup 

Use estes links para baixar o banco de dados de exemplo apropriado para seu cenário. 

- Os dados **OLTP** são para a maioria das cargas de trabalho de processamento de transações online típicas. 
- Os dados de **data warehouse (DW)** são para cargas de trabalho de data warehouse. 
- Os dados **leves (lt)** são uma versão leve e mais simples do exemplo de **OLTP** . 

Se você não tiver certeza de que precisa, comece com a versão do OLTP que corresponde à sua versão do SQL Server. 

|**OLTP** |**data warehouse** |**Leve**|
|---------|---------|---------|
|[AdventureWorks2019. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2019.bak)|[AdventureWorksDW2019. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2019.bak)|[AdventureWorksLT2019. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2019.bak)|
|[AdventureWorks2017. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)|[AdventureWorksDW2017. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)|[AdventureWorksLT2017. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2017.bak)|
|[AdventureWorks2016. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)|[AdventureWorksDW2016. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)|[AdventureWorksLT2016. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2016.bak)|
|[AdventureWorks2016_EXT. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016_EXT.bak)|[AdventureWorksDW2016_EXT. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016_EXT.bak)| N/D |
|[AdventureWorks2014. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)|[AdventureWorksDW2014. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)|[AdventureWorksLT2014. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2014.bak)|
|[AdventureWorks2012. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)|[AdventureWorksDW2012. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)|[AdventureWorksLT2012. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2012.bak)|
|[Banco AdventureWorks2008R2. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)| [AdventureWorksDW2008R2. bak](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak) | N/D |

Arquivos adicionais podem ser encontrados diretamente no GitHub: 

- [SQL Server 2014-2019](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL Server 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL Server 2008 e 2008R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)


## <a name="restore-to-sql-server"></a>Restaurar para SQL Server 

Você pode usar o `.bak` arquivo para restaurar seu banco de dados de exemplo para sua instância do SQL Server. Você pode fazer isso usando o comando [Restore (Transact-SQL)](../t-sql/statements/restore-statements-transact-sql.md) ou usando a interface gráfica (GUI) em [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) ou [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md).

# <a name="sql-server-management-studio-ssms"></a>[SQL Server Management Studio (SSMS)](#tab/ssms)

Se você não estiver familiarizado com o uso do SQL Server Management Studio (SSMS), poderá ver [conectar & consulta](../ssms/quickstarts/connect-query-sql-server.md) para começar. 

Para restaurar o banco de dados no SQL Server Management Studio, siga estas etapas:

1. Baixe o `.bak` arquivo apropriado de um dos links fornecidos na seção [baixar arquivos de backup](#download-backup-files) .
2. Mova o `.bak` arquivo para o local de backup SQL Server. Isso varia dependendo do local de instalação, do nome da instância e da versão do SQL Server. Por exemplo, o local padrão para uma instância padrão do SQL Server 2019 é:

   `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup`. 

3. Abra o SQL Server Management Studio (SSMS) e conecte-se ao seu SQL Server no. 
4. Clique com o botão direito do mouse em **bancos** de dados no **pesquisador de objetos**  >  **restaurar banco...** para iniciar o assistente para **restaurar banco de dados** . 

   :::image type="content" source="media/adventureworks-install-configure/restore-db-ssms.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::


1. Selecione **dispositivo** e, em seguida, selecione as reticências **(...)** para escolher um dispositivo. 
1. Selecione **Adicionar** e, em seguida, escolha o `.bak` arquivo que você moveu recentemente para esse local. Se você moveu o arquivo para esse local, mas não é possível vê-lo no assistente, isso normalmente indica um problema de permissões-SQL Server ou o usuário conectado ao SQL Server não tem permissão para esse arquivo nesta pasta. 
1. Selecione **OK** para confirmar a seleção de backup do banco de dados e feche a janela **selecionar dispositivos de backup** . 
1. Verifique a guia **arquivos** para confirmar a **restauração como** local e os nomes de arquivo correspondem ao local e aos nomes de arquivo pretendidos no Assistente para **restaurar banco de dados** . 
1. Selecione **OK** para restaurar o banco de dados. 

   :::image type="content" source="media/adventureworks-install-configure/restore-db-wizard-ssms.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::

Para obter mais informações sobre como restaurar um banco de dados SQL Server, consulte [restaurar um backup de banco de dados usando o SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).

# <a name="transact-sql-t-sql"></a>[Transact-SQL (T-SQL)](#tab/tsql)

Você pode restaurar seu banco de dados de exemplo usando Transact-SQL (T-SQL). Um exemplo para restaurar o AdventureWorks2019 é fornecido abaixo, mas o nome do banco de dados e o caminho do arquivo de instalação podem variar dependendo do seu ambiente. 

Para restaurar o AdventureWorks2019, modifique os valores conforme apropriado para o seu ambiente e execute o seguinte comando Transact-SQL (T-SQL):

```sql
USE [master]
RESTORE DATABASE [AdventureWorks2019] 
FROM  DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\AdventureWorks2019.bak' 
WITH  FILE = 1,  NOUNLOAD,  STATS = 5
GO

```

# <a name="azure-data-studio"></a>[Azure Data Studio](#tab/data-studio)

Se você não estiver familiarizado com o [Azure Data Studio Studio](../azure-data-studio/download-azure-data-studio.md), poderá ver [conectar & consulta](../azure-data-studio/quickstart-sql-server.md) para começar

Para restaurar o banco de dados no Azure Data Studio, siga estas etapas:

1. Baixe o `.bak` arquivo apropriado de um dos links fornecidos na seção [baixar arquivos de backup](#download-backup-files) .
1. Mova o `.bak` arquivo para o local de backup SQL Server. Isso varia dependendo do local de instalação, do nome da instância e da versão do SQL Server. Por exemplo, o local padrão para uma instância padrão do SQL Server 2019 é:

    `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup`.

1. Abra o Azure Data Studio Studio e conecte-se à sua instância do SQL Server.
1. Clique com o botão direito do mouse no servidor e selecione **gerenciar**.

   :::image type="content" source="media/adventureworks-install-configure/ads-manage.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::

1. Selecione **restaurar**

   :::image type="content" source="media/adventureworks-install-configure/ads-restore-database.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::

1. Na guia **geral** , preencha os valores listados em **origem**.
    1. Em **restaurar de**, selecione *arquivo de backup*.
    1. Em **caminho do arquivo de backup**, selecione o local em que você armazenou o arquivo. bak. 
    
   :::image type="content" source="media/adventureworks-install-configure/ads-source.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::
    
    Isso preenche automaticamente o restante dos campos, como **banco**de dados, **banco de dados de destino** e **restaurar para**o. 

   :::image type="content" source="media/adventureworks-install-configure/ads-destination-restore-plan.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::

1. Selecione **restaurar** para restaurar o banco de dados. 

   :::image type="content" source="media/adventureworks-install-configure/ads-restore.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::

---

## <a name="deploy-to-azure-sql-database"></a>Implantar no banco de dados SQL do Azure

Você tem duas opções para exibir os dados de exemplo do Azure SQL Database. Você pode usar um exemplo ao criar um novo banco de dados ou pode implantar um banco de dados do SQL Server diretamente no Azure usando SQL Server Management Studio (SSMS).

Para obter dados de exemplo para o SQL do Azure Instância Gerenciada em vez disso, consulte [restaurar importadores mundiais para sql instância gerenciada](/azure/azure-sql/managed-instance/restore-sample-database-quickstart). 

### <a name="deploy-new-sample-database"></a>Implantar novo banco de dados de exemplo

Ao criar um novo banco de dados no banco de dados SQL do Azure, você tem a opção de criar um banco de dados em branco ou um banco de dados de exemplo. 

Siga estas etapas para usar um banco de dados de exemplo para criar um novo banco de dados: 

1. Conecte-se ao seu portal do Azure.
1. Selecione **criar um recurso** na parte superior esquerda do painel de navegação. 
1. Selecione **bancos** de dados e, em seguida, selecione **banco de dados SQL**. 
1. Preencha as informações solicitadas para criar seu banco de dados. 
1. Na guia **configurações adicionais** , escolha **exemplo** como os dados existentes em **fonte de dados**: 

   :::image type="content" source="media/adventureworks-install-configure/deploy-sample-to-azure.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::

1. Selecione **criar** para criar seu novo banco de dados SQL, que é a cópia restaurada do banco de dados AdventureWorksLT. 


### <a name="deploy-database-from-sql-server"></a>Implantar banco de dados de SQL Server

SQL Server Management Studio fornece a capacidade de implantar um banco de dados diretamente no banco de dados SQL do Azure. Esse método atualmente não fornece validação de dados, portanto, destina-se a desenvolvimento e teste e não deve ser usado para produção. 

Para implantar um banco de dados de exemplo do SQL Server para o banco de dados SQL do Azure, siga estas etapas:

1. Conecte-se ao seu SQL Server no SQL Server Management Studio. 
1. Se você ainda não tiver feito isso, [restaure o banco de dados de exemplo para SQL Server](#restore-to-sql-server). 
1. Clique com o botão direito do mouse no banco de dados restaurado em tarefas do **pesquisador de objetos**  >  **Tasks**  >  **implantar banco de dados no banco de dados SQL do Microsoft Azure.** 

   :::image type="content" source="media/adventureworks-install-configure/deploy-db-to-azure.png" alt-text="Captura de tela mostrando como optar por restaurar o banco de dados clicando com o botão direito do mouse no Pesquisador de objetos e selecionando restaurar banco de dados.":::

1. Siga o assistente para se conectar ao banco de dados SQL do Azure e implantar seu banco de dados. 


## <a name="creation-scripts"></a>Scripts de criação

Em vez de restaurar um banco de dados, como alternativa, você pode usar scripts para criar os bancos de dados AdventureWorks, independentemente da versão. 

Os scripts abaixo podem ser usados para criar todo o banco de dados AdventureWorks: 

- [Zip de scripts do OLTP AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [Zip de scripts de DW do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

Informações adicionais sobre como usar os scripts podem ser encontradas no [GitHub](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). 

## <a name="next-steps"></a>Próximas etapas

Depois de restaurar o banco de dados de exemplo, usando os seguintes tutoriais para começar a usar o SQL Server: 


[Tutoriais para o mecanismo de banco de dados SQL Server](../relational-databases/database-engine-tutorials.md)   
[Conectar e consultar com SQL Server Management Studio (SSMS)](../ssms/quickstarts/connect-query-sql-server.md)   
[Conectar e consultar com Azure Data Studio](../ssms/quickstarts/connect-query-sql-server.md)