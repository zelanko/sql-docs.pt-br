---
title: Extensão da linguagem de programação R
description: Saiba mais sobre a execução de código R e as bibliotecas de R internas no SQL Server 2016 R Services ou SQL Server 2017 Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 300b5d25d62be24c1e5590f5cd9795d08da7f2c1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470495"
---
# <a name="r-language-extension-in-sql-server"></a>Extensão da linguagem R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A extensão R faz parte da SQL Server Serviços de Machine Learning complemento ao mecanismo de banco de dados relacional. Ele adiciona um ambiente de execução de R, distribuição de R base com bibliotecas e ferramentas padrão e as bibliotecas do Microsoft R: [RevoScaleR](../r/ref-r-revoscaler.md) para análise em escala, [MicrosoftML](../r/ref-r-microsoftml.md) para algoritmos de aprendizado de máquina e outras bibliotecas para acessar dados ou código R no SQL Server.

A integração do R está disponível em SQL Server a partir do SQL Server 2016, com [R Services](../r/sql-server-r-services.md)e continuando como parte do [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md).

## <a name="r-components"></a>Componentes do R

SQL Server inclui pacotes de software livre e proprietários. As bibliotecas de R base são instaladas por meio da distribuição da Microsoft de software livre R: Microsoft R Open (MRO). Os usuários atuais de R devem ser capazes de portar seu código R e executá-lo como um processo externo em SQL Server com poucas ou nenhuma modificação. O MRO é instalado independentemente das ferramentas SQL e é executado fora dos processos do mecanismo principal, na estrutura de extensibilidade. Durante a instalação, você deve concordar com os termos da licença de código-fonte aberto. Depois disso, você pode executar pacotes R padrão sem mais modificação, assim como faria em qualquer outra distribuição de software livre do R. 

