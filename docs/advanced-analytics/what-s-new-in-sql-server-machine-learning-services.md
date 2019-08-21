---
title: Novidades
description: Novos comunicados de recursos para cada versão do SQL Server 2016 R Services, R Server SQL Server Serviços de Machine Learning.
ms.date: 08/21/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f582088359c2878f5dfd84d4b353b1f9d8c369e5
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652297"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>O que há de novo no SQL Server Serviços de Machine Learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Os recursos de aprendizado de máquina são adicionados a SQL Server em cada versão à medida que continuamos a expandir, estender e aprofundar a integração entre a plataforma de dados, a análise avançada e a ciência de dados. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>Novo na versão prévia do SQL Server 2019

Esta versão adiciona os recursos mais solicitados para operações de aprendizado de máquina R e Python no SQL Server. Para obter mais informações sobre todos os recursos desta versão, consulte [What ' s New in SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [release notes for SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

> [!NOTE]
> Para obter a documentação sobre o que há de novo no Java no SQL Server 2019, consulte o [que há de novo nas extensões de linguagem do SQL Server?](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)

| Versão | Atualização de recurso |
|---------|----------------|
| RC 1 | [A conexão de auto-retorno para SQL Server de um script Python ou R](connect/loopback-connection.md) agora tem suporte para Windows e Linux. |
| CTP 3.2 | Nenhuma alteração. |
| CTP 3.1 | Nenhuma alteração. |
| CTP 3.0 | Nenhuma alteração. |
| CTP 2,5 | Nenhuma alteração. |
| CTP 2.4 | Suporte para Linux para [criar biblioteca externa (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) para R e Python. |
| CTP 2.3 | Somente no Windows, o código Python pode ser acessado em uma biblioteca externa usando a instrução [Create external library (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) . |
| CTP 2.2 | Nenhuma alteração. |
| CTP 2.1 | Nenhuma alteração. |
| CTP 2.0 | Suporte da plataforma Linux para aprendizado de máquina R e Python. Introdução à [instalação SQL Server serviços de Machine Learning no Linux](../linux/sql-server-linux-setup-machine-learning.md). |
|  | O [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) introduz dois novos parâmetros que permitem que você gere facilmente vários modelos a partir de dados particionados. Saiba mais neste tutorial, [criar modelos baseados em partição em R](tutorials/r-tutorial-create-models-per-partition.md). |
|   | O suporte ao cluster de failover agora tem suporte no Windows e no Linux, supondo que SQL Server Launchpad serviço seja iniciado em todos os nós. Para obter mais informações, consulte [SQL Server instalação de cluster de failover](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md). |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>Novidades no SQL Server 2017

Esta versão adiciona [suporte do Python e algoritmos de aprendizado de máquina líderes do setor](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Renomeado para refletir o novo escopo, SQL Server 2017 marca a introdução de [SQL Server serviços de Machine Learning (no banco de dados)](what-is-sql-server-machine-learning.md), com suporte de idioma para Python e R. 

Para anúncios de recursos, veja [novidades no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

### <a name="r-enhancements"></a>Aprimoramentos de R

O componente R do SQL Server Serviços de Machine Learning é a próxima geração de SQL Server 2016 R Services, com versões atualizadas de base R, RevoScaler e outros pacotes.

Os novos recursos do R incluem o [**Gerenciamento de pacotes**](r/install-additional-r-packages-on-sql-server.md), com os seguintes destaques: 

+ As funções de banco de dados ajudam DBAs a gerenciar pacotes e a atribuir permissões para a instalação do pacote.
+ [Criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) ajuda os DBAs a gerenciar pacotes na linguagem T-SQL familiar.
+ O [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) Functions ajuda a instalar, remover ou listar pacotes pertencentes a usuários. Para obter mais informações, consulte [como usar as funções RevoScaleR para localizar ou instalar pacotes R em SQL Server](r/use-revoscaler-to-manage-r-packages.md).

### <a name="r-libraries"></a>Bibliotecas de R

| Pacote | Descrição |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | Nesta versão, o MicrosoftML está incluído em uma instalação padrão do R, eliminando a etapa de atualização necessária no SQL Server 2016 R Services anterior. O MicrosoftML fornece algoritmos de aprendizado de máquina e transformações de dados de ponta que podem ser dimensionados ou executados em contextos de computação remota. Os algoritmos incluem redes neurais profundas personalizáveis, árvores de decisão rápidas e florestas de decisão, regressão linear e regressão logística.  |

### <a name="python-integration-for-in-database-analytics"></a>Integração do Python para análise no banco de dados

O Python é uma linguagem que oferece grande flexibilidade e potência para uma variedade de tarefas de aprendizado de máquina. As bibliotecas de software livre para Python incluem várias plataformas para redes neurais personalizáveis, bem como bibliotecas populares para processamento de idioma natural. 

Como o Python está integrado ao mecanismo de banco de dados, você pode manter a análise perto dos dados e eliminar os custos e os riscos de segurança associados à movimentação de dados. Você pode implantar soluções de aprendizado de máquina com base em Python usando ferramentas como o Visual Studio. Seus aplicativos de produção podem obter previsões, modelos ou visuais do tempo de execução do Python 3,5 usando SQL Server métodos de acesso a dados.

A integração do T-SQL e do Python tem suporte por meio do procedimento armazenado do sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) . Você pode chamar qualquer código Python usando este procedimento armazenado. O código é executado em uma arquitetura segura e dupla que permite a implantação de nível empresarial de scripts e modelos de Python, que podem ser chamados de um aplicativo usando um procedimento armazenado simples. Ganhos de desempenho adicionais são obtidos por meio de streaming de dados de SQL para processos Python e paralelização de anel MPI.

Você pode usar a função de [previsão](../t-sql/queries/predict-transact-sql.md) T-SQL para executar a [Pontuação nativa](sql-native-scoring.md) em um modelo pretreinado que foi salvo anteriormente no formato binário necessário.

### <a name="python-libraries"></a>Bibliotecas do Python

| Pacote | Descrição |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python-equivalente de RevoScaleR. Você pode criar modelos Python para regressões lineares e logísticas, árvores de decisão, árvores aumentadas e florestas aleatórias, todos os paralelizáveis e capazes de serem executados em contextos de computação remota. Este pacote dá suporte ao uso de várias fontes de dados e contextos de computação remota. O cientista ou desenvolvedor de dados pode executar código Python em um SQL Server remoto para explorar dados ou criar modelos sem mover dados. |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python-equivalente do pacote R MicrosoftML. |

### <a name="pre-trained-models"></a>Modelos previamente treinados

Os [**modelos pré-treinados**](install/sql-pretrained-models-install.md) estão disponíveis para o Python e o R. Use esses modelos para reconhecimento de imagem e análise de opiniões negativas positivas para gerar previsões sobre seus próprios dados. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>Servidor autônomo como um recurso compartilhado na instalação do SQL Server

Essa versão também adiciona [SQL Server Machine Learning Server (autônomo)](r/r-server-standalone.md), um servidor de ciência de dados totalmente independente, dando suporte a análises estatísticas e preditivas em R e Python. Assim como acontece com o R Services, esse servidor é a próxima versão do 2016 SQL Server R Server (autônomo). Com o servidor autônomo, você pode distribuir e dimensionar soluções de R ou Python sem dependências em SQL Server.
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2016"></a>Novidades no SQL Server 2016

Esta versão introduziu recursos de Machine Learning em SQL Server por meio de **SQL Server 2016 R Services**, um mecanismo de análise no banco de dados para processar o script R em dados residentes em uma instância do mecanismo de banco de dados.

Além disso, **SQL Server servidor r 2016 (autônomo)** foi lançado como uma maneira de instalar o R Server em um Windows Server. Inicialmente, SQL Server instalação forneceu a única maneira de instalar o R Server para Windows. Em versões posteriores, os desenvolvedores e os cientistas de dados que queriam que o R Server no Windows pudessem usar outro instalador autônomo para atingir o mesmo objetivo. O servidor autônomo no SQL Server é funcionalmente equivalente ao produto do servidor autônomo, [Microsoft R Server para o Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para anúncios de recursos, veja [novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

| Versão |Atualização de recurso |
|---------|----------------|
| Adições de atualização cumulativa | A [**Pontuação em tempo real**](real-time-scoring.md) depende de bibliotecas C++ nativas para ler um modelo armazenado em um formato binário otimizado e, em seguida, gerar previsões sem precisar chamar o tempo de execução de R. Isso torna as operações de Pontuação muito mais rápidas. Com a pontuação em tempo real, você pode executar um procedimento armazenado ou executar a pontuação em tempo real do código R. A pontuação em tempo real também está disponível para o SQL Server 2016, se a instância for atualizada para a versão [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]mais recente do. |
| Versão inicial | [**Integração do R para análise no banco de dados**](r/sql-server-r-services.md). <br/><br/> Pacotes de r para chamar funções do R no T-SQL e vice-versa. As funções RevoScaleR fornecem análise de R em escala, colocando dados em partes de componentes, coordenando e gerenciando o processamento distribuído e agregando resultados. No SQL Server R Services 2016 (no banco de dados), o mecanismo do RevoScaleR é integrado a uma instância do mecanismo de banco de dados, o brining data e a análise juntos no mesmo contexto de processamento. <br/><br/>Integração de T-SQL e R por meio do [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Você pode chamar qualquer código R usando esse procedimento armazenado. Essa infraestrutura segura permite a implantação de nível empresarial de modelos e scripts do RN que podem ser chamados de um aplicativo usando um procedimento armazenado simples. Ganhos de desempenho adicionais são obtidos por meio de streaming de dados de SQL para processos R e paralelização de anel MPI. <br/><br/>Você pode usar a função de [previsão](../t-sql/queries/predict-transact-sql.md) T-SQL para executar a [Pontuação nativa](sql-native-scoring.md) em um modelo pretreinado que foi salvo anteriormente no formato binário necessário.|

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="linux-support"></a>Suporte para Linux

SQL Server 2019 adiciona o suporte do Linux para R e Python quando você instala os pacotes de Machine Learning com uma instância do mecanismo de banco de dados. Para obter mais informações, consulte [instalar SQL Server serviços de Machine Learning no Linux](../linux/sql-server-linux-setup-machine-learning.md).

No Linux, SQL Server 2017 não tem integração de R ou Python, mas você pode usar a [Pontuação nativa](sql-native-scoring.md) no Linux, pois essa funcionalidade está disponível por meio da [previsão](../t-sql/queries/predict-transact-sql.md)de T-SQL, que é executada no Linux. A pontuação nativa permite a pontuação de alto desempenho de um modelo pretreinado, sem chamar ou até mesmo exigir um tempo de execução de R.
::: moniker-end

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Serviços de Machine Learning no banco de dados SQL do Azure

Serviços de Machine Learning no banco de dados SQL do Azure está em visualização pública. Para obter mais informações, consulte [serviços de Machine Learning do banco de dados SQL do Azure (versão prévia)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview).

## <a name="next-steps"></a>Próximas etapas

+ [Instalar SQL Server Serviços de Machine Learning (no banco de dados)](install/sql-machine-learning-services-windows-install.md)
+ [Exemplos e tutoriais do Machine Learning](tutorials/machine-learning-services-tutorials.md)
