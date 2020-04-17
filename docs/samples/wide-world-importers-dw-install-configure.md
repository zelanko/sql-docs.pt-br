---
title: Instalar & configurar o banco de dados de amostra DW WideWorldImporters
description: Siga estas instruções para baixar, instalar e configurar o banco de dados de amostra wideworldimportersDW com o SQL Server Management Studio.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 2f640415ecdc2ae4a48220aeec2a2c78ed79807c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488535"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>Instalação e configuração do WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Instruções de instalação e configuração para o banco de dados WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (ou superior) ou [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). Para usar a versão completa da amostra, use SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.

## <a name="download"></a>Baixar

A última versão da amostra:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

Baixe a amostra de backup/bacpac do banco de dados WideWorldImportersDW que corresponde à sua edição do SQL Server ou do Azure SQL Database.

O código-fonte para recriar o banco de dados de amostras está disponível a partir do local a seguir. Observe que a população de dados é baseada em ETL do banco de dados OLTP (WideWorldImporters):

[de todo o mundo-importadores-fonte](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

## <a name="install"></a>Instalar


### <a name="sql-server"></a>SQL Server

Para restaurar um backup em uma instância do SQL Server, você pode usar o Management Studio.

1. Abra o SQL Server Management Studio e conecte-se à instância de destino do SQL Server.
2. Clique com o botão direito do mouse no nó Banco sé.o e selecione **Restaurar banco de dados**. **Databases**
3. Selecione **Dispositivo** e clique no botão **...**
4. Na caixa de diálogo **Selecione dispositivos de backup,** clique em **Adicionar,** navegue até o backup do banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino dos dados e arquivos de registro, no painel **Arquivos.** Observe que é melhor praticar colocar dados e registrar arquivos em diferentes unidades.
6. Clique em **OK**. Isso iniciará a restauração do banco de dados. Depois que ele for concluído, você terá o banco de dados WideWorldImporters instalado na instância do SQL Server.

### <a name="azure-sql-database"></a>Banco de Dados SQL do Azure

Para importar um bacpac em um novo Banco de Dados SQL, você pode usar o Management Studio.

1. (opcional) Se você ainda não tiver um SQL Server no Azure, navegue até o [portal Azure](https://portal.azure.com/) e crie um novo Banco de Dados SQL. No processo de criação de um banco de dados, você criará um servidor. Anote o servidor.
   - Veja [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos
2. Abra o SQL Server Management Studio e conecte-se ao seu servidor no Azure.
3. Clique com o botão direito do mouse no nó **Bancos** de Dados e selecione **Import Data-Tier Application**.
4. Nas **Configurações de importação,** **selecione Importar do disco local** e selecione o bacpac do banco de dados de exemplo do seu sistema de arquivos.
5. Em **Configurações de banco de dados** altere o nome do banco de dados para *WideWorldImportersDW* e selecione o objetivo de edição e serviço de destino a ser usado.
6. Clique **em "Avançar** e **Terminar"** para iniciar a implantação. Isso levará alguns minutos para ser concluído. Ao especificar um objetivo de serviço menor que o S2, pode levar mais tempo.

## <a name="configuration"></a>Configuração

[Aplica-se ao SQL Server 2016 (e posteriormente) Desenvolvedor/Avaliação/Edição Corporativa]

O banco de dados de exemplo pode fazer uso do PolyBase para consultar arquivos no armazenamento de blob Hadoop ou Azure. No entanto, esse recurso não é instalado por padrão com o SQL Server - você precisa selecioná-lo durante a configuração do SQL Server. Portanto, é necessária uma etapa pós-instalação.

1. No SQL Server Management Studio, conecte-se ao banco de dados WideWorldImportersDW e abra uma nova janela de consulta.
2. Execute o seguinte comando T-SQL para permitir o uso do PolyBase no banco de dados:

   EXECUTE [Aplicativo]. [Configuration_ApplyPolyBase]
