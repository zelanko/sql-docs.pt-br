---
title: Etapa 2 importar dados para o SQL Server usando o PowerShell | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f8b90a18c0cdce9c4c2c73db4b599e488570f018
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461862"
---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>Etapa 2: Importar dados para o SQL Server usando o PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial [análise de Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você executa um dos scripts baixados para criar os objetos de banco de dados necessários para o passo a passo. O script também cria vários procedimentos armazenados e carrega os dados de exemplo para uma tabela no banco de dados especificado.

## <a name="create-database-objects-and-load-data"></a>Criar objetos de banco de dados e carregar dados

Entre os arquivos baixados, você deverá ver um script do PowerShell, `RunSQL_SQL_Walkthrough.ps1`. O objetivo desse script é preparar o ambiente para o passo a passo.

O script executa estas ações:

- Instala o SQL Native Client e utilitários de linha de comando do SQL, se ainda não estiver instalado. Esses utilitários são necessários para o carregamento em massa dos dados no banco de dados com o **bcp**.

- Cria um banco de dados e uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância e inserções em massa os dados na tabela.

- Cria várias funções SQL e procedimentos armazenados.

Se você tiver problemas, você pode usar o script como uma referência para executar as etapas manualmente.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>Modifique o script para usar uma identidade confiável do Windows

Por padrão, o script pressupõe um logon de usuário de banco de dados do SQL Server e uma senha. Se você estiver db_owner em sua conta de usuário do Windows, você pode usar sua identidade do Windows para criar os objetos. Para fazer isso, abra `RunSQL_SQL_Walkthrough.ps1` em um editor de código para acrescentar **`-T`** para o bcp comando inserção em massa:

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script"></a>Execute o script

1. Abra um prompt de comando do PowerShell como administrador. Se você não ainda estiver na pasta criada na etapa anterior, navegue até a pasta e, em seguida, execute o seguinte comando:
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```

2. O script solicitará as informações a seguir:

    - O nome ou endereço de um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instância em que os serviços do Machine Learning com o Python foi instalado.
    - O nome de usuário e a senha de uma conta na instância. A conta usada deve ter a capacidade de criar bancos de dados, criar tabelas e procedimentos armazenados e carregar dados para tabelas em massa. 
    - Se você não fornecer o nome de usuário e senha, sua identidade de Windows é usada para entrar no SQL Server.
    - O caminho e o nome do arquivo de dados de exemplo que você acabou de baixar. Por exemplo, `C:\temp\pysql\nyctaxi1pct.csv`

    > [!NOTE]
    > Para carregar os dados com êxito, o xmlrw. dll de biblioteca deve ser na mesma pasta que bcp.exe.

3. O script também modifica o [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts que você baixou anteriormente e substitui os espaços reservados com o nome do banco de dados e o usuário nome que você fornecem.
  
4. Quando o script for concluído, faça logon na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância usando o logon especificado, para verificar se o banco de dados, tabelas, funções e procedimentos armazenados foram criados. A imagem a seguir mostra os objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

    ![Procurar tabelas no SSMS](media/sqldev-python-browsetables1.png "exibir tabelas no SSMS")

    > [!NOTE]
    > Se os objetos de banco de dados já existiram, não pode ser criados novamente.
    > 
    > Se uma tabela existente de mesmo nome e esquema for encontrado, os dados serão acrescentados, não substituídos. Portanto, certifique-se descartar ou truncar tabelas existentes antes de executar o script.

## <a name="list-of-stored-procedures-and-functions"></a>Lista de procedimentos armazenados e funções

Os seguintes objetos do SQL Server são criados pelo script:

|**Nome do arquivo de script SQL**|**Função**|
|------|------|
|create-db-tb-upload-data.sql|Cria um banco de dados e duas tabelas:<br /><br />nyctaxi_sample: contém o conjunto de dados principal Táxi de Nova York. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta. A amostra de 1% do conjunto de dados Táxi de Nova York será inserida nesta tabela.<br /><br />nyc_taxi_models: usado para persistir o modelo treinado de análise avançada.|
|fnCalculateDistance.sql|Cria uma função de valor escalar que calcula a distância direta entre os locais de embarque e desembarque de passageiros|
|fnEngineerFeatures.sql|Cria uma função com valor de tabela que cria novos recursos de dados para treinamento do modelo|
|TrainingTestingSplit.sql|Dividir os dados na tabela nyctaxi_sample em duas partes: nyctaxi_sample_training e nyctaxi_sample_testing.|
|PredictTipSciKitPy.sql|Cria um procedimento armazenado que chama o modelo treinado (scikit-Saiba mais) para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada.|
|PredictTipRxPy.sql|Cria um procedimento armazenado que chama o modelo treinado (revoscalepy) para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada.|
|PredictTipSingleModeSciKitPy.sql|Cria um procedimento armazenado que chama o modelo treinado (scikit-Saiba mais) para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação.|
|PredictTipSingleModeRxPy.sql|Cria um procedimento armazenado que chama o modelo treinado (revoscalepy) para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação.|

A última parte deste passo a passo, você cria esses procedimentos armazenados adicionais:
    
|**Nome do arquivo de script SQL**|**Função**|
|------|------|
|SerializePlots.sql|Cria um procedimento armazenado para exploração de dados. Esse procedimento armazenado cria um gráfico usando o Python e, em seguida, serializar os objetos de gráfico.|
|TrainTipPredictionModelSciKitPy.sql|Cria um procedimento armazenado que treina um modelo de regressão logística (scikit-Saiba mais). O modelo prevê o valor da coluna tipped e é treinado usando um selecionado aleatoriamente 60% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models.|
|TrainTipPredictionModelRxPy.sql|Cria um procedimento armazenado que treina um modelo de regressão logística (revoscalepy). O modelo prevê o valor da coluna tipped e é treinado usando um selecionado aleatoriamente 60% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models.|

## <a name="next-step"></a>Próxima etapa

[Etapa 3: Explorar e visualizar os dados](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>Etapa anterior

[Etapa 1: Baixar os dados de exemplo](demo-data-nyctaxi-in-sql.md)

