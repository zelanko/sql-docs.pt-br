---
title: O que&#39;new - s serviços do SQL Server Machine Learning
description: Lançamentos de novos recursos para cada versão do SQL Server 2016 R Services, Microsoft R Server, serviços de aprendizado de máquina do SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f9e98d59318c9c7d43fd6f99195da972c4eca0c9
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432489"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>O que há de novo nos serviços do SQL Server Machine Learning 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Recursos de aprendizado de máquina são adicionados ao SQL Server em cada versão enquanto continuamos a expandir, estender e aprofundar a integração entre a plataforma de dados, análise avançada e de ciência de dados. 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>Novo na visualização do SQL Server de 2019

Essa versão adiciona os recursos mais solicitados para operações de aprendizado de máquina de R e Python no SQL Server. Para obter mais informações sobre todos os recursos nesta versão, consulte [o que há de novo no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [notas de versão do SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

| Versão | Atualização do recurso |
|---------|----------------|
| CTP 2.0 | Suporte a plataformas Linux para o R e Python de machine learning. Introdução ao [instalar o SQL Server Machine Learning Services no Linux](../linux/sql-server-linux-setup-machine-learning.md). |
|   | [Extensão da linguagem Java](java/extension-java.md) no Windows e Linux é novo na visualização do SQL Server de 2019. Você pode disponibilizar Java compilado de código para o SQL Server atribuindo permissões e definindo o caminho. Aplicativos de cliente com acesso ao SQL Server podem usar dados e executar seu código chamando [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), o mesmo procedimento usado para a integração de R e Python no SQL Server. | 
|  | O [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) apresenta dois novos parâmetros que permitem que você gere facilmente vários modelos de dados particionados. Saiba mais neste tutorial [criar modelos com base em partição em R](tutorials/r-tutorial-create-models-per-partition.md). |
|   | Agora há suporte para o suporte de cluster de failover no Windows e Linux, supondo que o serviço Launchpad do SQL Server é iniciado em todos os nós. Para obter mais informações, consulte [instalação de cluster de failover do SQL Server](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md). |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>Novo no SQL Server 2017

Essa versão adiciona [suporte do Python e algoritmos de aprendizado de máquina de líderes do setor](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Renomeado para refletir o novo escopo, o SQL Server 2017 marca a introdução de [serviços do SQL Server Machine Learning (no banco de dados)](what-is-sql-server-machine-learning.md), com suporte de idioma para o Python e R. 

Para o recurso anúncios completo, consulte [o que há de novo no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

### <a name="r-enhancements"></a>Aprimoramentos de R

O componente de R do SQL Server 2017 Machine Learning Services é a próxima geração do SQL Server 2016 R Services, com versões atualizadas de R base, RevoScaler e outros pacotes.

Novos recursos para R incluem [ **gerenciamento de pacotes**](r/install-additional-r-packages-on-sql-server.md), com os seguintes destaques: 

+ Funções de banco de dados ajudam os DBAs gerenciar pacotes e atribuir permissões para a instalação do pacote.
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DBAs de ajuda a gerenciar os pacotes na linguagem T-SQL familiar.
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) funções ajudam a instalar, remover ou listar pacotes pertencem aos usuários. Para obter mais informações, consulte [pacotes de como usar funções RevoScaleR para localizar ou instalar o R no SQL Server](r/use-revoscaler-to-manage-r-packages.md).

### <a name="r-libraries"></a>Bibliotecas do R

| Pacote | Descrição |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | Nesta versão, MicrosoftML é incluído em uma instalação de R padrão, eliminando a etapa de atualização necessária no SQL Server 2016 R Services anterior. MicrosoftML fornece transformações de dados que podem ser dimensionadas ou executadas em contextos de computação remota e algoritmos de aprendizado de máquina de última geração. Algoritmos incluem personalizáveis redes neurais profundas, árvores de decisão rápidas e florestas de decisão, regressão linear e regressão logística.  |

### <a name="python-integration-for-in-database-analytics"></a>Integração do Python para análise no banco de dados

Python é uma linguagem que oferece excelente flexibilidade e capacidade para uma variedade de tarefas de aprendizado de máquina. Bibliotecas de código-fonte aberto para Python incluem várias plataformas para as redes neurais personalizáveis, bem como bibliotecas populares para o processamento de idioma natural. Agora, essa linguagem amplamente usados é suportada no aprendizado de máquina do SQL Server 2017.

Como o Python é integrado com o mecanismo de banco de dados, você pode manter a análise próxima aos dados e eliminar os custos e riscos de segurança associados à movimentação de dados. Você pode implantar soluções de aprendizado de máquina com base em Python usando ferramentas como o Visual Studio. Seus aplicativos de produção podem obter previsões de modelos, ou métodos de acesso de visuais do tempo de execução de Python 3.5 usando dados do SQL Server.

Integração do T-SQL e Python tem suporte por meio de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimento armazenado do sistema. Você pode chamar qualquer código do Python usando esse procedimento armazenado. Código é executado em uma arquitetura dual segura que permite a implantação de empresarial de scripts, que pode ser chamados de um aplicativo usando um procedimento armazenado simples e modelos em Python. São obtidos ganhos de desempenho adicionais pela transmissão de dados do SQL para processos de Python e a paralelização de anel MPI.

Você pode usar o T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) função para realizar [pontuação nativa](sql-native-scoring.md) em um modelo previamente treinado que tenha sido previamente salva no formato binário solicitado.

### <a name="python-libraries"></a>Bibliotecas do Python

| Pacote | Descrição |
|---------|-------------|
[**revoscalepy**](python/ref-py-revoscalepy.md)| Equivalente de Python do RevoScaleR. Você pode criar modelos em Python para Regressão logística e linear, árvores de decisão, árvores aumentadas e florestas aleatórias, todos os paralelizáveis e sejam capazes de está sendo executado em contextos de computação remota. Este pacote dá suporte ao uso de várias fontes de dados e contextos de computação remota. O desenvolvedor ou cientista de dados pode executar código Python em um servidor SQL remoto, para explorar dados ou criar modelos sem movimentação de dados. |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python equivalente do pacote MicrosoftML R. |

### <a name="pre-trained-models"></a>Modelos previamente treinados

[**Modelos previamente treinados** ](install/sql-pretrained-models-install.md) estão disponíveis para Python e R. usam esses modelos para reconhecimento de imagem e análise de sentimento negativo positivo, para gerar previsões em seus próprios dados. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>Servidor autônomo como um recurso compartilhado na instalação do SQL Server

Esta versão também adiciona [SQL Server Machine Learning Server (autônomo)](r/r-server-standalone.md), um servidor de ciência de dados totalmente independente, que dão suporte a análise preditiva e estatística em R e Python. Como com o R Services, esse servidor é a próxima versão do SQL Server 2016 R Server (autônomo). Com o servidor autônomo, você pode distribuir e dimensionar soluções R ou Python, sem nenhuma dependência no SQL Server.
::: moniker-end

## <a name="new-in-sql-server-2016"></a>Novo no SQL Server 2016

Esta versão introduzida recursos de machine learning no SQL Server por meio **SQL Server 2016 R Services**, um mecanismo de análise no banco de dados para o script de R de processamento nos dados residentes em uma instância do mecanismo de banco de dados.

Além disso, **SQL Server 2016 R Server (autônomo)** foi lançado como uma maneira de instalar o R Server em um servidor Windows. Instalação do SQL Server fornecidas inicialmente, a única maneira de instalar o R Server para Windows. Em versões posteriores, os desenvolvedores e cientistas de dados que desejava R Server no Windows pode usar o instalador autônomo do outro para alcançar o mesmo objetivo. O servidor autônomo no SQL Server é funcionalmente equivalente ao produto de servidor autônomo, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para o recurso anúncios completo, consulte [o que há de novo no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

| Versão |Atualização do recurso |
|---------|----------------|
| Adições de atualização cumulativa | [**Pontuação em tempo real** ](real-time-scoring.md) se baseia em bibliotecas nativas do C++ para ler um modelo armazenado em um formato binário otimizado e, em seguida, gerar previsões sem a necessidade de chamar o tempo de execução de R. Isso torna muito mais rapidamente as operações de pontuação. Com a pontuação em tempo real, você pode executar um procedimento armazenado ou executar pontuação em tempo real de código R. Pontuação em tempo real também está disponível para o SQL Server 2016, se a instância for atualizada para a versão mais recente do [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versão inicial | [**Integração do R para análise no banco de dados**](r/sql-server-r-services.md). <br/><br/> Pacotes de R para R chamada de funções no T-SQL e vice-versa. Funções RevoScaleR fornecem análise de R em grande escala, fragmentando dados em partes componentes, coordenação e gerenciamento distribuído de processamento e agregar resultados. No SQL Server 2016 R Services (no banco de dados), o mecanismo de RevoScaleR é integrado com uma instância do mecanismo de banco de dados, brining juntos no mesmo contexto de processamento de análise e dados. <br/><br/>Integração do T-SQL e R por meio [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Você pode chamar qualquer código R usando esse procedimento armazenado. Essa infraestrutura segura permite a implantação de empresarial de modelos Rn e scripts que podem ser chamados a partir de um aplicativo usando um procedimento armazenado simples. São obtidos ganhos de desempenho adicionais pela transmissão de dados do SQL para processos de R e a paralelização de anel MPI. <br/><br/>Você pode usar o T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) função para realizar [pontuação nativa](sql-native-scoring.md) em um modelo previamente treinado que tenha sido previamente salva no formato binário solicitado.|

## <a name="linux-support-roadmap"></a>Roteiro de suporte do Linux

SQL Server 2019 CTP 2.0 adiciona suporte do Linux para R, Python e Java quando você instala os pacotes com uma instância do mecanismo de banco de dados de aprendizado de máquina. Para obter mais informações, consulte [instalar o SQL Server Machine Learning Services no Linux](../linux/sql-server-linux-setup-machine-learning.md).

No Linux, SQL Server 2017 não tem integração de R ou Python, mas você pode usar [pontuação nativa](sql-native-scoring.md) no Linux porque essa funcionalidade está disponível por meio do T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md), que é executado no Linux. Pontuação nativa permite que a pontuação de alto desempenho de um modelo previamente treinado, sem chamar ou até mesmo exigir um tempo de execução de R.

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Serviços no banco de dados SQL do Azure Machine Learning

Serviços de Machine Learning (com R) no banco de dados SQL está em visualização pública. Para obter mais informações, consulte [guia de início rápido: Usar serviços de Machine Learning (com R) no banco de dados do SQL do Azure (visualização)](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-r).

## <a name="next-steps"></a>Próximas etapas

+ [Instalar serviços de Machine Learning do SQL Server 2017 (no banco de dados)](install/sql-machine-learning-services-windows-install.md)
+ [Exemplos e tutoriais de aprendizado de máquina](tutorials/machine-learning-services-tutorials.md)
