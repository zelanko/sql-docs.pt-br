---
title: Virtualizar dados CSV do pool de armazenamento
subtitle: Clusters de Big Data do SQL Server
description: Etapas que detalham a criação de uma tabela externa para virtualização de um arquivo CSV em um Cluster de Big Data
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/24/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.metadata: seo-lt-2019
ms.openlocfilehash: 6625e985781f3980c44bef9b6dbd408243ac78a9
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523846"
---
# <a name="virtualize-csv-data-from-storage-pool-big-data-clusters"></a>Virtualizar dados CSV do pool de armazenamento (Clusters de Big Data)

Os Clusters de Big Data do SQL Server podem virtualizar dados de arquivos CSV no HDFS. Esse processo permite que os dados permaneçam em seu local original, mas possam ser consultados de uma instância do SQL Server como qualquer outra tabela. Esse recurso usa conectores do PolyBase e minimiza a necessidade de processos de ETL. Para obter mais informações sobre a virtualização de dados, confira [O que é o PolyBase?](../relational-databases/polybase/polybase-guide.md)

## <a name="prerequisites"></a>Pré-requisitos

- [Um cluster de Big Data implantado](deployment-guidance.md)
- [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)

## <a name="select-or-upload-a-csv-file-for-data-virtualization"></a>Selecionar ou carregar um arquivo CSV para virtualização de dados 

No ADS (Azure Data Studio), [conecte-se à instância mestra do SQL Server](connect-to-big-data-cluster.md#master) do Cluster de Big Data. Uma vez conectado, expanda os elementos do HDFS no Pesquisador de Objetos para localizar os arquivos CSV cujos dados gostaria de virtualizar. 

Para os fins deste tutorial, crie um diretório chamado **Dados**.

1. Clique com o botão direito do mouse no menu de contexto do diretório raiz do HDFS.
2. Clique em **Novo diretório**.
3. Dê ao novo diretório o nome *Dados*.

Carregar os dados de exemplo. Para um passo a passo simples, você pode usar um arquivo de dados CSV de exemplo. Este artigo usa os dados de causas de atrasos de companhias aéreas do [Departamento de Transporte dos EUA](https://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp?pn=1). Baixe os dados brutos e extraia-os no computador. Nomeie o arquivo *airline_delay_causes. csv*.

Para carregar o arquivo de exemplo após extraí-lo:

1. No Azure Data Studio, *clique com o botão direito do mouse* no novo diretório criado. 
2. Clique em **Carregar arquivos**.

![exemplo de arquivo CSV no HDFS](media/data-virtualization/100-csv-sample-file-hdfs.png)

O Azure Data Studio carrega os arquivos no HDFS no Cluster de Big Data.

## <a name="create-the-storage-pool-external-data-source-in-your-target-database"></a>Criar a fonte de dados externa do pool de armazenamento no banco de dados de destino

A fonte de dados externa do pool de armazenamento não é criada em um banco de dados por padrão no Cluster de Big Data. Antes de criar a tabela externa, crie a fonte de dados externa **SqlStoragePool** padrão no banco de dados de destino com a consulta Transact-SQL a seguir. Primeiro, altere o contexto da consulta para o banco de dados de destino.

```sql
-- Create the default storage pool source for SQL Big Data Cluster
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://controller-svc/default');
```

## <a name="create-the-external-table"></a>Criar a tabela externa

No ADS, clique com o botão direito do mouse no arquivo CSV e selecione **Criar Tabela Externa do Arquivo CSV** no menu de contexto. Você também poderá criar tabelas externas de arquivos CSV de um diretório no HDFS se os arquivos no diretório seguirem o mesmo esquema. Isso permitirá a virtualização dos dados no nível do diretório sem necessidade de processar arquivos individuais e obter um conjunto de resultados unido sobre os dados combinados. O Azure Data Studio orienta você nas etapas de criação da tabela externa.

Especifique o banco de dados, a fonte de dados, um nome de tabela, o esquema e o nome do formato de arquivo externo da tabela.

Clique em **Próximo**.

## <a name="preview-data"></a>Visualizar Dados

O Azure Data Studio fornece uma visualização dos dados importados.

![Captura de tela mostrando a janela Criar Tabela Externa de CSV com uma visualização dos dados importados.](media/data-virtualization/130-csv-preview-data.png)

Quando terminar de ver a versão prévia, clique em **Avançar** para continuar

## <a name="modify-columns"></a>Modificar Colunas

Na próxima janela, você poderá modificar as colunas da tabela externa que pretende criar. É possível alterar o nome da coluna, alterar o tipo de dados e permitir linhas anuláveis. 

![Captura de tela da janela Criar Tabela Externa de CSV mostrando a Etapa 3 Modificar Colunas.](media/data-virtualization/140-csv-modify-columns.png)

Depois de verificar as colunas de destino, clique em **Avançar**.

## <a name="summary"></a>Resumo

Essa etapa fornece um resumo das suas seleções. Ela fornece o nome do SQL Server, o nome do banco de dados, o nome da tabela, o esquema da tabela e as informações da tabela externa. Nesta etapa, você tem a opção de gerar um script ou criar uma tabela. **Gerar Script** cria um script no T-SQL para criar a fonte de dados externa. **Criar Tabela** cria a fonte de dados externa.

![Tela de resumo](media/data-virtualization/150-csv-virtualize-data-summary.png)

Se você clicar em **Criar Tabela** , o SQL Server criará a tabela externa no banco de dados de destino.

Se você clicar em **Gerar Script** , o Azure Data Studio criará a consulta T-SQL para criar a tabela externa.

Depois de criada, a tabela pode ser consultada diretamente usando o T-SQL na instância do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o Cluster de Big Data do SQL Server e cenários relacionados, consulte [O que é o Cluster de Big Data do SQL Server?](big-data-cluster-overview.md).
