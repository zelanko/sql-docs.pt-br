---
title: Baixe dados de demonstração de táxi de NYC e scripts para embedded R e Python (aprendizado de máquina do SQL Server) | Microsoft Docs
description: Instruções para baixar dados de exemplo de táxi de Nova York e criação de um banco de dados. Dados são usados nos tutoriais do SQL Server que mostra como inserir o R e Python no SQL Server procedimentos armazenados e funções T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6d5030287e7ad526816f89fd23b13fedae070c56
ms.sourcegitcommit: 320958d0f55b6974abf46f8a04f7a020ff86a0ae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703599"
---
# <a name="nyc-taxi-demo-data-for-sql-server"></a>Dados de demonstração de táxi de Nova York para o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo prepara o sistema para tutoriais sobre como usar o R e Python para análise no banco de dados no SQL Server.

Neste exercício, você baixará os dados de exemplo, um script do PowerShell para preparar o ambiente e [!INCLUDE[tsql](../../includes/tsql-md.md)] usados em vários tutoriais de arquivos de script. Quando tiver terminado, uma **NYCTaxi_Sample** banco de dados está disponível em sua instância local, fornecendo dados de demonstração para o aprendizado prático. 

## <a name="prerequisites"></a>Prerequisites

Você precisará de uma conexão de internet, o PowerShell e direitos administrativos locais no computador. Você deve ter [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou outra ferramenta para verificar a criação do objeto.

## <a name="download-nyc-taxi-demo-data-and-scripts-from-github"></a>Baixe dados de demonstração de táxi de NYC e scripts do Github

1.  Abra um console de comando do Windows PowerShell.
  
    Use o **executar como administrador** opção de criar o diretório de destino ou para gravar arquivos para o destino especificado.
  
2.  Execute os comandos do PowerShell a seguir, alterando o valor do parâmetro *DestDir* para um diretório local. O padrão que usamos aqui é **TempRSQL**.
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    Se a pasta especificada em *DestDir* não existir, ela será criada pelo script do PowerShell.
  
    > [!TIP]
    > Se você receber um erro, você pode definir temporariamente a política de execução de scripts do PowerShell para **irrestrito** somente para este passo a passo usando o argumento Bypass e as alterações à sessão atual de escopo.
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > A execução desse comando não resulta em uma alteração de configuração.
  
    Dependendo da conexão com a Internet, o download poderá demorar um pouco.
  
3.  Quando todos os arquivos tiverem sido baixados, o script do PowerShell é aberto para o *DestDir* pasta. No prompt de comando do PowerShell, execute o comando a seguir e examine os arquivos baixados.
  
    ```
    ls
    ```
  
    **Resultados:**
  
    ![lista de arquivos baixados pelo script do PowerShell](media/rsql-devtut-filelist.png "lista de arquivos baixados pelo script do PowerShell")

## <a name="create-nyctaxisample-database"></a>Criar banco de dados NYCTaxi_Sample

Entre os arquivos baixados, você deverá ver um script do PowerShell (**RunSQL_SQL_Walkthrough.ps1**) que cria um banco de dados e carrega os dados em massa. As ações executadas pelo script incluem:

+ Instala o SQL Native Client e utilitários de linha de comando do SQL, se ainda não estiver instalado. Esses utilitários são necessários para o carregamento em massa dos dados no banco de dados com o **bcp**.

+ Criar um banco de dados e tabelas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da instância e inserção em massa dados originados de um arquivo. csv.

+ Crie várias funções SQL e procedimentos armazenados usados em vários tutoriais.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>Modifique o script para usar uma identidade confiável do Windows

Por padrão, o script pressupõe um logon de usuário de banco de dados do SQL Server e uma senha. Se você estiver db_owner em sua conta de usuário do Windows, você pode usar sua identidade do Windows para criar os objetos. Para fazer isso, abra `RunSQL_SQL_Walkthrough.ps1` em um editor de código e acrescente **`-T`** para o bcp (linha 238) do comando inserção em massa:

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>Execute o script para criar objetos

Usando um prompt de comando do PowerShell de administrador no C:\tempRSQL, execute o comando a seguir.
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
Você será solicitado a inserir as informações a seguir:

- Instância de servidor em que [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] foi instalado. Em uma instância padrão, isso pode ser tão simple quanto o nome do computador.

- Nome do banco de dados. Para este tutorial, os scripts presumem `NYCTaxi_Sample`.

- Nome de usuário e senha do usuário. Insira um logon de banco de dados do SQL Server para obter esses valores. Como alternativa, se você tiver modificado o script para aceitar uma identidade confiável do Windows, pressione Enter para deixar esses valores em branco. Sua identidade de Windows é usada em que a conexão.

- Nome de arquivo totalmente qualificado para os dados de exemplo baixados na lição anterior. Por exemplo: `C:\tempRSQL\nyctaxi1pct.csv`

Depois de fornecer esses valores, o script é executado imediatamente. Durante a execução do script, todos os nomes de espaço reservado no [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts foram atualizados para usar entradas fornecidas por você.

## <a name="review-database-objects"></a>Examine os objetos de banco de dados
   
Quando a execução do script for concluída, confirme se os objetos de banco de dados existem na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você deve ver o banco de dados, tabelas, funções e procedimentos armazenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> Se os objetos de banco de dados já existirem, não será possível criá-los novamente.
>   
> Se a tabela já existir, os dados serão acrescentados, não substituídos. Portanto, lembre-se de remover todos os objetos existentes antes de executar o script.

### <a name="objects-in-nyctaxisample-database"></a>Objetos no banco de dados NYCTaxi_Sample

A tabela a seguir resume os objetos criados no banco de dados de demonstração de táxi de Nova York. Embora você só executar um script do PowerShell (`RunSQL_SQL_Walkthrough.ps1`), esse script chama outros scripts SQL por sua vez para criar os objetos no banco de dados. Scripts usados para criar cada objeto são mencionadas na descrição.

|**Nome do objeto**|**Tipo de objeto**|**Descrição**|
|----------|------------------------|---------------|
|**TaxiNYC_Sample** | Banco de Dados |Criado pelo script create-db-tb-upload-data.sql. Cria um banco de dados e duas tabelas:<br /><br />tabela nyctaxi_sample: contém o conjunto de dados principal táxi de Nova York. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta. A amostra de 1% do conjunto de dados de táxi de Nova York será inserida nesta tabela.<br /><br />tabela dbo.nyc_taxi_models: usado para persistir o modelo treinado de análise avançada.|
|**fnCalculateDistance** |função de valor escalar | Criado pelo script fnCalculateDistance.sql. Calcula a distância direta entre os locais de embarque e desembarque de passageiros. Essa função é usada na [criar recursos de dados](sqldev-create-data-features-using-t-sql.md), [treinar e salvar um modelo](../r/sqldev-train-and-save-a-model-using-t-sql.md) e [Operacionalizar o modelo de R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |função com valor de tabela | Criado pelo script fnEngineerFeatures.sql. Cria novos recursos de dados para treinamento do modelo. Essa função é usada na [criar recursos de dados](sqldev-create-data-features-using-t-sql.md) e [Operacionalizar o modelo de R](sqldev-operationalize-the-model.md).|
|**PlotHistogram** |procedimento armazenado | Criado pelo script PlotHistogram.sql. Chama uma função do R para plotar o histograma de uma variável e, em seguida, retorna a plotagem como um objeto binário. Esse procedimento armazenado é usado em [explorar e visualizar dados](sqldev-explore-and-visualize-the-data.md).|
|**PlotInOutputFiles** |procedimento armazenado| Criado pelo script PlotInOutputFiles.sql. Cria um gráfico usando uma função do R e, em seguida, salva a saída como um arquivo PDF local. Esse procedimento armazenado é usado em [explorar e visualizar dados](sqldev-explore-and-visualize-the-data.md).|
|**PersistModel** |procedimento armazenado | Criado pelo script PersistModel.sql. Usa um modelo que foi serializado em um tipo de dados varbinary e grava-o para a tabela especificada. |
|**PredictTip**  |procedimento armazenado |Criado pelo script PredictTip.sql. Chama o modelo treinado para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada. Esse procedimento armazenado é usado em [Operacionalizar o modelo de R](sqldev-operationalize-the-model.md).|
|**PredictTipSingleMode**  |procedimento armazenado| Criado pelo script PredictTipSingleMode.sql. Chama o modelo treinado para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação. Esse procedimento armazenado é usado em [Operacionalizar o modelo de R](sqldev-operationalize-the-model.md).|
|**TrainTipPredictionModel**  |procedimento armazenado|Criado pelo script TrainTipPredictionModel.sql. Treina um modelo de regressão logística chamando um pacote R. O modelo prevê o valor da coluna tipped e é treinado usando uma seleção aleatória de 70% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models. Esse procedimento armazenado é usado em [treinar e salvar um modelo](../r/sqldev-train-and-save-a-model-using-t-sql.md).|

## <a name="next-steps"></a>Próximas etapas

Dados de exemplo de táxi de NYC agora estão disponíveis para o aprendizado prático.

+ [Aprenda a análise no banco de dados usando o R no SQL Server](sqldev-in-database-r-for-sql-developers.md)