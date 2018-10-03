---
title: Instalar e configurar o banco de dados de exemplo de WideWorldImporters - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3860eae1663b512af1835a0e1268145a742d161a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701454"
---
# <a name="installation-and-configuration"></a>Instalação e configuração
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
OLTP de importadores mundiais instruções de instalação e configuração do banco de dados.

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) (ou superior) ou [banco de dados SQL](https://azure.microsoft.com/services/sql-database/). Para a versão completa do exemplo, use o SQL Server Developer/avaliação/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.

## <a name="download"></a>Download

A versão mais recente do exemplo:

[wide-world-importers-release](http://go.microsoft.com/fwlink/?LinkID=800630)

Baixe o exemplo WideWorldImporters banco de dados backup/bacpac que corresponde à sua edição do SQL Server ou banco de dados SQL.

O código-fonte para recriar o banco de dados de exemplo está disponível no seguinte local. Observe que recriar a amostra resultará em pequenas diferenças nos dados, já que não há um fator aleatório na geração de dados:

[wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

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
5. Sob **configurações de banco de dados** altere o nome do banco de dados para *WideWorldImporters* e selecione o objetivo de edição e o serviço de destino para usar.
6. Clique em **próxima** e **concluir** para disparar a implantação. Ele será alguns minutos para ser concluída em um P1. Se uma redução de preços camada for desejado, é recomendável importar para um novo banco de dados P1 e, em seguida, altere o tipo de preço para o nível desejado.

## <a name="configuration"></a>Configuração

### <a name="full-text-indexing"></a>Indexação de texto completo

O banco de dados de exemplo pode fazer com o uso da indexação de texto completo. No entanto, esse recurso não está instalado por padrão com o SQL Server – você precisa selecioná-lo durante a instalação do SQL Server (ela é habilitada por padrão no BD SQL do Azure). Portanto, uma etapa pós-instalação é necessária.

1. No SQL Server Management Studio, conecte-se ao banco de dados de WideWorldImporters e abra uma nova janela de consulta.
2. Execute o seguinte comando T-SQL para habilitar o uso da indexação de texto completo no banco de dados:  `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>Auditoria do SQL Server

Aplica-se a: SQL Server

Habilitar a auditoria no SQL Server requer a configuração do servidor. Para habilitar a auditoria do SQL Server para o exemplo WideWorldImporters, execute a seguinte instrução no banco de dados:

    EXECUTE [Application].[Configuration_ApplyAuditing]

No banco de dados SQL Azure, a auditoria é configurada por meio de [portal do Azure](https://portal.azure.com/).

### <a name="row-level-security"></a>Segurança em nível de linha

Aplica-se a: banco de dados SQL do Azure

Segurança em nível de linha não está habilitada por padrão no download de WideWorldImporters bacpac. Para habilitar a segurança em nível de linha no banco de dados, execute o seguinte procedimento armazenado:

    EXECUTE [Application].[Configuration_ApplyAuditing]

