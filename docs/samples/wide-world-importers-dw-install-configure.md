---
title: Instalar & configurar o banco de dados de exemplo do DW WideWorldImporters
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
ms.openlocfilehash: d8768fec2f96c725a9ba4bbf91996e95de4c800a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74056298"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>Instalação e configuração do WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Instruções de instalação e configuração para o banco de dados WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (ou superior) ou [banco de dados SQL do Azure](https://azure.microsoft.com/services/sql-database/). Para usar a versão completa do exemplo, use Avaliação do SQL Server/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.

## <a name="download"></a>Baixar

A versão mais recente do exemplo:

[Wide-World-outporters-versão](https://go.microsoft.com/fwlink/?LinkID=800630)

Baixe o exemplo de backup/bacpac do banco de dados WideWorldImportersDW que corresponde à sua edição do SQL Server ou banco de dados SQL do Azure.

O código-fonte para recriar o banco de dados de exemplo está disponível no seguinte local. Observe que a população de dados se baseia no ETL do banco de dados OLTP (WideWorldImporters):

[Wide-World-outporters-fonte](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>Instalar


### <a name="sql-server"></a>SQL Server

Para restaurar um backup em uma instância do SQL Server, você pode usar Management Studio.

1. Abra SQL Server Management Studio e conecte-se à instância de SQL Server de destino.
2. Clique com o botão direito do mouse no nó **bancos** de dados e selecione **Restore Database**.
3. Selecione **dispositivo** e clique no botão **...**
4. Na caixa de diálogo **selecionar dispositivos de backup**, clique em **Adicionar**, navegue até o backup do banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino dos arquivos de dados e de log no painel **arquivos** . Observe que é uma prática recomendada posicionar arquivos de dados e de log em unidades diferentes.
6. Clique em **OK**. Isso iniciará a restauração do banco de dados. Após a conclusão, você terá o banco de dados WideWorldImporters instalado em sua instância de SQL Server.

### <a name="azure-sql-database"></a>Banco de Dados SQL do Azure

Para importar um bacpac para um novo banco de dados SQL, você pode usar Management Studio.

1. adicional Se você ainda não tiver uma SQL Server no Azure, navegue até a [portal do Azure](https://portal.azure.com/) e crie um novo banco de dados SQL. No processo de criar um banco de dados, você criará um servidor do. Anote o servidor.
   - Consulte [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos
2. Abra SQL Server Management Studio e conecte-se ao servidor no Azure.
3. Clique com o botão direito do mouse no nó **bancos** de dados e selecione **importar aplicativo da camada de dados**.
4. Em **configurações de importação** , selecione **Importar do disco local** e selecione o bacpac do banco de dados de exemplo do sistema de arquivos.
5. Em **configurações do banco de dados** , altere o nome do banco de dados para *WideWorldImportersDW* e selecione a edição de destino e o objetivo de serviço a serem usados.
6. Clique em **Avançar** e em **concluir** para iniciar a implantação. Isso levará alguns minutos para ser concluído. Ao especificar um objetivo de serviço inferior a S2, pode levar mais tempo.

## <a name="configuration"></a>Configuração

[Aplica-se a SQL Server 2016 (e posterior) Developer/Evaluation/Enterprise Edition]

O banco de dados de exemplo pode fazer uso do polybase para consultar arquivos no Hadoop ou no armazenamento de BLOBs do Azure. No entanto, esse recurso não é instalado por padrão com o SQL Server-você precisa selecioná-lo durante a instalação do SQL Server. Portanto, uma etapa pós-instalação é necessária.

1. No SQL Server Management Studio, conecte-se ao banco de dados WideWorldImportersDW e abra uma nova janela de consulta.
2. Execute o seguinte comando T-SQL para habilitar o uso do polybase no banco de dados:

   EXECUTE [Application]. [Configuration_ApplyPolyBase]
