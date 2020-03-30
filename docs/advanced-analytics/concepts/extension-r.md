---
title: Extensão da linguagem R
description: Saiba mais sobre a execução de código R e bibliotecas R internas nos SQL Server R Services ou nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98ef57702b01a3f32babd6b0ac9b64fb3c22e9ea
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727654"
---
# <a name="r-language-extension-in-sql-server"></a>Extensão da linguagem R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A extensão R faz parte do complemento Serviços de Machine Learning do SQL Server para o mecanismo de banco de dados relacional. Ela adiciona um ambiente de execução de R, uma distribuição de R base com bibliotecas e ferramentas padrão e as bibliotecas do Microsoft R: [RevoScaleR](../r/ref-r-revoscaler.md) para análise em escala, [MicrosoftML](../r/ref-r-microsoftml.md) para algoritmos de aprendizado de máquina e outras bibliotecas para acessar dados ou código R no SQL Server.

A integração do R está disponível no [SQL Server R Services](../r/sql-server-r-services.md) e nos [Serviços de Machine Learning do SQL Server](../what-is-sql-server-machine-learning.md).

## <a name="r-components"></a>Componentes R

O SQL Server inclui pacotes de software livre e proprietários. As bibliotecas de R base são instaladas por meio da distribuição de R de software livre da Microsoft: MRO (Microsoft R Open). Os usuários atuais de R devem ser capazes de portar seu código R e executá-lo como um processo externo em SQL Server com poucas ou nenhuma modificação. O MRO é instalado independentemente das ferramentas SQL e é executado fora dos processos do mecanismo principal, na estrutura de extensibilidade. Durante a instalação, você deve consentir com os termos da licença de software livre. Depois disso, você poderá executar pacotes R padrão sem modificações adicionais como faria em qualquer outra distribuição de software livre de R. 

