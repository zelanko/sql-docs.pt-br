---
title: Banco de dados de exemplo WideWorldImporters OLAP - instale e configure - o SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 69eee1a6460509e70b061583d7a096c2b8293294
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW instalação e configuração
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Instruções de instalação e configuração para o banco de dados WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (ou superior) ou [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/). Para usar a versão completa do exemplo, use o SQL Server Developer/avaliação/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.

## <a name="download"></a>Download

A versão mais recente do exemplo:

[wide-world-importers-release](http://go.microsoft.com/fwlink/?LinkID=800630)

Baixe o exemplo WideWorldImportersDW banco de dados backup/bacpac que corresponde à sua edição do SQL Server ou banco de dados do SQL Azure.

Código-fonte para recriar o banco de dados de exemplo está disponível no seguinte local. Observe que a população de dados é baseada em ETL do banco de dados OLTP (WideWorldImporters):

[wide-world-importers-source](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>Instalar


### <a name="sql-server"></a>SQL Server

Para restaurar um backup de uma instância do SQL Server, você pode usar o Management Studio.

1. Abra o SQL Server Management Studio e conecte-se à instância do SQL Server de destino.
2. Clique com botão direito no **bancos de dados** nó e selecione **restaurar banco de dados**.
3. Selecione **dispositivo** e clique no botão **...**
4. Na caixa de diálogo **Selecione dispositivos de backup**, clique em **adicionar**, navegue até o backup do banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino para os dados e arquivos de log, além de **arquivos** painel. Observe que é uma prática recomendada para colocar os dados e arquivos de log em unidades diferentes.
6. Clique em **OK**. Isso irá iniciar a restauração do banco de dados. Depois de concluir, você terá o banco de dados de WideWorldImporters instalados na instância do SQL Server.

### <a name="azure-sql-database"></a>Azure SQL Database

Para importar um bacpac para um novo banco de dados SQL, você pode usar o Management Studio.

1. (opcional) Se você ainda não tiver um SQL Server no Azure, navegue até o [portal do Azure](https://portal.azure.com/) e criar um novo banco de dados SQL. No processo de criar um banco de dados, você criará um servidor. Anote o servidor.
   - Consulte [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos
2. Abra o SQL Server Management Studio e conecte-se ao seu servidor no Azure.
3. Clique com botão direito no **bancos de dados** nó e selecione **importar aplicativo da camada de dados**.
4. No **importar configurações** selecione **importar de disco local** e selecione o bacpac do banco de dados de exemplo do seu sistema de arquivos.
5. Em **configurações de banco de dados** altere o nome do banco de dados para *WideWorldImportersDW* e selecione o objetivo de edição e o serviço de destino a ser usado.
6. Clique em **próximo** e **concluir** para disparar a implantação. Levará alguns minutos para ser concluída. Ao especificar um objetivo de serviço inferior S2 pode levar mais tempo.

## <a name="configuration"></a>Configuração

[Aplica-se ao SQL Server 2016 (e posterior) Evaluation/desenvolvedor/Enterprise Edition]

O banco de dados de exemplo pode fazer uso do PolyBase para arquivos de consulta no armazenamento de BLOBs do Azure ou Hadoop. No entanto, esse recurso não está instalado por padrão com o SQL Server - você precisa para selecioná-la durante a instalação do SQL Server. Portanto, uma etapa pós-instalação é necessária.

1. No SQL Server Management Studio, conecte-se ao banco de dados WideWorldImportersDW e abrir uma nova janela de consulta.
2. Execute o seguinte comando T-SQL para permitir o uso do PolyBase no banco de dados:

   EXECUTE [aplicativo]. [Configuration_ApplyPolyBase]
