---
title: Extensão do R no SQL Server | Microsoft Docs
description: Saiba mais sobre a execução de código do R e bibliotecas do R internos no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: af71b03238a744702288f1f7411a5ebec3911f60
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892847"
---
# <a name="r-extension-in-sql-server"></a>Extensão do R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A extensão de R é parte do complemento serviços do SQL Server Machine Learning para o mecanismo de banco de dados relacional. Ele adiciona um ambiente de execução de R, a distribuição de R base com bibliotecas padrão e ferramentas e as bibliotecas do R da Microsoft: [RevoScaleR](../r/revoscaler-overview.md) para análise em grande escala, [MicrosoftML](../using-the-microsoftml-package.md) para aprendizado de máquina algoritmos e outras bibliotecas para acessar dados ou código R no SQL Server.

Integração do R está disponível no SQL Server a partir do SQL Server 2016, [R Services](../r/sql-server-r-services.md)e continuando adiante como parte da [serviços de Machine Learning do SQL Server](../what-is-sql-server-machine-learning.md).

## <a name="r-components"></a>Componentes do R

O SQL Server inclui pacotes de software livre e proprietários. As bibliotecas de R base são instaladas por meio da distribuição da Microsoft de software livre r: R abrir MRO (Microsoft). Os usuários atuais do R devem ser capazes de portar seu código do R e executá-lo como um processo externo no SQL Server com poucas ou nenhuma modificação. MRO é instalado, independentemente das ferramentas do SQL e é executado fora do principais processos de mecanismo, na estrutura de extensibilidade. Durante a instalação, você deve concordar com os termos da licença de software livre. Depois disso, você pode executar pacotes de R padrão sem modificações adicionais como faria em qualquer outra distribuição de software livre do R. 

