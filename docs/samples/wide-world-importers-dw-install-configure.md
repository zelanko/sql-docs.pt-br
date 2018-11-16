---
title: Banco de dados de exemplo do OLAP WideWorldImporters - instale e configure - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 0a1335b430346cf64d143ce3e07887d78f65a451
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51662325"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW de instalação e configuração
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Instruções de instalação e configuração para o banco de dados WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (ou superior) ou [banco de dados SQL](https://azure.microsoft.com/services/sql-database/). Para usar a versão completa do exemplo, use o SQL Server Developer/avaliação/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.

## <a name="download"></a>Download

A versão mais recente do exemplo:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

Baixe o exemplo WideWorldImportersDW banco de dados backup/bacpac que corresponde à sua edição do SQL Server ou banco de dados SQL.

O código-fonte para recriar o banco de dados de exemplo está disponível no seguinte local. Observe que o preenchimento dos dados é baseado no ETL do banco de dados OLTP (WideWorldImporters):

[wide-world-importers-source](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>Instalar


### <a name="sql-server"></a>SQL Server

Para restaurar um backup de uma instância do SQL Server, você pode usar o Management Studio.

1. Abra o SQL Server Management Studio e conecte-se à instância do SQL Server de destino.
2. Clique com botão direito no **bancos de dados** nó e selecione **restaurar banco de dados**.
3. Selecione **dispositivo** e clique no botão **...**
4. Na caixa de diálogo **Selecione dispositivos de backup**, clique em **Add**, navegue até o backup de banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino para os dados e arquivos de log, além de **arquivos** painel. Observe que é uma prática recomendada colocar dados e arquivos de log em unidades diferentes.
6. Clique em **OK**. Isso iniciará a restauração de banco de dados. Depois que ela for concluída, você terá o banco de dados de WideWorldImporters instalados na instância do SQL Server.

### <a name="azure-sql-database"></a>Banco de dados SQL do Azure

Para importar um bacpac para um novo banco de dados SQL, você pode usar o Management Studio.

1. (opcional) Se você ainda não tiver um SQL Server no Azure, navegue até a [portal do Azure](https://portal.azure.com/) e crie um novo banco de dados SQL. No processo de criar um banco de dados, você criará um servidor. Anote o servidor.
   - Ver [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos
2. Abra o SQL Server Management Studio e conecte-se ao seu servidor no Azure.
3. Clique com botão direito no **bancos de dados** nó e selecione **importar aplicativo da camada de dados**.
4. No **configurações de importação** selecionar **importar de disco local** e selecione o bacpac do banco de dados de exemplo no seu sistema de arquivos.
5. Sob **configurações de banco de dados** altere o nome do banco de dados para *WideWorldImportersDW* e selecione o objetivo de edição e o serviço de destino para usar.
6. Clique em **próxima** e **concluir** para disparar a implantação. Levará alguns minutos para ser concluída. Ao especificar um objetivo de serviço inferior S2 pode levar mais tempo.

## <a name="configuration"></a>Configuração

[Aplica-se ao SQL Server 2016 (e posterior) Evaluation/desenvolvedor/Enterprise Edition]

O banco de dados de exemplo pode fazer com o uso do PolyBase para arquivos de consulta no armazenamento de BLOBs do Azure ou Hadoop. No entanto, esse recurso não está instalado por padrão com o SQL Server – você precisa selecioná-lo durante a instalação do SQL Server. Portanto, uma etapa pós-instalação é necessária.

1. No SQL Server Management Studio, conecte-se ao banco de dados WideWorldImportersDW e abra uma nova janela de consulta.
2. Execute o seguinte comando T-SQL para habilitar o uso do PolyBase no banco de dados:

   EXECUTE [aplicativo]. [Configuration_ApplyPolyBase]
