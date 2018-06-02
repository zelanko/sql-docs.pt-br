---
title: O que&#39;novo nos serviços de aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 092216f7bc1142125156b3658f035154d809c2e9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34586068"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>O que há de novo nos serviços de aprendizado de máquina do SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Recursos de aprendizado de máquina são adicionados ao SQL Server em cada versão conforme continuamos a expandir, estender e aprofundar a integração entre a plataforma de dados e a ciência de dados, análise e supervisionado aprendizado sobre os dados que você deseja implementar. 

## <a name="new-in-sql-server-2017"></a>Novo no SQL Server de 2017

Esta versão adicionado algoritmos de aprendizado de máquina de setor e suporte de Python. Renomeado para refletir o novo escopo, SQL Server 2017 marcado a introdução de **serviços de aprendizado de máquina do SQL Server (no banco de dados)**, com o suporte de linguagem Python e R. 

Esta versão também introduzida **o servidor de aprendizado de máquina do SQL Server (autônomo)** totalmente independentes do SQL Server, para R e Python cargas de trabalho que você deseja executar em um sistema dedicado. Com o servidor autônomo, você pode distribuir e dimensionar soluções R ou Python sem usar o SQL Server.

| Versão | Atualização de recurso |
|---------|----------------|
| ATUALIZAÇÃO CUMULATIVA 6 | Correções de bugs e atualização de pacote, mas nenhum novo recurso anúncios. Correções incluem suporte para tipos de dados de data/hora na consulta SPEES Python e mensagens de erro aprimoradas no microsoftml quando modelos previamente treinados estão ausentes. |
| ATUALIZAÇÃO CUMULATIVA 5 | Correções de bugs e atualização de pacote, mas nenhum novo recurso anúncios. Correções incluem melhorias para transformar a funções e variáveis no revoscalepy, correção dos erros relacionados a caminho longo em rxInstallPackages, corrigindo conexões em um loopback para RxExec rx_exec funções e revisões de mensagens de aviso. |
| ATUALIZAÇÃO CUMULATIVA 4 | Correções de bugs e atualização de pacote, mas nenhum novo recurso anúncios. |
| ATUALIZAÇÃO CUMULATIVA 3 | Serialização no revoscalepy, de modelo do Python usando a [rx_serialize_model função](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/><br/>[Pontuação nativo](sql-native-scoring.md) mais aprimoramentos [em tempo real de pontuação](real-time-scoring.md). Com a pontuação no banco de dados, taxa de transferência é um milhão de linhas por segundo usando modelos de R. Nesta atualização, em tempo real de pontuação e pontuação nativo oferecem melhor desempenho em uma linha e a pontuação do lote. Nativo pontuação usa uma função de T-SQL para pontuação rápida que pode ser executada em qualquer edição do SQL Server, mesmo em Linux. A função não requer nenhuma instalação de R ou configuração adicional. Isso significa que você pode treinar um modelo em outro lugar, salvá-lo no SQL Server e, em seguida, executar pontuação sem nunca chamar R. Para obter mais informações sobre as metodologias de pontuação, consulte [como realizar em tempo real de pontuação ou pontuação nativo](r/how-to-do-realtime-scoring.md). |
| ATUALIZAÇÃO CUMULATIVA 2 | Correções de bugs e atualização de pacote, mas nenhum novo recurso anúncios. |
| ATUALIZAÇÃO CUMULATIVA 1 | Revoscalepy, adiciona rx_create_col_info para retornar informações de esquema de uma fonte de dados do SQL Server, semelhante a [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) r. <br/><br/>Aprimoramentos para [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para dar suporte a cenários paralelos usando o `RxLocalParallel` contexto de computação.|
| Versão inicial |[**Integração do Python para análise no banco de dados**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>O [revoscalepy](python/what-is-revoscalepy.md) pacote é o equivalente de Python de RevoScaleR. Você pode criar modelos de Python para árvores de decisão, regressão linear e logística, árvores aumentadas e florestas aleatórias, todos os paralelizáveis e é capazes de está sendo executado em contextos de computação remota. Este pacote dá suporte ao uso de várias fontes de dados e contextos de computação remota. O cientista de dados ou o desenvolvedor pode executar o código Python em um servidor SQL remoto, para explorar dados ou criar modelos sem mover os dados. <br/><br/>O [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) pacote é o equivalente de Python do pacote MicrosoftML R.<br/><br/>Integração do T-SQL e Python por meio de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Você pode chamar qualquer código Python usando esse procedimento armazenado. Essa infraestrutura segura permite a implantação de nível empresarial de scripts que podem ser chamados a partir de um aplicativo usando um procedimento armazenado simples e modelos de Python. São obtidos ganhos de desempenho adicionais por streaming de dados do SQL para paralelização do anel MPI e processos de Python. <br/><br/>Você pode usar o T-SQL [PREVER](../t-sql/queries/predict-transact-sql.md) função para executar [pontuação nativo](sql-native-scoring.md) em um modelo previamente treinado que tenha sido previamente salva em formato binário necessário.|
| Versão inicial | [**MicrosoftML (R)** ](using-the-microsoftml-package.md) contém algoritmos e transformação de dados que pode ser contextos de computação remota dimensionado ou executados em de aprendizado de máquina de última geração. Algoritmos incluem redes neurais profundas personalizáveis, árvores de decisão rápida e florestas de decisão, regressão linear e regressão logística. |
| Versão inicial | [**Modelos previamente treinados** ](r/install-pretrained-models-sql-server.md) de reconhecimento de imagem e análise de sentimento positivo negativo. Use esses modelos para gerar previsões em seus próprios dados. |
| Versão inicial | [**Gerenciamento de pacotes de R**](r/install-additional-r-packages-on-sql-server.md), incluindo os seguintes destaques: funções para ajudar a gerenciar pacotes e atribuir permissões ao instalar pacotes, o DBA do banco de dados [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução T-SQL para ajuda os DBAs gerenciar pacotes sem precisar saber o R e um conjunto avançado de R funções em [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) ajudar a instalar, remover ou listar pacotes pertencentes a usuários. |
| Versão inicial | [**Operacionalização por meio de mrsdeploy** ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package) para a implantação e o script de R como um serviço web de hospedagem. Aplica-se a somente script R (nenhum equivalente de Python). Deve ser a opção de servidor (autônomo) evitar a competição do recurso com outras operações do SQL Server. |


## <a name="new-in-sql-server-2016"></a>Novo no SQL Server 2016

Esse recursos no SQL Server por meio de aprendizado de máquina de versão introduzido **SQL Server 2016 R Services**, um mecanismo de análise no banco de dados para o script de processamento de R em dados residentes em uma instância do mecanismo de banco de dados.

Além disso, **servidor de R (autônomo) do SQL Server 2016** foi lançado como uma maneira de instalar o R Server em um servidor Windows. Instalação do SQL Server fornecidas inicialmente, a única maneira de instalar o R Server para Windows. Em versões posteriores, os desenvolvedores e cientistas de dados que desejavam R Server no Windows podem usar o instalador autônomo do outro para alcançar o mesmo objetivo. O servidor autônomo no SQL Server é funcionalmente equivalente ao produto de servidor autônomo, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

| Versão |Atualização de recurso |
|---------|----------------|
| Adições de atualizações Cumulativas | [**Em tempo real de pontuação** ](real-time-scoring.md) se baseia em bibliotecas nativas C++ para ler um modelo armazenado em um formato binário otimizado e, em seguida, gerar previsões sem a necessidade de chamar o tempo de execução de R. Isso torna muito mais rápido de operações de pontuação. Com a pontuação em tempo real, você pode executar um procedimento armazenado ou realizar em tempo real de pontuação do código R. Em tempo real de pontuação também está disponível para o SQL Server 2016, se a instância for atualizada para a versão mais recente do [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versão inicial | [**Integração do R para análise no banco de dados**](r/sql-server-r-services.md). <br/><br/> Pacotes de R para R chamando funções em T-SQL e vice-versa. Funções de RevoScaleR fornecem análises de R em escala por agrupamento de dados em partes do componente, coordenação e gerenciamento distribuído de processamento e agregar os resultados. No SQL Server 2016 R Services (no banco de dados), o mecanismo de RevoScaleR é integrado com uma instância do mecanismo de banco de dados, brining dados e análise junto no mesmo contexto de processamento. <br/><br/>Integração do T-SQL e R por meio de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Você pode chamar qualquer código de R usando esse procedimento armazenado. Essa infraestrutura segura permite a implantação de nível empresarial de modelos Rn e scripts que podem ser chamados a partir de um aplicativo usando um procedimento armazenado simples. São obtidos ganhos de desempenho adicionais por streaming de dados do SQL para paralelização do anel MPI e processos de R. <br/><br/>Você pode usar o T-SQL [PREVER](../t-sql/queries/predict-transact-sql.md) função para executar [pontuação nativo](sql-native-scoring.md) em um modelo previamente treinado que tenha sido previamente salva em formato binário necessário.|

## <a name="linux-support-roadmap"></a>Roteiro de suporte do Linux

Aprendizado de máquina usando o R ou Python no banco de dados não é suportado atualmente no SQL Server no Linux. Procure os anúncios em uma versão posterior.

No entanto, no Linux você pode executar [pontuação nativo](sql-native-scoring.md) usando a função PREVER T-SQL. Pontuação nativo permite a pontuação de um modelo pré-treinado muito rápido, sem chamar ou até mesmo exigir um tempo de execução de R. Isso significa que você pode usar o SQL Server no Linux para gerar previsões muito rápidos, para atender a aplicativos cliente.

<a name="azure-sql-database-roadmap"></a>

## <a name="azure-sql-database-roadmap"></a>Roteiro de banco de dados SQL do Azure

Não há suporte limitado para R no banco de dados do SQL Azure: disponível apenas no Oeste centro dos EUA, em serviços criados na camada Premium. Cobertura expandida, incluindo suporte a Python, é provável a seguir em uma versão futura. No entanto, há uma data de lançamento projetada no momento.  

## <a name="next-steps"></a>Próximas etapas

+ [Instale os serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados)](install/sql-machine-learning-services-windows-install.md)
+ [Exemplos e tutoriais de aprendizado de máquina](tutorials/machine-learning-services-tutorials.md)
