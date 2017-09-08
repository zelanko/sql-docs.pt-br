---
title: 'Etapa 2: Importar dados para o SQL Server usando PowerShell | Microsoft Docs'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-vnext-ctp2
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62a06d6c442428132f84b3f8e5a665e872a8d361
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>Etapa 2: Importar dados para o SQL Server usando o PowerShell

Nesta etapa, você vai executar um dos scripts baixados, para criar os objetos de banco de dados necessários para o passo a passo. O script também cria a maioria dos procedimentos armazenados que serão usados e carrega os dados de exemplo em uma tabela no banco de dados especificado.

## <a name="create-sql-objects-and-data"></a>Criar dados e objetos do SQL

Entre os arquivos baixados, você deverá ver um script do PowerShell. Para preparar o ambiente para o passo a passo, você vai executar este script.  O script executa estas ações:

- Instala o SQL Native Client e utilitários de linha de comando do SQL, se ainda não estiver instalado. Esses utilitários são necessários para o carregamento em massa dos dados no banco de dados com o **bcp**.

- Cria um banco de dados e uma tabela de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância e inserções em massa os dados na tabela.

- Cria várias funções SQL e procedimentos armazenados.

### <a name="run-the-script"></a>Execute o script

1. Abra um prompt de comando do PowerShell como administrador e execute o comando a seguir.
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  

    Será solicitado que você insira as seguintes informações:
    - O nome ou endereço de um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instância em que os serviços com Python de aprendizado de máquina tiver sido instalada
    - O nome de usuário e a senha de uma conta na instância. A conta usada deve ter a capacidade de criar bancos de dados, criar tabelas e procedimentos armazenados, bem como carregar dados em tabelas. Se você não fornecer o nome de usuário e senha, a identidade do Windows é usada para entrar no SQL Server.
    - O caminho e o nome do arquivo de dados de exemplo que você acabou de baixar. Por exemplo, `C:\tempRSQL\nyctaxi1pct.csv`

    > [!NOTE]
    > Certifique-se de que seu xmlrw.dll está na mesma pasta que o bcp.exe. Caso contrário, copie-o em.

2.  Como parte dessa etapa, todos os scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] também são modificados para substituir os espaços reservados pelos nomes do banco de dados e de usuário fornecidos como entradas de script.
  
3. Reserve um minuto para examinar os procedimentos armazenados e as funções criadas pelo script.
     
    |**Nome do arquivo de script SQL**|**Função**|
    |------|------|
    |create-db-tb-upload-data.sql|Cria um banco de dados e duas tabelas:<br /><br />nyctaxi_sample: contém o conjunto de dados principal Táxi de Nova York. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta. A amostra de 1% do conjunto de dados Táxi de Nova York será inserida nesta tabela.<br /><br />nyc_taxi_models: usado para persistir o modelo treinado de análise avançada.|
    |fnCalculateDistance.sql|Cria uma função de valor escalar que calcula a distância direta entre os locais de embarque e desembarque de passageiros|
    |fnEngineerFeatures.sql|Cria uma função com valor de tabela que cria novos recursos de dados para treinamento do modelo|
    |TrainingTestingSplit.sql|Dividir os dados na tabela nyctaxi_sample em duas partes: nyctaxi_sample_training e nyctaxi_sample_testing.|
    |PredictTipSciKitPy.sql|Cria um procedimento armazenado que chama o modelo treinado (scikit-Saiba) para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada.|
    |PredictTipRxPy.sql|Cria um procedimento armazenado que chama o modelo treinado (revoscalepy) para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada.|
    |PredictTipSingleModeSciKitPy.sql|Cria um procedimento armazenado que chama o modelo treinado (scikit-Saiba) para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação.|
    |PredictTipSingleModeRxPy.sql|Cria um procedimento armazenado que chama o modelo treinado (revoscalepy) para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação.|
  
4. Você criará alguns procedimentos armazenados adicionais na última parte deste passo a passo:
    
    |**Nome do arquivo de script SQL**|**Função**|
    |------|------|
    |SerializePlots.sql|Cria um procedimento armazenado para exploração de dados. Esse procedimento armazenado cria um gráfico usando Python e, em seguida, serializar os objetos de gráfico.|
    |TrainTipPredictionModelSciKitPy.sql|Cria um procedimento armazenado que treina um modelo de regressão logística (scikit-Saiba). O modelo prevê o valor da coluna Oblíquo e é treinado usando um selecionado aleatoriamente de 60% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models.|
    |TrainTipPredictionModelRxPy.sql|Cria um procedimento armazenado que treina um modelo de regressão logística (revoscalepy). O modelo prevê o valor da coluna Oblíquo e é treinado usando um selecionado aleatoriamente de 60% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models.|
  
3. Faça logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o logon especificado para verificar se você pode ver o banco de dados, as tabelas, as funções e os procedimentos armazenados criados.

    ![Procurar tabelas no SSMS](media/sqldev-python-browsetables1.png "exibir tabelas no SSMS")

    > [!NOTE]
    > Se os objetos de banco de dados já existirem, não será possível criá-los novamente. Se a tabela já existir, os dados serão acrescentados, não substituídos. Portanto, lembre-se de remover todos os objetos existentes antes de executar o script.
    > Siga as instruções [aqui](https://docs.microsoft.com/en-us/sql/advanced-analytics/r/set-up-sql-server-r-services-in-database#bkmk_enableFeature) para habilitar os serviços de script externo.
    


## <a name="next-step"></a>Próxima etapa

[Etapa 3: Explorar e visualizar os dados](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>Etapa anterior

[Etapa 1: Baixar os dados de exemplo](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>Consulte também

[Serviços de aprendizado de máquina com Python](../python/sql-server-python-services.md)