SQL Server não modifica os executáveis de R base, mas você deve usar a versão do R instalada pela instalação, pois essa versão é aquela na qual os pacotes proprietários são compilados e testados. Para obter mais informações sobre como o MRO difere de uma distribuição base do R que você pode obter do CRAN, consulte interoperabilidade [com a linguagem r e os produtos e recursos do Microsoft R](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

A distribuição de pacote base do R instalada pela instalação do pode ser encontrada na pasta associada à instância do. Por exemplo, se você instalou o R Services em uma instância padrão do SQL Server 2016, as bibliotecas do R estarão localizadas nessa pasta `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`por padrão:. Da mesma forma, as ferramentas de R associadas à instância padrão seriam localizadas nesta pasta por padrão `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`:.

Os pacotes de R adicionados pela Microsoft para cargas de trabalho paralelas e distribuídas incluem as bibliotecas a seguir.

| Biblioteca | Descrição |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | Dá suporte a objetos de fonte de dados e exploração de dados, manipulação, transformação e visualização. Ele dá suporte à criação de contextos de computação remota, bem como a vários modelos escalonáveis de aprendizado de máquina, como o **rxLinMod**. As APIs foram otimizadas para analisar conjuntos de dados que são grandes demais para caber na memória e executar cálculos distribuídos em vários processadores ou núcleos. O pacote RevoScaleR também dá suporte ao formato de arquivo XDF para movimentação e armazenamento mais rápidos de dados usados para análise. O formato XDF usa armazenamento colunar, é portátil e pode ser usado para carregar e manipular dados de várias fontes, incluindo texto, SPSS ou uma conexão ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contém algoritmos de aprendizado de máquina que foram otimizados para velocidade e precisão, bem como transformações em linha para trabalhar com texto e imagens. Para obter mais informações, consulte [MicrosoftML in SQL Server](../r/ref-r-microsoftml.md). | 

## <a name="using-r-in-sql-server"></a>Usando o R no SQL Server

Você pode criar o script de R usando funções base, mas para se beneficiar de vários processamentos, você deve importar os módulos **RevoScaleR** e **MicrosoftML** para o código R e, em seguida, chamar suas funções para criar modelos que são executados em paralelo. 
 
As fontes de dados com suporte incluem bancos de dados ODBC, SQL Server e formato de arquivo XDF para trocar dados com outras fontes, ou com soluções de R. Os dados de entrada devem ser tabulares. Todos os resultados de R devem ser retornados na forma de um quadro de dados.

Os contextos de computação com suporte incluem o contexto de computação local ou remoto SQL Server. Um contexto de computação remota refere-se à execução de código que começa em um computador como uma estação de trabalho, mas, em seguida, alterna a execução do script para um computador remoto. Alternar o contexto de computação requer que ambos os sistemas tenham a mesma biblioteca RevoScaleR.

Contexto de computação local, como você pode esperar, inclui a execução do código R no mesmo servidor que a instância do mecanismo de banco de dados, com o código dentro de T-SQL ou inserido em um procedimento armazenado. Você também pode executar o código de um IDE R local e fazer com que o script seja executado no computador SQL Server, definindo um contexto de computação remota.

## <a name="execution-architecture"></a>Arquitetura de execução

Os diagramas a seguir descrevem a interação de SQL Server componentes com o tempo de execução de R em cada um dos cenários com suporte: execução de script no banco de dados e execução remota de uma linha de comando do R, usando um contexto de computação SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Scripts R executados de SQL Server no banco de dados

O código R executado de SQL Server "dentro" é executado chamando-se um procedimento armazenado. Portanto, qualquer aplicativo que possa fazer uma chamada de procedimento armazenado pode iniciar a execução de código R.  Depois disso SQL Server gerencia a execução do código R, conforme resumido no diagrama a seguir.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Uma solicitação para o tempo de execução de R é indicada pelo parâmetro _@language='R'_ passado para o procedimento armazenado, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). SQL Server envia essa solicitação ao serviço Launchpad.
2. O serviço Launchpad inicia o inicializador apropriado; neste caso, RLauncher.
3. O RLauncher inicia o processo de R externo.
4. BxlServer coordena com o tempo de execução de R para gerenciar intercâmbios de dados com SQL Server e armazenamento de resultados de trabalho.
5. O satélite do SQL gerencia as comunicações sobre tarefas e processos relacionados com o SQL Server.
6. O BxlServer usa o satélite do SQL para comunicar o status e os resultados para SQL Server.
7. SQL Server obtém resultados e fecha as tarefas e os processos relacionados.

### <a name="r-scripts-executed-from-a-remote-client"></a>Scripts R executados de um cliente remoto

Ao se conectar de um cliente de ciência de dados remoto que dá suporte ao Microsoft R, você pode executar funções do R no contexto de SQL Server usando as funções RevoScaleR. Esse é um fluxo de trabalho diferente do anterior e é resumido no diagrama a seguir.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. Para funções RevoScaleR, o tempo de execução de R chama uma função de vinculação que, por sua vez, chama BxlServer.
2. O BxlServer é fornecido com o Microsoft R e é executado em um processo separado do tempo de execução do R.
3. O BxlServer determina o destino da conexão e inicia uma conexão usando o ODBC, passando as credenciais fornecidas como parte da cadeia de conexão no objeto de fonte de dados do R.
4. BxlServer abre uma conexão com a instância de SQL Server.
5. Para uma chamada de R, o serviço Launchpad é invocado, que é ativado para iniciar o iniciador apropriado, RLauncher. Depois disso, o processamento do código R é semelhante ao processo para executar o código R de T-SQL.
6. RLauncher faz uma chamada para a instância do tempo de execução do R que está instalada no computador SQL Server.
7. Os resultados são retornados ao BxlServer.
8. O satélite do SQL gerencia a comunicação com SQL Server e a limpeza de objetos de trabalho relacionados.
9. SQL Server passa os resultados de volta para o cliente.

## <a name="see-also"></a>Confira também

+ [Estrutura de extensibilidade no SQL Server](extensibility-framework.md)
+ [Extensões de aprendizado de máquina e Python no SQL Server](extension-python.md)