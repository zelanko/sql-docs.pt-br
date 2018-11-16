---
title: Instalar e configurar o banco de dados de exemplo AdventureWorks - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7881400c3e4696426b1999229e917630cf905d0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657506"
---
# <a name="adventureworks-installation-and-configuration"></a>Configuração e instalação de AdventureWorks
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Baixe o AdventureWorks links e instruções de instalação. 

## <a name="prerequisites"></a>Prerequisites

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) ou [banco de dados SQL do Azure](https://azure.microsoft.com/services/sql-database/). Para a versão completa do exemplo, use o SQL Server Developer/avaliação/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.
 
## <a name="github-links"></a>Links do GitHub

- [Todos os arquivos AdventureWorks para SQL 2016 de 2014](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [Todos os arquivos AdventureWorks do SQL 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [Todos os arquivos AdventureWorks para SQL 2008 e 2008 R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>Downloads OLTP

Links diretos para as versões OLTP da AdventureWorks podem ser encontrados abaixo:

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
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>Scripts de criação
Os scripts abaixo pode ser usado para criar todo banco de dados AdventureWorks, independentemente da versão. 

- [Zip de Scripts do AdventureWorks OLTP](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [Zip de Scripts do AdventureWorks DW](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>Instalar o SQL Server

### <a name="restore-backup"></a>Restaurar backup
Siga as etapas a seguir para restaurar um backup de banco de dados usando o SQL Server Management Studio. 

1. Abra o SQL Server Management Studio e conecte-se à instância do SQL Server de destino.
2. Clique com botão direito no **bancos de dados** nó e selecione **restaurar banco de dados**.
3. Selecione **dispositivo** e clique nas reticências (**...** )
4. Na caixa de diálogo **Selecione dispositivos de backup**, clique em **Add**, navegue até o backup de banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino para os dados e arquivos de log, além de **arquivos** painel. Observe que é uma prática recomendada colocar dados e arquivos de log em unidades diferentes.
6. Clique em **OK**. Isso iniciará a restauração de banco de dados. Depois que ela for concluída, você terá um banco de dados AdventureWorks instalado na instância do SQL Server.

Para obter mais informações sobre como restaurar um banco de dados do SQL Server, consulte [restaurar um backup de banco de dados usando o SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).


### <a name="attach-a-datafile"></a>Anexar um arquivo de dados
Siga as etapas a seguir para anexar o arquivo de dados do banco de dados usando o SQL Server Management Studio.

1. Abra o SQL Server Management Studio e conecte-se à instância do SQL Server de destino.
2. Clique com botão direito no **bancos de dados** nó e selecione **Attach**.
3. Selecione **adicionar** e navegue até o. Arquivo MDF que você deseja anexar. 
1. Selecione o arquivo e clique em **Okey**. 
    1. O banco de dados selecionado deve ser exibido na janela inferior. Se o arquivo é listado como "não encontrado", selecione as reticências (**...** ) ao lado do nome de arquivo e atualizar o caminho para o caminho correto. 
    1. Se você tiver apenas o arquivo de dados (. mdf) e não o arquivo de log (. ldf), em seguida, realce o. ldf na janela inferior e selecione **remover**. Isso criará um novo arquivo de log. 
1. Selecione **Okey** para anexar o arquivo. Depois que o arquivo é anexado, você terá um banco de dados AdventureWorks instalado na instância do SQL Server.  

Para obter mais informações sobre como anexar arquivos de banco de dados, consulte [anexar um banco de dados](../relational-databases/databases/attach-a-database.md). 

## <a name="install-to-azure-sql-database"></a>Instalar o banco de dados SQL do Azure


Se você ainda não tiver um SQL Server no Azure, navegue até a [portal do Azure](https://portal.azure.com/) e crie um novo banco de dados SQL. No processo de criar um banco de dados, você criará um servidor. Anote o servidor. Ver [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos.

1. Conecte-se ao seu portal do Azure.
1. Selecione **criar um recurso** na parte superior esquerda do painel de navegação. 
1. Selecione **bancos de dados** e, em seguida, selecione **banco de dados SQL**. 
1. Preencha as informações solicitadas.
1. No **Selecionar origem** campo, selecione **exemplo (AdventureWorksLT)** para restaurar um backup do backup mais recente do AdventureWorksLT.
1. Selecione **criar** para criar um novo banco de dados SQL, que é a cópia restaurada do banco de dados AdventureWorksLT. 


## <a name="see-also"></a>Confira também
[Tutoriais do SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
[tutoriais do mecanismo de banco de dados do SQL Server](../relational-databases/database-engine-tutorials.md)
