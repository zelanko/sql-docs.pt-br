---
title: Instale e configure o banco de dados de amostras AdventureWorks
description: Siga estas instruções para baixar e instalar bancos de dados de amostra AdventureWorks com o SQL Server Management Studio ou no Azure SQL Database.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 7fa3d199450750a444f2b67ae3e4583549d449b9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484565"
---
# <a name="adventureworks-installation-and-configuration"></a>Instalação e configuração do AdventureWorks
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks baixe links e instruções de instalação. 

## <a name="prerequisites"></a>Pré-requisitos

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) ou [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). Para a versão completa da amostra, use SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.
 
## <a name="oltp-downloads"></a>Downloads OLTP

Links diretos para as versões OLTP do AdventureWorks podem ser encontrados abaixo:

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>Downloads do Data Warehouse

Links diretos para as versões do Data Warehouse do AdventureWorks podem ser encontrados abaixo:

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksD2008R2.bak](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak)

## <a name="creation-scripts"></a>Scripts de criação
Os scripts abaixo podem ser usados para criar todo o banco de dados AdventureWorks, independentemente da versão. 

- [AdventureWorks OLTP Scripts Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW Scripts Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>Links do GitHub

- [Todos os arquivos AdventureWorks para SQL 2014 - 2016](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [Todos os arquivos AdventureWorks para SQL 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [Todos os arquivos AdventureWorks para SQL 2008 e 2008R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>Instale no SQL Server

### <a name="restore-backup"></a>Restaurar backup
Siga as etapas abaixo para restaurar um backup do seu banco de dados usando o SQL Server Management Studio. 

1. Abra o SQL Server Management Studio e conecte-se à instância de destino do SQL Server.
2. Clique com o botão direito do mouse no nó Banco sé.o e selecione **Restaurar banco de dados**. **Databases**
3. Selecione **Dispositivo** e clique nas elipses (**...**)
4. Na caixa de diálogo **Selecione dispositivos de backup,** clique em **Adicionar,** navegue até o backup do banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino dos dados e arquivos de registro, no painel **Arquivos.** Observe que é melhor praticar colocar dados e registrar arquivos em diferentes unidades.
6. Clique em **OK**. Isso iniciará a restauração do banco de dados. Depois que ele for concluído, você terá o banco de dados AdventureWorks instalado na instância do SQL Server.

Para obter mais informações sobre como restaurar um banco de dados do SQL Server, consulte [Restaurar um backup de banco de dados usando SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).


### <a name="attach-a-datafile"></a>Anexar um arquivo de dados
Siga as etapas abaixo para anexar o arquivo de dados para o seu banco de dados usando o SQL Server Management Studio.

1. Abra o SQL Server Management Studio e conecte-se à instância de destino do SQL Server.
2. Clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Anexar**.
3. Selecione **Adicionar** e navegar até o . Arquivo MDF que você deseja anexar. 
1. Selecione o arquivo e clique em **OK**. 
    1. O banco de dados selecionado deve ser exibido na janela inferior. Se o arquivo estiver listado como "não encontrado", selecione as elipses (**...**) ao lado do nome do arquivo e atualize o caminho para o caminho correto. 
    1. Se você tiver apenas o arquivo de dados (.mdf) e não o arquivo de log (.ldf), então destaque o .ldf na janela inferior e selecione **Remover**. Isso criará um novo arquivo de log. 
1. Selecione **OK** para anexar o arquivo. Depois que o arquivo for anexado, você terá o banco de dados AdventureWorks instalado na instância do SQL Server.  

Para obter mais informações sobre a anexação de arquivos de banco de dados, consulte [Anexar um banco de dados](../relational-databases/databases/attach-a-database.md). 

## <a name="install-to-azure-sql-database"></a>Instale no Banco de Dados SQL do Azure


Se você ainda não tiver um SQL Server no Azure, navegue até o [portal Azure](https://portal.azure.com/) e crie um novo Banco de Dados SQL. No processo de criação de um banco de dados, você criará um servidor. Anote o servidor. Veja [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos.

1. Conecte-se ao seu portal Azure.
1. Selecione **Criar um recurso** no canto superior esquerdo do painel de navegação. 
1. Selecione **Bancos de Dados** e, em seguida, selecione **Banco de Dados SQL**. 
1. Preencha as informações solicitadas.
1. No campo **Selecionar origem,** selecione **Sample (AdventureWorksLT)** para restaurar um backup do backup mais recente do AdventureWorksLT.
1. Selecione **Criar** para criar seu novo banco de dados SQL, que é a cópia restaurada do banco de dados AdventureWorksLT. 


## <a name="see-also"></a>Confira também
[Tutoriais para SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[Tutoriais para o mecanismo de banco de dados SQL Server](../relational-databases/database-engine-tutorials.md)