SQL Server não modifica os executáveis de R base, mas você deve usar a versão do R instalado pela instalação porque essa versão é o que os pacotes de proprietários são criados e testados em. Para obter mais informações sobre como o MRO difere de uma distribuição de base do R que você pode obter do CRAN, consulte [interoperabilidade com linguagem R e recursos e produtos do Microsoft R](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

A distribuição de pacote básico de R instalada pelo programa de instalação pode ser encontrada na pasta associada à instância. Por exemplo, se você instalou o R Services em uma instância do SQL Server 2016 padrão, as bibliotecas do R estão localizadas nesta pasta por padrão: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`. Da mesma forma, as ferramentas do R associadas à instância padrão seriam localizadas nesta pasta por padrão: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`.

Pacotes de R adicionados pela Microsoft para cargas de trabalho paralelas e distribuídas incluem as seguintes bibliotecas.

| Biblioteca | Description |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | Dá suporte à visualização e exploração de dados, manipulação, transformação e objetos de fonte de dados. Ele dá suporte à criação de contextos de computação remota, bem como um vários modelos de aprendizado de máquina escalonáveis, tais como **rxLinMod**. As APIs foram otimizadas para analisar conjuntos de dados que são grandes demais para caber na memória e executar cálculos distribuídos em vários processadores ou núcleos. O pacote RevoScaleR também suporta o formato de arquivo XDF para movimentação e armazenamento de dados usados para análise mais rápidos. O formato XDF usa armazenamento colunar, é portátil e pode ser usado para carregar e manipular dados de várias fontes, incluindo texto, SPSS ou uma conexão ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contém algoritmos de aprendizado de máquina que foram otimizados para velocidade e precisão, bem como as transformações para trabalhar com imagens e texto em linha. Para obter mais informações, consulte [usando o pacote MicrosoftML com o SQL Server](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package). | 

## <a name="using-r-in-sql-server"></a>Usando o R no SQL Server

Você pode criar scripts R usando funções de base, mas para se beneficiar de multiprocessamento, você deve importar o **RevoScaleR** e **MicrosoftML** módulos no seu código R e, em seguida, chame suas funções para criar modelos que Execute em paralelo. 
 
Fontes de dados com suporte incluem bancos de dados ODBC, o SQL Server e o formato de arquivo XDF para trocar dados com outras fontes, ou com soluções de R. Dados de entrada devem ser tabulares. Todos os resultados de R devem ser retornados na forma de um quadro de dados.

Contextos de computação com suporte incluem o contexto de computação do SQL Server local ou remoto. Um contexto de computação remota refere-se a execução de código que começa em um computador, como uma estação de trabalho, mas, em seguida, opções de execução de um script para um computador remoto. Alternar o contexto de computação requer que ambos os sistemas tenham a mesma biblioteca RevoScaleR.

Contexto de computação local, como você pode esperar, inclui a execução de código do R no mesmo servidor como a instância do mecanismo de banco de dados, com o código de T-SQL ou inserido em um procedimento armazenado. Você também pode executar o código de um IDE R local e têm o script executado no computador do SQL Server, o contexto de computação com a definição de um controle remoto.

## <a name="execution-architecture"></a>Arquitetura de execução

O diagrama a seguir mostra a interação de componentes do SQL Server com o tempo de execução de R em cada um dos cenários com suporte: em execução a execução do script no banco de dados e remotos em uma linha de comando de R, usando um contexto de computação do SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Scripts R executados do SQL Server no banco de dados

Código de R que é executado em "inside" do SQL Server é executado chamando um procedimento armazenado. Portanto, qualquer aplicativo que possa fazer uma chamada de procedimento armazenado pode iniciar a execução de código R.  Depois do SQL Server gerencia a execução de código de R, conforme resumido no diagrama a seguir.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Uma solicitação para o tempo de execução de R é indicada pelo parâmetro _@language='R'_ passado para o procedimento armazenado, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). SQL Server envia essa solicitação ao serviço Launchpad.
2. O serviço Launchpad inicia o inicializador apropriado; neste caso, RLauncher.
3. O RLauncher inicia o processo de R externo.
4. O BxlServer coordena com o tempo de execução de R para gerenciar a troca de dados com o SQL Server e o armazenamento de resultados do trabalho.
5. Satélite SQL gerencia comunicações sobre processos com o SQL Server e tarefas relacionadas.
6. O BxlServer usa satélite SQL para se comunicar o status e os resultados para o SQL Server.
7. SQL Server obtém resultados e fecha os processos e tarefas relacionadas.

### <a name="r-scripts-executed-from-a-remote-client"></a>Scripts R executados de um cliente remoto

Ao conectar-se de um cliente de ciência de dados remotos que dá suporte ao Microsoft R, você pode executar funções do R no contexto do SQL Server usando as funções de RevoScaleR. Esse é um fluxo de trabalho diferente do anterior e é resumido no diagrama a seguir.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. Para funções de RevoScaleR, o tempo de execução do R chama uma função de vinculação que por sua vez, chama BxlServer.
2. O BxlServer é fornecido com o Microsoft R e é executado em um processo separado do tempo de execução do R.
3. O BxlServer determina o destino da conexão e inicia uma conexão usando o ODBC, passando as credenciais fornecidas como parte da cadeia de conexão no objeto de fonte de dados do R.
4. O BxlServer abre uma conexão à instância do SQL Server.
5. Para uma chamada de R, o serviço Launchpad é chamado, o que é a vez inicia o inicializador apropriado, RLauncher. Depois disso, o processamento do código R é semelhante ao processo para executar o código R de T-SQL.
6. O RLauncher faz uma chamada para a instância do tempo de execução de R instalado no computador do SQL Server.
7. Os resultados são retornados ao BxlServer.
8. Satélite SQL gerencia a comunicação com o SQL Server e a limpeza dos objetos de trabalho relacionados.
9. SQL Server passa os resultados ao cliente.

## <a name="see-also"></a>Confira também

+ [Estrutura de extensibilidade no SQL Server](extensibility-framework.md)
+ [Python e extensões no SQL Server de aprendizado de máquina](extension-python.md)