O SQL Server não modifica os executáveis de R base, mas você deve usar a versão do R instalada pela Instalação, pois essa versão é aquela na qual os pacotes proprietários são compilados e testados. Para obter mais informações sobre como o MRO difere de uma distribuição base de R que você pode obter do CRAN, confira [Interoperabilidade com a linguagem R e os produtos e recursos do Microsoft R](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

A distribuição do pacote base de R configurada pela Instalação pode ser encontrada na pasta associada à instância. Por exemplo, se você tiver instalado o R Services na instância padrão do SQL Server, as bibliotecas de R estarão localizadas nesta pasta por padrão: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`. Da mesma forma, as ferramentas de R associadas à instância padrão deverão estar localizadas nesta pasta por padrão: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`.

Os pacotes de R adicionados pela Microsoft para cargas de trabalho paralelas e distribuídas incluem as bibliotecas a seguir.

| Biblioteca | Descrição |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | É compatível com objetos de fonte de dados e exploração, manipulação, transformação e visualização de dados. Ele é compatível com a criação de contextos de computação remota, bem como com vários modelos de machine learning escalonáveis, como **rxLinMod**. As APIs foram otimizadas para analisar conjuntos de dados que são grandes demais para caber na memória e executar cálculos distribuídos em vários processadores ou núcleos. O pacote RevoScaleR também é compatível com o formato de arquivo XDF para movimentação e armazenamento mais rápidos de dados usados para análise. O formato XDF usa armazenamento colunar, é portátil e pode ser usado para carregar e manipular dados de várias fontes, incluindo texto, SPSS ou uma conexão ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contém algoritmos de aprendizado de máquina que foram otimizados para velocidade e precisão, bem como transformações em linha para trabalhar com texto e imagens. Para obter mais informações, confira [MicrosoftML no SQL Server](../r/ref-r-microsoftml.md). | 

## <a name="using-r-in-sql-server"></a>Como usar R no SQL Server

Você pode criar o script R usando funções base, mas para se beneficiar de vários processamentos, é necessário importar os módulos **RevoScaleR** e **MicrosoftML** no código R e, em seguida, chamar as funções para criar modelos executados em paralelo. 
 
As fontes de dados compatíveis incluem bancos de dados ODBC, SQL Server e formato de arquivo XDF para trocar dados com outras fontes ou com soluções de R. Os dados de entrada devem ser tabulares. Todos os resultados de R devem ser retornados na forma de um quadro de dados.

Os contextos de computação compatíveis incluem o contexto de computação local ou remota do SQL Server. Um contexto de computação remota refere-se à execução de código que começa em um computador, como uma estação de trabalho, mas, em seguida, alterna a execução do script para um computador remoto. Alternar o contexto de computação requer que ambos os sistemas tenham a mesma biblioteca RevoScaleR.

O contexto de computação local, como você pode esperar, inclui a execução do código R no mesmo servidor que a instância do mecanismo de banco de dados, com o código dentro de T-SQL ou inserido em um procedimento armazenado. Você também pode executar o código de um IDE R local e fazer com que o script seja executado no computador SQL Server, definindo um contexto de computação remota.

## <a name="execution-architecture"></a>Arquitetura de execução

Os diagramas a seguir descrevem a interação dos componentes do SQL Server com o runtime do R em cada um dos cenários compatíveis: execução de script no banco de dados e execução remota de uma linha de comando de R, usando um contexto de computação do SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Scripts R executados do SQL Server no banco de dados

O código R que é executado de "dentro" do SQL Server é executado chamando um procedimento armazenado. Portanto, qualquer aplicativo que possa fazer uma chamada de procedimento armazenado pode iniciar a execução de código R.  Então, o SQL Server gerencia a execução de código R, conforme resumido no diagrama a seguir.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Uma solicitação para o runtime de R é indicada pelo parâmetro _@language='R'_ passado para o procedimento armazenado, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). O SQL Server envia essa solicitação para o serviço Launchpad.
No Linux, o SQL usa um serviço **Launchpad** para se comunicar com um processo Launchpad separado para cada usuário. Veja o [Diagrama da arquitetura de extensibilidade](extensibility-framework.md#architecture-diagram) para obter detalhes.
2. O serviço Launchpad inicia o inicializador apropriado; neste caso, RLauncher.
3. O RLauncher inicia o processo de R externo.
4. O BxlServer coordena-se com o runtime do R para gerenciar a troca de dados com o SQL Server e o armazenamento de resultados funcionais.
5. O Satélite SQL gerencia as comunicações sobre processos e tarefas relacionadas com o SQL Server.
6. O BxlServer usa Satélite SQL para comunicar o status e os resultados ao SQL Server.
7. O SQL Server obtém resultados e fecha os processos e tarefas relacionados.

### <a name="r-scripts-executed-from-a-remote-client"></a>Scripts R executados de um cliente remoto

Ao conectar-se de um cliente de ciência de dados remotos compatível com o Microsoft R, você pode executar funções do R no contexto do SQL Server usando as funções RevoScaleR. Esse é um fluxo de trabalho diferente do anterior e é resumido no diagrama a seguir.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. Para funções do RevoScaleR, o runtime do R chama uma função de vinculação que, por sua vez, chama o BxlServer.
2. O BxlServer é fornecido com o Microsoft R e é executado em um processo separado do runtime do R.
3. O BxlServer determina o destino da conexão e inicia uma conexão usando o ODBC, passando as credenciais fornecidas como parte da cadeia de conexão no objeto de fonte de dados do R.
4. O BxlServer abre uma conexão para a instância do SQL Server.
5. Para uma chamada do R, o serviço Launchpad é invocado e, por sua vez, inicia o inicializador apropriado, RLauncher. Depois disso, o processamento do código R é semelhante ao processo para executar o código R de T-SQL.
6. O RLauncher faz uma chamada para a instância de runtime do R instalada no computador do SQL Server.
7. Os resultados são retornados ao BxlServer.
8. O Satélite SQL gerencia a comunicação com o SQL Server e a limpeza dos objetos de trabalho relacionados.
9. O SQL Server passa os resultados de volta para o cliente.

## <a name="see-also"></a>Confira também

+ [Estrutura de extensibilidade no SQL Server](extensibility-framework.md)
+ [Extensões de aprendizado de máquina e Python no SQL Server](extension-python.md)