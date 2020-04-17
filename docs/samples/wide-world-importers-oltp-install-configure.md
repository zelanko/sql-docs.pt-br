---
title: Instale e configure o banco de dados de amostra wideworldimporters
description: Siga estas instruções para baixar, instalar e configurar o banco de dados de amostra wideworldimporters com o SQL Server Management Studio.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 355eaa254fcc7bb6cd4aa9a39c2cbcb269d88396
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487065"
---
# <a name="installation-and-configuration"></a>Instalação e configuração
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Instruções de instalação e configuração do banco de dados Wide World Importers OLTP.

## <a name="prerequisites"></a>Pré-requisitos

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (ou superior) ou [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). Para a versão completa da amostra, use SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obter os melhores resultados, use a versão de junho de 2016 ou posterior.

## <a name="download"></a>Baixar

A última versão da amostra:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

Baixe a amostra de backup/bacpac do banco de dados WideWorldImporters que corresponde à sua edição do SQL Server ou do Azure SQL Database.

O código-fonte para recriar o banco de dados de amostras está disponível a partir do local a seguir. Observe que a recriação da amostra resultará em pequenas diferenças nos dados, uma vez que há um fator aleatório na geração de dados:

[grandes importadores do mundo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

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
5. Em **Configurações de banco de dados** altere o nome do banco de dados para *WideWorldImporters* e selecione o objetivo de edição e serviço de destino a ser usado.
6. Clique **em "Avançar** e **Terminar"** para iniciar a implantação. Ele vai alguns minutos para completar em um P1. Se um nível de preços mais baixo for desejado, recomenda-se importar para um novo banco de dados P1 e, em seguida, alterar o nível de preços para o nível desejado.

## <a name="configuration"></a>Configuração

### <a name="full-text-indexing"></a>Indexação de texto completo

O banco de dados de amostras pode fazer uso da Indexação de Texto Completo. No entanto, esse recurso não é instalado por padrão com o SQL Server - você precisa selecioná-lo durante a configuração do SQL Server (ele é ativado por padrão no Azure SQL DB). Portanto, é necessária uma etapa pós-instalação.

1. No SQL Server Management Studio, conecte-se ao banco de dados WideWorldImporters e abra uma nova janela de consulta.
2. Execute o seguinte comando T-SQL para permitir o uso da Indexação de Texto Completo no banco de dados:`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>Auditoria do SQL Server

Aplica-se a: SQL Server

Habilitar a auditoria no SQL Server requer a configuração do servidor. Para habilitar a auditoria do SQL Server para a amostra WideWorldImporters, execute a seguinte declaração no banco de dados:

    EXECUTE [Application].[Configuration_ApplyAuditing]

No Banco de Dados SQL do Azure, a auditoria é configurada através do [portal Azure](https://portal.azure.com/).

### <a name="row-level-security"></a>Segurança em nível de linha

Aplica-se a: Banco de Dados SQL do Azure

A Segurança em Nível de Linha não é habilitada por padrão no download bacpac do WideWorldImporters. Para habilitar a segurança em nível de linha no banco de dados, execute o seguinte procedimento armazenado:

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

