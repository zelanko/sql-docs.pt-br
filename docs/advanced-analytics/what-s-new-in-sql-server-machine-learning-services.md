---
title: O que&#39;s novos no SQL Server Machine Learning Services | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf56d52823727609d713639d534e277be57caaef
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174803"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>O que há de novo nos serviços do SQL Server Machine Learning 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Recursos de aprendizado de máquina são adicionados ao SQL Server em cada versão enquanto continuamos a expandir, estender e aprofundar a integração entre a plataforma de dados e de ciência de dados, análise e você deseja implementar sobre seus dados de aprendizado supervisionado. 

## <a name="new-in-sql-server-2017"></a>Novo no SQL Server 2017

Esta versão adicionado o suporte do Python e algoritmos de aprendizado de máquina de líderes do setor. Renomeado para refletir o novo escopo, o SQL Server 2017 marcado a introdução da **serviços do SQL Server Machine Learning (no banco de dados)**, com suporte de idioma para o Python e R. 

Esta versão também introduzida **SQL Server Machine Learning Server (autônomo)** totalmente independente do SQL Server, para cargas de trabalho R e Python que você deseja executar em um sistema dedicado. Com o servidor autônomo, você pode distribuir e dimensionar soluções R ou Python sem usar o SQL Server.

| Versão | Atualização do recurso |
|---------|----------------|
| CU 6 | Correções de bugs e atualização de pacotes, mas nenhum novo recurso anúncios. Correções incluem suporte para tipos de dados de data e hora na consulta SPEES para o Python e mensagens de erro aprimoradas no microsoftml quando modelos previamente treinados estão ausentes. |
| CU 5 | Correções de bugs e atualização de pacotes, mas nenhum novo recurso anúncios. Correções incluem melhorias para transformar as funções e variáveis no revoscalepy, corrigindo os erros relacionados longo caminho em rxInstallPackages, corrigindo as conexões em um loopback para RxExec rx_exec funções e revisões de mensagens de aviso. |
| CU 4 | Correções de bugs e atualização de pacotes, mas nenhum novo recurso anúncios. |
| CU 3 | Revoscalepy, a serialização do modelo de Python usando o [rx_serialize_model função](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/><br/>[Pontuação nativa](sql-native-scoring.md) além de aprimoramentos [em tempo real de pontuação](real-time-scoring.md). No banco de dados de pontuação, taxa de transferência é um milhão de linhas por segundo usando modelos do R. Nesta atualização, a pontuação em tempo real e a pontuação nativa oferecem melhor desempenho em uma única linha e a pontuação do lote. Nativo de pontuação usa uma função T-SQL para rápido de pontuação que pode ser executada em qualquer edição do SQL Server, até mesmo no Linux. A função não requer nenhuma instalação do R ou configuração adicional. Isso significa que você pode treinar um modelo em outro lugar, salvá-lo no SQL Server e, em seguida, executar pontuação sem nunca chamar o R. Para obter mais informações sobre as metodologias de pontuação, consulte [como executar pontuação em tempo real ou pontuação nativa](r/how-to-do-realtime-scoring.md). |
| CU 2 | Correções de bugs e atualização de pacotes, mas nenhum novo recurso anúncios. |
| CU 1 | Revoscalepy, adiciona rx_create_col_info para retornar informações de esquema de uma fonte de dados do SQL Server, semelhante à [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) r. <br/><br/>Aprimoramentos [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para dar suporte a cenários paralelos usando o `RxLocalParallel` contexto de computação.|
| Versão inicial |[**Integração do Python para análise no banco de dados**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>O [revoscalepy](python/what-is-revoscalepy.md) pacote é o equivalente de Python do RevoScaleR. Você pode criar modelos em Python para Regressão logística e linear, árvores de decisão, árvores aumentadas e florestas aleatórias, todos os paralelizáveis e sejam capazes de está sendo executado em contextos de computação remota. Este pacote dá suporte ao uso de várias fontes de dados e contextos de computação remota. O desenvolvedor ou cientista de dados pode executar código Python em um servidor SQL remoto, para explorar dados ou criar modelos sem movimentação de dados. <br/><br/>O [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) pacote é o equivalente de Python do pacote MicrosoftML R.<br/><br/>Integração do T-SQL e Python por meio [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Você pode chamar qualquer código do Python usando esse procedimento armazenado. Essa infraestrutura segura permite a implantação de empresarial de modelos em Python e scripts que podem ser chamados a partir de um aplicativo usando um procedimento armazenado simples. São obtidos ganhos de desempenho adicionais pela transmissão de dados do SQL para processos de Python e a paralelização de anel MPI. <br/><br/>Você pode usar o T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) função para realizar [pontuação nativa](sql-native-scoring.md) em um modelo previamente treinado que tenha sido previamente salva no formato binário solicitado.|
| Versão inicial | [**MicrosoftML (R)** ](using-the-microsoftml-package.md) contém algoritmos e transformação de dados que pode ser contextos de computação remota em escala ou executados em de aprendizado de máquina de última geração. Algoritmos incluem personalizáveis redes neurais profundas, árvores de decisão rápidas e florestas de decisão, regressão linear e regressão logística. |
| Versão inicial | [**Modelos previamente treinados** ](install/sql-pretrained-models-install.md) para reconhecimento de imagem e análise de sentimento negativo positivo. Use esses modelos para gerar previsões em seus próprios dados. |
| Versão inicial | [**Gerenciamento de pacotes de R**](r/install-additional-r-packages-on-sql-server.md), incluindo os seguintes destaques: funções para ajudar a gerenciar pacotes e atribuir permissões para instalar os pacotes, o DBA [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução no T-SQL para ajuda os DBAs gerenciar pacotes sem precisar saber o R e funções de um conjunto avançado de R no [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) ajudar a instalar, remover ou listar pacotes pertencentes aos usuários. |
| Versão inicial | [**Operacionalização por meio do mrsdeploy** ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package) para a implantação e o script de R como um serviço web de hospedagem. Aplica-se a somente script de R (não há equivalente no Python). Deve ser a opção de servidor (autônomo) evitar a competição por recurso com outras operações do SQL Server. |


## <a name="new-in-sql-server-2016"></a>Novo no SQL Server 2016

Esta versão introduzida recursos de machine learning no SQL Server por meio **SQL Server 2016 R Services**, um mecanismo de análise no banco de dados para o script de R de processamento nos dados residentes em uma instância do mecanismo de banco de dados.

Além disso, **SQL Server 2016 R Server (autônomo)** foi lançado como uma maneira de instalar o R Server em um servidor Windows. Instalação do SQL Server fornecidas inicialmente, a única maneira de instalar o R Server para Windows. Em versões posteriores, os desenvolvedores e cientistas de dados que desejava R Server no Windows pode usar o instalador autônomo do outro para alcançar o mesmo objetivo. O servidor autônomo no SQL Server é funcionalmente equivalente ao produto de servidor autônomo, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

| Versão |Atualização do recurso |
|---------|----------------|
| Adições de CU | [**Pontuação em tempo real** ](real-time-scoring.md) se baseia em bibliotecas nativas do C++ para ler um modelo armazenado em um formato binário otimizado e, em seguida, gerar previsões sem a necessidade de chamar o tempo de execução de R. Isso torna muito mais rapidamente as operações de pontuação. Com a pontuação em tempo real, você pode executar um procedimento armazenado ou realizar em tempo real de pontuação do código R. Pontuação em tempo real também está disponível para o SQL Server 2016, se a instância for atualizada para a versão mais recente do [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
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
