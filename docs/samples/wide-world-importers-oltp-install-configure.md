---
title: Instalar e configurar o banco de dados de exemplo WideWorldImporters
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: e1683adfa20851d279e8b8e18a3c767db9e5810d
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056269"
---
# <a name="installation-and-configuration"></a>Instalação e configuração
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Instruções de configuração e instalação do banco de dados OLTP de importadores mundiais.

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (ou superior) ou [banco de dados SQL do Azure](https://azure.microsoft.com/services/sql-database/). Para obter a versão completa do exemplo, use Avaliação do SQL Server/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.

## <a name="download"></a>Download

A versão mais recente do exemplo:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

Baixe o exemplo de backup/bacpac do banco de dados WideWorldImporters que corresponde à sua edição do SQL Server ou banco de dados SQL do Azure.

O código-fonte para recriar o banco de dados de exemplo está disponível no seguinte local. Observe que a recriação do exemplo resultará em pequenas diferenças nos dados, já que há um fator aleatório na geração de dados:

[wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Instalar


### <a name="sql-server"></a>SQL Server

Para restaurar um backup em uma instância do SQL Server, você pode usar Management Studio.

1. Abra SQL Server Management Studio e conecte-se à instância de SQL Server de destino.
2. Clique com o botão direito do mouse no nó **bancos** de dados e selecione **Restore Database**.
3. Selecione **dispositivo** e clique no botão **...**
4. Na caixa de diálogo **selecionar dispositivos de backup**, clique em **Adicionar**, navegue até o backup do banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino dos arquivos de dados e de log no painel **arquivos** . Observe que é uma prática recomendada posicionar arquivos de dados e de log em unidades diferentes.
6. Clique em **OK**. Isso iniciará a restauração do banco de dados. Após a conclusão, você terá o banco de dados WideWorldImporters instalado em sua instância de SQL Server.

### <a name="azure-sql-database"></a>Azure SQL Database

Para importar um bacpac para um novo banco de dados SQL, você pode usar Management Studio.

1. adicional Se você ainda não tiver uma SQL Server no Azure, navegue até a [portal do Azure](https://portal.azure.com/) e crie um novo banco de dados SQL. No processo de criar um banco de dados, você criará um servidor do. Anote o servidor.
   - Consulte [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos
2. Abra SQL Server Management Studio e conecte-se ao servidor no Azure.
3. Clique com o botão direito do mouse no nó **bancos** de dados e selecione **importar aplicativo da camada de dados**.
4. Em **configurações de importação** , selecione **Importar do disco local** e selecione o bacpac do banco de dados de exemplo do sistema de arquivos.
5. Em **configurações do banco de dados** , altere o nome do banco de dados para *WideWorldImporters* e selecione a edição de destino e o objetivo de serviço a serem usados.
6. Clique em **Avançar** e em **concluir** para iniciar a implantação. Haverá alguns minutos para ser concluído em um P1. Se um tipo de preço mais baixo for desejado, é recomendável importar para um novo banco de dados P1 e, em seguida, alterar o tipo de preço para o nível desejado.

## <a name="configuration"></a>Configuração

### <a name="full-text-indexing"></a>Indexação de texto completo

O banco de dados de exemplo pode fazer uso de indexação de texto completo. No entanto, esse recurso não é instalado por padrão com SQL Server-você precisa selecioná-lo durante a instalação do SQL Server (ele é habilitado por padrão no banco de BD SQL do Azure). Portanto, uma etapa pós-instalação é necessária.

1. No SQL Server Management Studio, conecte-se ao banco de dados WideWorldImporters e abra uma nova janela de consulta.
2. Execute o seguinte comando T-SQL para habilitar o uso de indexação de texto completo no banco de dados: `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>Auditoria do SQL Server

Aplica-se a: SQL Server

Habilitar a auditoria no SQL Server requer a configuração do servidor. Para habilitar SQL Server auditoria para o exemplo WideWorldImporters, execute a seguinte instrução no banco de dados:

    EXECUTE [Application].[Configuration_ApplyAuditing]

No banco de dados SQL do Azure, a auditoria é configurada por meio do [portal do Azure](https://portal.azure.com/).

### <a name="row-level-security"></a>Segurança em nível de linha

Aplica-se a: banco de dados SQL do Azure

A segurança em nível de linha não é habilitada por padrão no download de bacpac de WideWorldImporters. Para habilitar a segurança em nível de linha no banco de dados, execute o seguinte procedimento armazenado:

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

