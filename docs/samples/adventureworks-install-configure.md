---
title: Instalar & configurar o banco de dados de exemplo AdventureWorks
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 0d9f6842ebe5e7d6ee923eef17f491f0cb7ef6ec
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056738"
---
# <a name="adventureworks-installation-and-configuration"></a>Instalação e configuração do AdventureWorks
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Links de download do AdventureWorks e instruções de instalação. 

## <a name="prerequisites"></a>Prerequisites

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) ou [banco de dados SQL do Azure](https://azure.microsoft.com/services/sql-database/). Para obter a versão completa do exemplo, use Avaliação do SQL Server/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.
 
## <a name="github-links"></a>Links do github

- [Todos os arquivos AdventureWorks para SQL 2014-2016](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [Todos os arquivos AdventureWorks do SQL 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [Todos os arquivos AdventureWorks para SQL 2008 e 2008R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>Downloads de OLTP

Links diretos para as versões de OLTP do AdventureWorks podem ser encontrados abaixo:

- [AdventureWorks2017. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014. bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>Downloads de data warehouse

Links diretos para as versões data warehouse do AdventureWorks podem ser encontrados abaixo:

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>Scripts de criação
Os scripts abaixo podem ser usados para criar todo o banco de dados AdventureWorks, independentemente da versão. 

- [Zip de scripts do OLTP AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [Zip de scripts de DW do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>Instalar no SQL Server

### <a name="restore-backup"></a>Restaurar backup
Siga as etapas abaixo para restaurar um backup de seu banco de dados usando SQL Server Management Studio. 

1. Abra SQL Server Management Studio e conecte-se à instância de SQL Server de destino.
2. Clique com o botão direito do mouse no nó **bancos** de dados e selecione **Restore Database**.
3. Selecione **dispositivo** e clique nas reticências ( **...** )
4. Na caixa de diálogo **selecionar dispositivos de backup**, clique em **Adicionar**, navegue até o backup do banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino dos arquivos de dados e de log no painel **arquivos** . Observe que é uma prática recomendada posicionar arquivos de dados e de log em unidades diferentes.
6. Clique em **OK**. Isso iniciará a restauração do banco de dados. Após a conclusão, você terá o banco de dados AdventureWorks instalado em sua instância de SQL Server.

Para obter mais informações sobre como restaurar um banco de dados SQL Server, consulte [restaurar um backup de banco de dados usando o SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).


### <a name="attach-a-datafile"></a>Anexar um DataFile
Siga as etapas abaixo para anexar o arquivo de dados ao seu banco usando SQL Server Management Studio.

1. Abra SQL Server Management Studio e conecte-se à instância de SQL Server de destino.
2. Clique com o botão direito do mouse no nó **bancos de dados** e selecione **anexar**.
3. Selecione **Adicionar** e navegue até o. Arquivo MDF que você deseja anexar. 
1. Selecione o arquivo e clique em **OK**. 
    1. O banco de dados selecionado deve ser exibido na janela inferior. Se o arquivo estiver listado como "não encontrado", selecione as reticências ( **...** ) ao lado do nome do arquivo e atualize o caminho para o caminho correto. 
    1. Se você tiver apenas o arquivo de dados (. MDF), e não o arquivo de log (. ldf), realce o. ldf na janela inferior e selecione **remover**. Isso criará um novo arquivo de log. 
1. Selecione **OK** para anexar o arquivo. Depois que o arquivo for anexado, você terá o banco de dados AdventureWorks instalado em sua instância de SQL Server.  

Para obter mais informações sobre como anexar arquivos de banco de dados, consulte [anexar um banco de dados](../relational-databases/databases/attach-a-database.md). 

## <a name="install-to-azure-sql-database"></a>Instalar no banco de dados SQL do Azure


Se você ainda não tiver uma SQL Server no Azure, navegue até a [portal do Azure](https://portal.azure.com/) e crie um novo banco de dados SQL. No processo de criar um banco de dados, você criará um servidor do. Anote o servidor. Consulte [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos.

1. Conecte-se ao seu portal do Azure.
1. Selecione **criar um recurso** na parte superior esquerda do painel de navegação. 
1. Selecione **bancos** de dados e, em seguida, selecione **banco de dados SQL**. 
1. Preencha as informações solicitadas.
1. No campo **selecionar origem** , selecione **exemplo (AdventureWorksLT)** para restaurar um backup do backup do AdventureWorksLT mais recente.
1. Selecione **criar** para criar seu novo banco de dados SQL, que é a cópia restaurada do banco de dados AdventureWorksLT. 


## <a name="see-also"></a>Confira também
[Tutoriais para SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[Tutoriais para o mecanismo de banco de dados SQL Server](../relational-databases/database-engine-tutorials.md)
