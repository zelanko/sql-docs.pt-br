---
title: Virtualizar dados externos no SQL Server 2019 CTP 2.0 | Microsoft Docs
description: Esta página fornece detalhes sobre as etapas para usar o assistente criar tabela externa para um arquivo CSV
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6a8ce50e4e359c8ce8dc2b0015300f9a7afb88d1
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710604"
---
# <a name="use-the-external-table-wizard-with-csv-files"></a>Usar o Assistente de Tabela Externa com arquivos CSV

O SQL Server 2019 também permite a capacidade de virtualizar os dados de um arquivo CSV no HDFS.  Esse processo permite que os dados permaneçam em seu local original, no entanto, é possível **virtualizar** os dados em uma instância do SQL Server para que ela possa ser consultada lá como qualquer outra tabela no SQL Server. Esse recurso minimizará a necessidade de processos de ETL. Isso é possível com o uso de conectores do Polybase. Para obter mais informações sobre a Virtualização de dados, confira nosso documento de [Introdução ao PolyBase](polybase-guide.md).

## <a name="prerequisite"></a>Pré-requisito

No CTP 2.4 em diante, as fontes de dados externas do pool de dados e do pool de armazenamento não são mais criadas por padrão no cluster de Big Data. Antes de usar o assistente, crie a fonte de dados externa **SqlStoragePool** padrão no banco de dados de destino com a consulta Transact-SQL a seguir. Primeiro altere o contexto da consulta para o banco de dados de destino.

```sql
-- Create default data sources for SQL Big Data Cluster
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
    CREATE EXTERNAL DATA SOURCE SqlDataPool
    WITH (LOCATION = 'sqldatapool://controller-svc/default');

IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://controller-svc/default');
```

## <a name="launch-the-external-table-wizard"></a>Inicializar o Assistente de tabela externa

Conecte-se à raiz do HDFS usando o endereço IP. Expanda os elementos no Pesquisador de Objetos. Em seguida, selecione um dos CSV dos quais você gostaria de virtualizar os dados em uma instância do SQL Server existente. Clique com o botão direito do mouse no arquivo e selecione **Criar Tabela Externa do Arquivo CSV** no menu de contexto. Você também poderá criar tabelas externas de arquivos CSV de uma pasta no HDFS se os arquivos na pasta seguirem o mesmo esquema. Isso permitirá a virtualização de dados em um nível de pasta sem necessidade de processar arquivos individuais e obter um conjunto de resultados unido sobre os dados combinados. Isso inicia o Assistente de virtualização de dados. Você também pode iniciar o Assistente de virtualização de dados na paleta de comandos pressionando Ctrl+Shift+P (no Windows) e Cmd+Shift+P (no Mac).

![Assistente de virtualização de dados](media/data-virtualization/csv-virtualize-data-wizard.png)

## <a name="connect-to-a-sql-server-master-instance"></a>Conectar a uma Instância Mestra do SQL Server

Aqui você pode especificar a qual instância mestra do SQL você se conectará usando as informações de IP, Porta e Credencial. Conexões salvas anteriormente podem ser acessadas por meio da caixa suspensa **Conexões do SQL Server ativas**. 
> [!NOTE]
>Se você estiver usando uma conexão salva, os outros campos estarão bloqueados


![Selecionar uma fonte de dados](media/data-virtualization/csv-connect-to-master.png)

Clique em Avançar para prosseguir para a próxima etapa do assistente que define a Chave Mestra do Banco de Dados.

## <a name="select-destination-database"></a>Selecionar Banco de Dados de Destino

Nesta etapa, você escolherá o banco de dados de destino no qual deseja virtualizar os dados. O campo de lista suspensa conterá todos os bancos de dados aceitáveis na instância do SQL Master especificada na tela anterior. Aqui você também pode nomear a nova tabela externa e ver o esquema que ela vai usar.

![Criar uma chave mestra de banco de dados](media/data-virtualization/csv-select-destination.png)


## <a name="preview-data"></a>Visualizar Dados

Nesta janela, você poderá ver uma versão prévia das primeiras 50 linhas do arquivo CSV para validação.

Depois de terminar de exibir a versão prévia, clique em "Avançar" para continuar

![Credenciais de fonte de dados externa](media/data-virtualization/csv-preview-data.png)

## <a name="modify-columns"></a>Modificar Colunas

Na próxima janela, você poderá Modificar as colunas da tabela externa que pretende criar. é possível alterar o nome da coluna, Alterar o tipo de dados e permitir linhas Anuláveis. 

![Credenciais de fonte de dados externa](media/data-virtualization/csv-modify-columns.png)


## <a name="summary"></a>Resumo

Essa etapa fornece um resumo das suas seleções. Fornece informações sobre a tabela Externa Proposta e de Instância Mestra do SQL. Nesta etapa, você tem a opção de **"Gerar Script"** , que gerará script em T-SQL a sintaxe para criar a fonte de dados externa ou **Criar** que criará o objeto da Fonte de dados externa.

![Tela de resumo](media/data-virtualization/csv-virtualize-data-summary.png)

Se você clicar em "Criar", poderá ver a tabela Externa criada no Banco de dados de Destino.

![Fontes de dados externas](media/data-virtualization/csv-external-data-sources.png)

Se você clicar em **Gerar Script**, verá a consulta T-SQL que está sendo gerada para criar o objeto de Fonte de dados externa.

![Gerar script](media/data-virtualization/csv-generated-script.png)

> [!NOTE]
> Gerar Script estará visível somente na última página do assistente. Atualmente, essa opção é mostrada em todas as páginas.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o Cluster de Big Data do SQL Server e cenários relacionados, consulte [O que é o Cluster de Big Data do SQL Server?](../../big-data-cluster/big-data-cluster-overview.md).
