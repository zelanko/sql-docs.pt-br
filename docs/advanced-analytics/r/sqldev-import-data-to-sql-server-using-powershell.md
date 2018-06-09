---
title: Ambiente tutorial do R preparar lição 2 usando o PowerShell (aprendizado de máquina do SQL Server) | Microsoft Docs
description: Tutorial mostra como inserir R no SQL Server procedimentos armazenados e funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1280d7c82d48c8ed596271cd7a73fa13ec1664c7
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249739"
---
# <a name="lesson-2-set-up-the-tutorial-environment-using-powershell"></a>Lição 2: Configurar o ambiente de tutorial usando o PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial para desenvolvedores em SQL sobre como usar o R no SQL Server.

Nesta etapa, você executará um script do PowerShell para criar os objetos de banco de dados necessários para o passo a passo. O script cria e carrega um banco de dados usando dados de exemplo obtidos na etapa anterior. Ele também cria funções e procedimentos armazenados usados em todo o tutorial.

## <a name="create-and-load-database-objects"></a>Criar e carregar objetos de banco de dados

Entre os arquivos baixados, você deverá ver um script do PowerShell (`RunSQL_SQL_Walkthrough.ps1`) que prepara o ambiente para o passo a passo. As ações executadas pelo script incluem:

- Instale o SQL Native Client e utilitários de linha de comando do SQL, se ainda não estiver instalado. Esses utilitários são necessários para o carregamento em massa dos dados no banco de dados com o **bcp**.

- Criar um banco de dados e tabelas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância e inserção em massa dados originados de um arquivo. csv.

- Crie várias funções SQL e procedimentos armazenados.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>Modifique o script para usar uma identidade confiável do Windows

Por padrão, o script supõe um logon de usuário de banco de dados do SQL Server e uma senha. Se você estiver db_owner em sua conta de usuário do Windows, você pode usar a identidade do Windows para criar os objetos. Para fazer isso, abra `RunSQL_SQL_Walkthrough.ps1` em um editor de código e acrescente **`-T`** para bcp em massa inserir o comando (linha 238):

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>Execute o script para criar objetos

Abra um prompt de comando do PowerShell como administrador e execute o comando a seguir.
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
Você será solicitado a inserir as informações a seguir:

- Instância de servidor em que [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] foi instalado. Em uma instância padrão, isso pode ser tão simple quanto o nome do computador.

- Nome do banco de dados. Para este tutorial, os scripts presumem `TaxiNYC_Sample`.

- Nome de usuário e senha do usuário. Insira um logon de banco de dados do SQL Server para esses valores. Como alternativa, se você tiver modificado o script para aceitar uma identidade confiável do Windows, pressione Enter para manter esses valores em branco. A identidade do Windows é usada na conexão.

- Nome de arquivo totalmente qualificado para os dados de exemplo baixados na lição anterior. Por exemplo: `C:\tempRSQL\nyctaxi1pct.csv`

Depois que você fornecer esses valores, o script será executado imediatamente. Durante a execução do script, todos os nomes de espaço reservado no [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts são atualizados para usar as entradas que você fornecer.

## <a name="review-database-objects"></a>Examine os objetos de banco de dados
   
Terminada a execução do script, confirme que os objetos de banco de dados existem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você deve ver o banco de dados, tabelas, funções e procedimentos armazenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> Se os objetos de banco de dados já existirem, não será possível criá-los novamente.
>   
> Se a tabela já existir, os dados serão acrescentados, não substituídos. Portanto, lembre-se de remover todos os objetos existentes antes de executar o script.

## <a name="objects-used-in-this-tutorial"></a>Objetos usados neste tutorial

A tabela a seguir resume os objetos criados nesta lição. Embora somente executar um script do PowerShell (`RunSQL_SQL_Walkthrough.ps1`), esse script chama outros scripts SQL para criar os objetos no banco de dados. Os scripts usados para criar cada objeto são mencionados na descrição.

|**Nome do objeto**|**Tipo de objeto**|**Descrição**|
|----------|------------------------|---------------|
|**TaxiNYC_Sample** | Banco de Dados |Criado pelo script de criação-db-tb-upload-data.sql. Cria um banco de dados e duas tabelas:<br /><br />tabela dbo.nyctaxi_sample: contém o conjunto de dados principal NYC táxi. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta. O exemplo de % 1 do conjunto de dados NYC táxi é inserido nessa tabela.<br /><br />tabela dbo.nyc_taxi_models: usado para manter o modelo treinado análise avançada.|
|**fnCalculateDistance** |função de valor escalar | Criado pelo script fnCalculateDistance.sql. Calcula a distância direta entre os locais de retirada e redução. Essa função é usada na [criar recursos de dados](../tutorials/sqldev-create-data-features-using-t-sql.md), [treinar e salvar um modelo de](sqldev-train-and-save-a-model-using-t-sql.md) e [Operacionalizar o modelo R](../tutorials/sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |função com valor de tabela | Criado pelo script fnEngineerFeatures.sql. Cria novos recursos de dados de treinamento do modelo. Essa função é usada na [criar recursos de dados](../tutorials/sqldev-create-data-features-using-t-sql.md) e [Operacionalizar o modelo R](../tutorials/sqldev-operationalize-the-model.md).|
|**PlotHistogram** |procedimento armazenado | Criado pelo script PlotHistogram.sql. Chama uma função de R para plotar o histograma de uma variável e, em seguida, retorna o gráfico como um objeto binário. Esse procedimento armazenado é usado em [explorar e visualizar dados](../tutorials/sqldev-explore-and-visualize-the-data.md).|
|**PlotInOutputFiles** |procedimento armazenado| Criado pelo script PlotInOutputFiles.sql. Cria um gráfico usando uma função de R e, em seguida, salva a saída como um arquivo PDF local. Esse procedimento armazenado é usado em [explorar e visualizar dados](../tutorials/sqldev-explore-and-visualize-the-data.md).|
|**PersistModel** |procedimento armazenado | Criado pelo script PersistModel.sql. Usa um modelo que tenha sido serializado em um tipo de dados varbinary e grava-o para a tabela especificada. |
|**PredictTip**  |procedimento armazenado |Criado pelo script PredictTip.sql. Chama o modelo treinado para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada. Esse procedimento armazenado é usado em [Operacionalizar o modelo R](../tutorials/sqldev-operationalize-the-model.md).|
|**PredictTipSingleMode**  |procedimento armazenado| Criado pelo script PredictTipSingleMode.sql. Chama o modelo treinado para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação. Esse procedimento armazenado é usado em [Operacionalizar o modelo R](../tutorials/sqldev-operationalize-the-model.md).|
|**TrainTipPredictionModel**  |procedimento armazenado|Criado pelo script TrainTipPredictionModel.sql. Treina um modelo de regressão logística chamando um pacote R. O modelo prevê o valor da coluna tipped e é treinado usando uma seleção aleatória de 70% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models. Esse procedimento armazenado é usado em [treinar e salvar um modelo](sqldev-train-and-save-a-model-using-t-sql.md).|

## <a name="next-lesson"></a>Próxima lição

[Lição 3: Explorar e visualizar os dados](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 1: Baixar os dados de exemplo](../tutorials/sqldev-download-the-sample-data.md)
