---
title: O que&#39;s novos no SQL Server Machine Learning Services | Microsoft Docs
description: Lançamentos de novos recursos para cada versão do SQL Server 2016 R Services, Microsoft R Server, serviços de aprendizado de máquina do SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8d3dc4c730ea9c7c9ba0126a50ed4bb8129efc9c
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152576"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>O que há de novo nos serviços do SQL Server Machine Learning 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Recursos de aprendizado de máquina são adicionados ao SQL Server em cada versão enquanto continuamos a expandir, estender e aprofundar a integração entre a plataforma de dados e de ciência de dados, análise e você deseja implementar sobre seus dados de aprendizado supervisionado. 

## <a name="new-in-sql-server-2017"></a>Novo no SQL Server 2017

Essa versão adiciona [suporte do Python e algoritmos de aprendizado de máquina de líderes do setor](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Renomeado para refletir o novo escopo, o SQL Server 2017 marca a introdução de [serviços do SQL Server Machine Learning (no banco de dados)](what-is-sql-server-machine-learning.md), com suporte de idioma para o Python e R. 

Esta versão também introduzida [SQL Server Machine Learning Server (autônomo)](r/r-server-standalone.md)totalmente independente do SQL Server, para cargas de trabalho R e Python que você deseja executar em um sistema dedicado. Com o servidor autônomo, você pode distribuir e dimensionar soluções R ou Python sem usar o SQL Server.

### <a name="python-integration-for-in-database-analytics"></a>Integração do Python para análise no banco de dados

Agora há suporte para a integração do T-SQL e Python por meio de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimento armazenado do sistema. Você pode chamar qualquer código do Python usando esse procedimento armazenado. Código é executado em uma arquitetura dual segura que permite a implantação de empresarial de scripts, que pode ser chamados de um aplicativo usando um procedimento armazenado simples e modelos em Python. São obtidos ganhos de desempenho adicionais pela transmissão de dados do SQL para processos de Python e a paralelização de anel MPI.

Você pode usar o T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) função para realizar [pontuação nativa](sql-native-scoring.md) em um modelo previamente treinado que tenha sido previamente salva no formato binário solicitado.

### <a name="python-libraries"></a>Bibliotecas do Python

| Pacote | Description |
|---------|-------------|
[**revoscalepy**](python/what-is-revoscalepy.md)| Equivalente de Python do RevoScaleR. Você pode criar modelos em Python para Regressão logística e linear, árvores de decisão, árvores aumentadas e florestas aleatórias, todos os paralelizáveis e sejam capazes de está sendo executado em contextos de computação remota. Este pacote dá suporte ao uso de várias fontes de dados e contextos de computação remota. O desenvolvedor ou cientista de dados pode executar código Python em um servidor SQL remoto, para explorar dados ou criar modelos sem movimentação de dados. |
|[**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) |Python equivalente do pacote MicrosoftML R. |

### <a name="r-libraries"></a>Bibliotecas do R

