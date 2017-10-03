---
title: "Instalação e configuração | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6dd1f09b-dcff-4627-899a-eca5162d9e5b
caps.latest.revision: 4
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 3b4a02b7b8c17f6bd5a75714a8fc3357dcfbd9a3
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="installation-and-configuration"></a>Instalação e configuração
Wide World Importers OLTP instruções de instalação e configuração do banco de dados.

## <a name="prerequisites"></a>Pré-requisitos

- [SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) (ou superior) ou [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/). Para obter a versão completa do exemplo, use o SQL Server Developer/avaliação/Enterprise Edition.
- [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.

## <a name="download"></a>Download

A versão mais recente do exemplo:

[todo-world importers versão](http://go.microsoft.com/fwlink/?LinkID=800630)

Baixe o exemplo WideWorldImporters banco de dados backup/bacpac que corresponde à sua edição do SQL Server ou banco de dados do SQL Azure.

Código-fonte para recriar o banco de dados de exemplo está disponível no seguinte local. Observe que recriar a amostra resultará em pequenas diferenças nos dados, pois já existe um fator aleatório na geração de dados:

[world-wide-importadores](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Instalar


### <a name="sql-server"></a>SQL Server

Para restaurar um backup de uma instância do SQL Server, você pode usar o Management Studio.

1. Abra o SQL Server Management Studio e conecte-se à instância do SQL Server de destino.
2. Clique com botão direito no **bancos de dados** nó e selecione **restaurar banco de dados**.
3. Selecione **dispositivo** e clique no botão **...**
4. Na caixa de diálogo **Selecione dispositivos de backup**, clique em **adicionar**, navegue até o backup do banco de dados no sistema de arquivos do servidor e selecione o backup. Clique em **OK**.
5. Se necessário, altere o local de destino para os dados e arquivos de log, além de **arquivos** painel. Observe que é uma prática recomendada para colocar os dados e arquivos de log em unidades diferentes.
6. Clique em **OK**. Isso irá iniciar a restauração do banco de dados. Depois de concluir, você terá o banco de dados de WideWorldImporters instalados na instância do SQL Server.

### <a name="azure-sql-database"></a>Banco de dados SQL do Azure

Para importar um bacpac para um novo banco de dados SQL, você pode usar o Management Studio.

1. (opcional) Se você ainda não tiver um SQL Server no Azure, navegue até o [portal do Azure](https://portal.azure.com/) e criar um novo banco de dados SQL. No processo de criar um banco de dados, você criará um servidor. Anote o servidor.
   - Consulte [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para criar um banco de dados em minutos
2. Abra o SQL Server Management Studio e conecte-se ao seu servidor no Azure.
3. Clique com botão direito no **bancos de dados** nó e selecione **importar aplicativo da camada de dados**.
4. No **importar configurações** selecione **importar de disco local** e selecione o bacpac do banco de dados de exemplo do seu sistema de arquivos.
5. Em **configurações de banco de dados** altere o nome do banco de dados para *WideWorldImporters* e selecione o objetivo de edição e o serviço de destino a ser usado.
6. Clique em **próximo** e **concluir** para disparar a implantação. Ele será alguns minutos para ser concluída em um P1. Se um preço mais baixo nível é desejado, é recomendável importar para um novo banco de dados de P1, e, em seguida, altere a camada de preços para o nível desejado.

## <a name="configuration"></a>Configuração

### <a name="full-text-indexing"></a>Indexação de texto completo

O banco de dados de exemplo pode fazer uso de indexação de texto completo. No entanto, esse recurso não está instalado por padrão com o SQL Server - você precisa para selecioná-la durante a instalação do SQL Server (ela é habilitada por padrão no banco de dados de SQL Azure). Portanto, uma etapa pós-instalação é necessária.

1. No SQL Server Management Studio, conecte-se ao banco de dados de WideWorldImporters e abrir uma nova janela de consulta.
2. Execute o seguinte comando T-SQL para habilitar o uso de indexação de texto completo no banco de dados:`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>Auditoria do SQL Server

Aplica-se a: SQL Server

Habilitar a auditoria do SQL Server requer a configuração do servidor. Para habilitar a auditoria do SQL Server para o exemplo de WideWorldImporters, execute a seguinte instrução no banco de dados:

    EXECUTE [Application].[Configuration_ApplyAuditing]

No banco de dados SQL Azure, a auditoria é configurada por meio de [portal do Azure](https://portal.azure.com/).

### <a name="row-level-security"></a>Segurança em nível de linha

Aplica-se a: banco de dados SQL do Azure

Segurança em nível de linha não está habilitada por padrão no download do bacpac de WideWorldImporters. Para habilitar a segurança em nível de linha no banco de dados, execute o seguinte procedimento armazenado:

    EXECUTE [Application].[Configuration_ApplyAuditing]


