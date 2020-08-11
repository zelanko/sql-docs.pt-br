---
title: Novidades dos Serviços de Machine Learning do SQL Server
titleSuffix: ''
description: Comunicados de novos recursos para cada versão do Serviços de Machine Learning do SQL Server e Serviço de R do SQL Server 2016.
ms.date: 11/04/2019
ms.topic: overview
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7e4092bd98749006b6f68b8c55fee3baca678255
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245235"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Novidades dos Serviços de Machine Learning do SQL Server

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

As funcionalidades de aprendizado de máquina são adicionadas ao SQL Server em cada versão à medida que continuamos expandindo, estendendo e aprofundando a integração entre a plataforma de dados, a análise avançada e a ciência de dados. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019"></a>Novidades do SQL Server 2019

Esta versão adiciona os recursos mais solicitados para operações de aprendizado de máquina do Python e do R no SQL Server. Para obter mais informações sobre todos os recursos desta versão, confira [Novidades do SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [Notas sobre a versão do SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

> [!NOTE]
> Para obter a documentação das novidades do Java no SQL Server 2019, confira [Novidades das Extensões de Linguagem do SQL Server](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)

Confira abaixo os novos recursos dos Serviços de Machine Learning do SQL Server, disponíveis no **Windows** e no **Linux**:

- A compatibilidade com a plataforma Linux foi adicionada nos Serviços de Machine Learning para Python e para R. Introdução a [Instalar os Serviços de Machine Learning do SQL Server no Linux](../linux/sql-server-linux-setup-machine-learning.md).
- [Conexão em loopback para SQL Server de um script Python ou R](connect/loopback-connection.md). 
- [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) para Python e R.
- O [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) introduz dois novos parâmetros que permitem gerar com facilidade vários modelos com base em dados particionados. Saiba mais neste tutorial: [Criar modelos baseados em partição no R](tutorials/r-tutorial-create-models-per-partition.md).
- A compatibilidade do cluster de failover está disponível para o serviço Launchpad, supondo que o serviço SQL Server Launchpad tenha sido iniciado em todos os nós. Para obter mais informações, confira [Instalação do cluster de failover do SQL Server](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md).
- Alterações no mecanismo de isolamento para os Serviços de Machine Learning. Para obter mais informações, confira [SQL Server 2019 no Windows: alterações de isolamento nos Serviços de Machine Learning](install/sql-server-machine-learning-services-2019.md).

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>Novidades do SQL Server 2017

Esta versão adiciona [o suporte do Python e algoritmos de aprendizado de máquina líderes do setor](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Renomeado para refletir o novo escopo, o SQL Server 2017 marca a introdução dos [Serviços de Machine Learning do SQL Server (no Banco de Dados)](sql-server-machine-learning-services.md), com suporte a linguagens para Python e R. 

Para obter os comunicados sobre todos os recursos, confira [Novidades do SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

### <a name="r-enhancements"></a>Melhorias do R

O componente do R dos Serviços de Machine Learning do SQL Server é a próxima geração do SQL Server 2016 R Services, com versões atualizadas do R base, do RevoScaler e de outros pacotes.

As novas funcionalidades do R incluem o [**gerenciamento de pacotes**](package-management/install-r-packages-with-tsql.md), com os seguintes destaques: 

+ As funções de banco de dados ajudam os DBAs a gerenciar pacotes e atribuir permissões para a instalação de pacotes.
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) ajuda os DBAs a gerenciar pacotes na linguagem T-SQL que eles já conhecem.
+ As funções do [RevoScaleR](package-management/install-r-packages-with-revoscaler.md) ajudam a instalar, remover ou listar os pacotes pertencentes aos usuários. Para obter mais informações, confira [Como usar as funções do RevoScaleR para localizar ou instalar pacotes R no SQL Server](package-management/install-r-packages-with-revoscaler.md).

### <a name="r-libraries"></a>Bibliotecas do R

| Pacote | Descrição |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | Nesta versão, o MicrosoftML está incluído em uma instalação padrão do R, eliminando a etapa de atualização necessária no SQL Server 2016 R Services anterior. O MicrosoftML fornece algoritmos de aprendizado de máquina e transformações de dados de última geração que podem ser dimensionados ou executados em contextos de computação remota. Os algoritmos incluem redes neurais profundas personalizáveis, árvores de decisão rápida e florestas de decisão, regressão linear e regressão logística.  |

### <a name="python-integration-for-in-database-analytics"></a>Integração do Python para análise no banco de dados

O Python é uma linguagem que oferece grande flexibilidade e poder para uma variedade de tarefas de aprendizado de máquina. As bibliotecas open-source para o Python incluem várias plataformas para redes neurais personalizáveis, bem como bibliotecas populares para processamento de idioma natural. 

Como o Python é integrado ao mecanismo de banco de dados, você pode manter a análise próxima aos dados e eliminar os custos e os riscos de segurança associados à movimentação de dados. Implante soluções de aprendizado de máquina baseadas no Python usando ferramentas como o Visual Studio. Seus aplicativos de produção podem obter previsões, modelos ou visuais do runtime do Python 3.5 usando métodos de acesso a dados do SQL Server.

Há suporte para a integração entre o T-SQL e o Python por meio do procedimento armazenado do sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Você pode chamar qualquer código Python usando esse procedimento armazenado. O código é executado em uma arquitetura segura e dupla que permite a implantação de nível empresarial de scripts e modelos do Python, que podem ser chamados em um aplicativo usando um procedimento armazenado simples. Ganhos de desempenho adicionais são obtidos por meio do streaming de dados dos processos do SQL para os processos do Python e da paralelização de anel MPI.

Use a função T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) para executar a [pontuação nativa](predictions/native-scoring-predict-transact-sql.md) em um modelo pré-treinado que foi salvo anteriormente no formato binário exigido.

### <a name="python-libraries"></a>Bibliotecas do Python

| Pacote | Descrição |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Equivalente no Python do RevoScaleR. Crie modelos do Python para regressões lineares e logísticas, árvores de decisão, árvores aumentadas e florestas aleatórias, todas paralelizáveis e com a capacidade de serem executadas em contextos de computação remota. Esse pacote dá suporte ao uso de várias fontes de dados e de contextos de computação remota. O cientista de dados ou o desenvolvedor pode executar o código Python em um SQL Server remoto para explorar os dados ou criar modelos sem mover os dados. |
|[**microsoftml**](python/ref-py-microsoftml.md) |Equivalente no Python do pacote R MicrosoftML. |

### <a name="pre-trained-models"></a>Modelos previamente treinados

[**Modelos pré-treinados**](install/sql-pretrained-models-install.md) estão disponíveis para o Python e o R. Use esses modelos para reconhecimento de imagem e análise de sentimento positivo/negativo, a fim de gerar previsões com base em seus próprios dados. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>Servidor autônomo como um recurso compartilhado na Instalação do SQL Server

Essa versão também adiciona o [SQL Server Machine Learning Server (Autônomo)](r/r-server-standalone.md), um servidor de ciência de dados totalmente independente, que dá suporte às análises estatística e preditiva no R e no Python. Assim como ocorre com o R Services, esse servidor é a próxima versão do SQL Server 2016 R Server (Autônomo). Com o servidor autônomo, você pode distribuir e dimensionar soluções do R ou do Python sem dependências no SQL Server.
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2016"></a>Novidades do SQL Server 2016

Esta versão introduziu funcionalidades de aprendizado de máquina no SQL Server por meio do **SQL Server 2016 R Services**, um mecanismo de análise no banco de dados para processamento do script R em dados residentes em uma instância do mecanismo de banco de dados.

Além disso, o **SQL Server 2016 R Server (Autônomo)** foi lançado como uma maneira de instalar o R Server em um Windows Server. Inicialmente, a Instalação do SQL Server fornecia a única maneira de instalar o R Server para Windows. Em versões posteriores, os desenvolvedores e os cientistas de dados que queriam o R Server no Windows puderam usar outro instalador autônomo para atingir a mesma meta. O servidor autônomo no SQL Server é funcionalmente equivalente ao produto de servidor autônomo, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para obter os comunicados sobre todos os recursos, confira [Novidades do SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

| Versão |Atualização de recursos |
|---------|----------------|
| Adições de CU | A [**pontuação em tempo real**](predictions/real-time-scoring.md) depende de bibliotecas nativas C++ para ler um modelo armazenado em um formato binário otimizado e, em seguida, gerar previsões sem precisar chamar o runtime do R. Isso torna as operações de pontuação muito mais rápidas. Com a pontuação em tempo real, você pode executar um procedimento armazenado ou realizar a pontuação em tempo real por meio do código R. A pontuação em tempo real também estará disponível para o SQL Server 2016 se a instância for atualizada para a última versão do [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versão inicial | [**Integração do R para análise no banco de dados**](r/sql-server-r-services.md). <br/><br/> Pacotes R para chamar funções do R no T-SQL e vice-versa. As funções do RevoScaleR fornecem a análise do R em escala, dividindo os dados em partes de componentes, coordenando e gerenciando o processamento distribuído e agregando os resultados. No SQL Server 2016 R Services (no Banco de Dados), o mecanismo do RevoScaleR é integrado a uma instância do mecanismo de banco de dados, reunindo os dados e a análise no mesmo contexto de processamento. <br/><br/>Integração entre o T-SQL e o R por meio de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Você pode chamar qualquer código R usando esse procedimento armazenado. Essa infraestrutura segura permite a implantação de nível empresarial de modelos e scripts do Rn que podem ser chamados em um aplicativo usando um procedimento armazenado simples. Ganhos de desempenho adicionais são obtidos por meio do streaming de dados dos processos do SQL para os processos do R e da paralelização de anel MPI. <br/><br/>Use a função T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) para executar a [pontuação nativa](predictions/native-scoring-predict-transact-sql.md) em um modelo pré-treinado que foi salvo anteriormente no formato binário exigido.|

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="linux-support"></a>Suporte para Linux

O SQL Server 2019 adiciona o suporte para Linux para R e Python quando você instala os pacotes de aprendizado de máquina com uma instância do mecanismo de banco de dados. Para obter mais informações, confira [Instalar os Serviços de Machine Learning do SQL Server no Linux](../linux/sql-server-linux-setup-machine-learning.md).

No Linux, o SQL Server 2017 não tem a integração do R nem do Python, mas você pode usar a [pontuação nativa](predictions/native-scoring-predict-transact-sql.md) no Linux, pois essa funcionalidade está disponível por meio do T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md), que é executado no Linux. A pontuação nativa permite a pontuação de alto desempenho por meio de um modelo pré-treinado, sem chamar ou, até mesmo, exigir um runtime do R.
::: moniker-end

## <a name="next-steps"></a>Próximas etapas

+ [Instalar os Serviços de Machine Learning do SQL Server (no Banco de Dados)](install/sql-machine-learning-services-windows-install.md)