| Pacote | Description |
|---------|-------------|
| [**MicrosoftML (R)**](using-the-microsoftml-package.md) | Algoritmos de aprendizado de máquina de última geração e transformação de dados que pode ser remoto em escala ou execução em contextos de computação. Algoritmos incluem personalizáveis redes neurais profundas, árvores de decisão rápidas e florestas de decisão, regressão linear e regressão logística.  |
| [**Gerenciamento de pacotes de R**](r/install-additional-r-packages-on-sql-server.md) | Aperfeiçoado nesta versão, com os seguintes destaques: funções para ajudar a gerenciar pacotes e atribuir permissões para instalar os pacotes, o DBA [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução no T-SQL para ajudar os DBAs gerenciar pacotes sem necessidade de conhecer o R e um conjunto avançado de funções do R no [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) ajudar a instalar, remover ou listar pacotes pertencentes aos usuários. |

### <a name="pre-trained-models"></a>Modelos previamente treinados

[**Modelos previamente treinados** ](install/sql-pretrained-models-install.md) estão disponíveis para Python e R. usam esses modelos para reconhecimento de imagem e análise de sentimento negativo positivo, para gerar previsões em seus próprios dados. 


## <a name="new-in-sql-server-2016"></a>Novo no SQL Server 2016

Esta versão introduzida recursos de machine learning no SQL Server por meio **SQL Server 2016 R Services**, um mecanismo de análise no banco de dados para o script de R de processamento nos dados residentes em uma instância do mecanismo de banco de dados.

Além disso, **SQL Server 2016 R Server (autônomo)** foi lançado como uma maneira de instalar o R Server em um servidor Windows. Instalação do SQL Server fornecidas inicialmente, a única maneira de instalar o R Server para Windows. Em versões posteriores, os desenvolvedores e cientistas de dados que desejava R Server no Windows pode usar o instalador autônomo do outro para alcançar o mesmo objetivo. O servidor autônomo no SQL Server é funcionalmente equivalente ao produto de servidor autônomo, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

| Versão |Atualização do recurso |
|---------|----------------|
| Adições de CU | [**Pontuação em tempo real** ](real-time-scoring.md) se baseia em bibliotecas nativas do C++ para ler um modelo armazenado em um formato binário otimizado e, em seguida, gerar previsões sem a necessidade de chamar o tempo de execução de R. Isso torna muito mais rapidamente as operações de pontuação. Com a pontuação em tempo real, você pode executar um procedimento armazenado ou executar pontuação em tempo real de código R. Pontuação em tempo real também está disponível para o SQL Server 2016, se a instância for atualizada para a versão mais recente do [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versão inicial | [**Integração do R para análise no banco de dados**](r/sql-server-r-services.md). <br/><br/> Pacotes de R para R chamada de funções no T-SQL e vice-versa. Funções RevoScaleR fornecem análise de R em grande escala, fragmentando dados em partes componentes, coordenação e gerenciamento distribuído de processamento e agregar resultados. No SQL Server 2016 R Services (no banco de dados), o mecanismo de RevoScaleR é integrado com uma instância do mecanismo de banco de dados, brining juntos no mesmo contexto de processamento de análise e dados. <br/><br/>Integração do T-SQL e R por meio [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Você pode chamar qualquer código R usando esse procedimento armazenado. Essa infraestrutura segura permite a implantação de empresarial de modelos Rn e scripts que podem ser chamados a partir de um aplicativo usando um procedimento armazenado simples. São obtidos ganhos de desempenho adicionais pela transmissão de dados do SQL para processos de R e a paralelização de anel MPI. <br/><br/>Você pode usar o T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) função para realizar [pontuação nativa](sql-native-scoring.md) em um modelo previamente treinado que tenha sido previamente salva no formato binário solicitado.|

## <a name="linux-support-roadmap"></a>Roteiro de suporte do Linux

Aprendizado de máquina usando o R ou Python no banco de dados no momento, não há suporte no SQL Server no Linux. Procure anúncios em uma versão posterior.

No entanto, no Linux você pode realizar [pontuação nativa](sql-native-scoring.md) usando a função PREVER o T-SQL. Pontuação nativa permite a pontuação de um modelo pré-treinado muito rápido, sem chamar ou até mesmo exigir um tempo de execução de R. Isso significa que você pode usar o SQL Server no Linux para gerar previsões com muita rapidez para atender a aplicativos cliente.

<a name="azure-sql-database-roadmap"></a>

## <a name="azure-sql-database-roadmap"></a>Roteiro de banco de dados SQL do Azure

Há suporte limitado para R no banco de dados SQL: disponível apenas no Centro-Oeste dos EUA, em serviços criados na camada Premium. Cobertura expandida, incluindo o suporte do Python, é provável a seguir em uma versão futura. No entanto, não há nenhuma data de lançamento projetada no momento.  

## <a name="next-steps"></a>Próximas etapas

+ [Instalar serviços de Machine Learning do SQL Server 2017 (no banco de dados)](install/sql-machine-learning-services-windows-install.md)
+ [Exemplos e tutoriais de aprendizado de máquina](tutorials/machine-learning-services-tutorials.md)
