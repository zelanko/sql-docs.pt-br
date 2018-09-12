---
title: R e Python de Machine Learning Services no SQL Server | Microsoft Docs
description: R no SQL Server e o Python no SQL Server, a integração com dados relacionais para ciência de dados e modelagem estatística, modelos de aprendizado de máquina, análise preditiva, visualização de dados e muito mais.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cf67348b703677035435e54c323334478a1dfdf4
ms.sourcegitcommit: a083e9d59e2014a06cda9138b7e17c17ecab90e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2018
ms.locfileid: "44343103"
---
# <a name="machine-learning-services-r-python-in-sql-server-2017"></a>Serviços de Machine Learning (R, Python) no SQL Server 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Serviços de aprendizado de máquina do SQL Server 2017 é um complemento a uma instância do mecanismo de banco de dados, usado para executar código R e Python no SQL Server. Código é executado em uma estrutura de extensibilidade, isolados dos principais processos de mecanismo, mas totalmente disponíveis para dados relacionais, como procedimentos armazenados, como o script T-SQL que contém instruções de R ou Python ou como código R ou Python, que contém o T-SQL. 

Se você usou anteriormente [SQL Server 2016 R Services](r/sql-server-r-services.md), serviços de Machine Learning no SQL Server 2017 é a próxima geração do suporte a R, com as versões atualizadas do MicrosoftML R, RevoScaleR, base, e outras bibliotecas introduzidos em 2016.

A proposição de valor de chave dos serviços de Machine Learning é a potência de sua empresa R e pacotes do Python para fornecer análise avançada em escala e a capacidade de trazer os cálculos e processamento para onde os dados residem, eliminando a necessidade de efetuar pull de dados em a rede.

## <a name="components"></a>Componentes

O SQL Server 2017 oferece suporte às linguagens R e Python. A tabela a seguir descreve os componentes.

| Componente | Description |
|-----------|-------------|
| Serviço do Launchpad do SQL Server | Um serviço que gerencia a comunicação entre os tempos de execução de R e Python externos e a instância do mecanismo de banco de dados. |
| Pacotes de R | [**RevoScaleR** ](r/revoscaler-overview.md) é a biblioteca principal para funções de R. escalonável nessa biblioteca estão entre mais amplamente usados. Transformações de dados e manipulação, resumo estatístico, visualização e muitas formas de modelagem e as análises são encontradas nessas bibliotecas. Além disso, funções nessas bibliotecas distribuir automaticamente as cargas de trabalho entre os núcleos disponíveis para processamento paralelo, com a capacidade de trabalhar em partes de dados que são coordenados e gerenciados pelo mecanismo de cálculo.  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto. <br/>[**sqlRUtils** ](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) fornece funções auxiliares para colocar os scripts do R em um procedimento armazenado T-SQL, registrando um procedimento armazenado com um banco de dados e executar o procedimento armazenado de um ambiente de desenvolvimento de R.<br/>[**olapR** ](r/how-to-create-mdx-queries-using-olapr.md) é para criar ou executar uma consulta MDX no script R.|
| Microsoft R Open MRO) | [**MRO** ](https://mran.microsoft.com/open) é a distribuição do código-fonte aberto da Microsoft do R. O pacote e o interpretador são incluídos. Sempre use a versão do MRO instalado pela instalação. |
| Ferramentas do R | Janelas do console de R e prompts de comando são ferramentas padrão em uma distribuição de R.  |
| Exemplos de R e scripts |  Pacotes de R e RevoScaleR do código-fonte aberto incluem conjuntos de dados internos para que você pode criar e executar o script usando os dados previamente instalados. |
| Pacotes do Python | [**revoscalepy** ](python/what-is-revoscalepy.md) é a biblioteca principal para o Python escalonável com funções de manipulação de dados, transformação, visualização e análise. <br/>[**microsoftml (Python)** ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto.  |
| Ferramentas do Python | A ferramenta de linha de comando interna do Python é útil para testar ad hoc e tarefas.  |
| Anaconda | O anaconda é uma distribuição de software livre de Python e pacotes essenciais. |
| Scripts e exemplos de Python | Assim como acontece com R, Python inclui conjuntos de dados internos e scripts.  |
| Modelos previamente treinados em R e Python | Modelos previamente treinados são criados para casos de uso específicos e mantidos pela equipe de engenharia de ciência de dados na Microsoft. Você pode usar os modelos previamente treinados como-é a pontuação de sentimento negativo positivo em texto ou detectar recursos em imagens usando as novas entradas de dados que você fornecer. Os modelos de execução nos serviços de aprendizado de máquina, mas não podem ser instalados pela instalação do SQL Server. Para obter mais informações, consulte [Install previamente treinado modelos de machine learning no SQL Server](install/sql-pretrained-models-install.md). |

## <a name="using-sql-mls"></a>Usando SQL MLS

Analistas e desenvolvedores geralmente têm código em execução na parte superior de uma instância do SQL Server local. Adicionando serviços de Machine Learning e habilitar a execução do script externo, você ganha a capacidade de executar código R e Python em modalidades de SQL Server: encapsular o script em procedimentos armazenados, armazenar modelos em uma tabela do SQL Server ou a combinação de funções de R ou Python e T-SQL em consultas.

Execução do script está dentro dos limites do modelo de segurança de dados: permissões no banco de dados relacional são a base de acesso a dados em seu script. Um usuário que está executando o script de R ou Python não deve ser capaz de usar todos os dados que não pôde ser acessados pelo usuário em uma consulta SQL. Você precisa de permissões de gravação e a leitura do banco de dados padrão, além de uma permissão adicional para executar o script externo. Modelos e o código que você escreve para dados relacionais são encapsulados em procedimentos armazenados, ou serializados em formato binário e armazenados em uma tabela ou carregados do disco, se você o fluxo de bytes brutos em um arquivo serializado.

A abordagem mais comum para análise no banco de dados é usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), passando o script de R ou Python como um parâmetro de entrada.

Interações de cliente-servidor clássico são outra abordagem. De qualquer estação de trabalho cliente que tenha um IDE, você pode instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) ou o [bibliotecas Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)e, em seguida, escrever um código que envia por push de execução (conhecido como um *computação remota contexto*) para dados e operações para um SQL Server remoto. 

Por fim, se você estiver usando um [servidor autônomo](r/r-server-standalone.md) e Developer edition, você pode criar soluções em uma estação de trabalho do cliente usando as mesmas bibliotecas e interpretadores e, em seguida, implantar o código de produção em aprendizado de máquina do SQL Server Serviços (no banco de dados). 

## <a name="how-to-get-started"></a>Como começar

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

+ [(No banco de dados) de serviços de aprendizado de máquina do SQL Server](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Etapa 2: Configurar uma ferramenta de desenvolvimento

Cientistas de dados geralmente usam R ou Python na estação de trabalho seu próprios laptops ou desenvolvimento, para explorar dados e criar e ajustar modelos de previsão, até que um bom modelo de previsão é obtido. Com a análise no banco de dados no SQL Server, não é necessário alterar esse processo. Após a instalação for concluída, você pode executar código R ou Python no SQL Server local e remotamente.

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **Usar o IDE que preferir**. Você pode vincular as bibliotecas de R e Python para sua ferramenta de desenvolvimento de escolha. Para obter mais informações, consulte [configurar ferramentas do R](r/set-up-a-data-science-client.md) e [configurar ferramentas Python](python/setup-python-client-tools-sql.md).  

+ **Trabalhar remotamente ou localmente**. Os cientistas de dados podem se conectar ao SQL Server e trazer os dados para o cliente para análise local, como de costume. No entanto, uma solução melhor é usar o **RevoScaleR** ou **revoscalepy** APIs para enviar cálculos para o computador do SQL Server, evitando a movimentação de dados cara e insegura.

+ **Inserir scripts R ou Python em procedimentos armazenados do SQL Server**. Quando seu código totalmente é otimizado, coloque-o em um procedimento armazenado para evitar a movimentação desnecessária de dados e otimizar tarefas de processamento de dados.

### <a name="step-3-write-your-first-script"></a>Etapa 3: Escrever seu primeiro script

Chame funções de R ou Python de dentro do script T-SQL:

+ [R: Aprenda a análise de no banco de dados usando o R](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R: instruções passo a passo de ponta a ponta do com R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python: executar o Python usando o T-SQL](tutorials/run-python-using-t-sql.md)
+ [Python: Aprenda a análise de no banco de dados usando o Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

Escolha a melhor linguagem para a tarefa. R é melhor para cálculos estatísticos que são difíceis de implementar usando SQL. Para operações baseadas em conjunto em dados, aproveite a potência do SQL Server para obter o máximo desempenho. Use o mecanismo de banco de dados na memória para cálculos muito rápidos nas colunas.

### <a name="step-4-optimize-your-solution"></a>Etapa 4: Otimizar sua solução

Quando o modelo estiver pronto para ser dimensionado nos dados da empresa, o cientista de dados geralmente funciona com o desenvolvedor do DBA ou SQL para otimizar os processos, como:

+ Engenharia de recursos
+ Ingestão de dados e transformação de dados
+ Pontuação

Tradicionalmente, os cientistas de dados usando o R teve problemas com desempenho e dimensionamento, especialmente ao usar um grande conjunto de dados. Isso ocorre porque a implementação de tempo de execução comum é single-threaded e pode acomodar apenas os conjuntos de dados que cabem na memória disponível no computador local. Integração com serviços do SQL Server Machine Learning fornece vários recursos para melhorar o desempenho, com mais dados:

+ **RevoScaleR**: pacote R este contém implementações de algumas das funções R mais populares, remodeladas para oferecer paralelismo e escala. O pacote também inclui funções que aumentam ainda mais o desempenho e a escala enviando cálculos para o computador do SQL Server, que geralmente tem muito mais memória e potência computacional.

+ **revoscalepy**. Essa biblioteca Python implementa funções mais populares do RevoScaleR, como contextos de computação remota e processamento distribuído de muitos algoritmos que oferecem suporte.

Para obter mais informações sobre o desempenho, consulte este [estudo de caso de desempenho](r/performance-case-study-r-services.md) e [otimização de dados e do R](r/r-and-data-optimization-r-services.md).

### <a name="step-5-deploy-and-consume"></a>Etapa 5: Implantar e consumir

Depois que o script ou o modelo estiver pronto para uso em produção, um desenvolvedor de banco de dados pode incorporar o código ou o modelo em um procedimento armazenado para que o código R ou Python salvo pode ser chamado a partir de um aplicativo. Armazenar e executar código R do SQL Server tem muitos benefícios: você pode usar a interface conveniente do SQL Server, e todos os cálculos ocorrem no banco de dados, evitando a movimentação de dados desnecessários.

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **Seguro e extensível**. SQL Server usa uma nova arquitetura de extensibilidade que mantém seu mecanismo de banco de dados seguro e isola as sessões de R e Python. Você também tem controle sobre os usuários que podem executar scripts, e você pode especificar quais bancos de dados podem ser acessados pelo código. Você pode controlar a quantidade de recursos alocados para o tempo de execução, para evitar que cálculos imensos prejudiquem o desempenho geral do servidor.

+ **Agendamento e a auditoria**. Quando os trabalhos de script externo são executados no SQL Server, você pode controlar e auditar os dados usados por cientistas de dados. Você também pode agendar trabalhos e criar fluxos de trabalho que contêm scripts R ou Python externos, exatamente como você pode agendar qualquer trabalho T-SQL ou procedimento armazenado.

Para tirar proveito dos recursos de segurança e gerenciamento de recursos no SQL Server, o processo de implantação pode incluir estas tarefas:

+ Convertendo seu código para uma função que pode ser executados de forma ideal em um procedimento armazenado
+ Configurando a segurança e bloqueio de pacotes usados por uma tarefa específica
+ Habilitar a governança de recursos (requer a Enterprise edition)

Para obter mais informações, consulte [governança de recursos para R](r/resource-governance-for-r-services.md) e [gerenciamento de pacotes de R para SQL Server](r/install-additional-r-packages-on-sql-server.md).

## <a name="version-history"></a>Histórico de versão

Serviços de aprendizado de máquina do SQL Server 2017 é a próxima geração do SQL Server 2016 R Services, aprimoradas para incluir o Python. A tabela a seguir é uma lista completa de todas as versões do produto, desde a concepção até a versão atual. 

| Nome do produto | Versão do mecanismo | Data de liberação |
|--------------|---------|--------------|
| Serviços de Machine Learning do SQL Server 2017 (no banco de dados) | R Server 9.2.1 <br/> Servidor de Python 9.2 | Outubro de 2017 |
| SQL Server 2017 Machine Learning Server (autônomo) | R Server 9.2.1 <br/> Servidor de Python 9.2 | Outubro de 2017 |
| SQL Server 2016 R Services (no banco de dados) | R Server 9.1  | Julho de 2017  |
| SQL Server 2016 R Server (autônomo)  |  R Server 9.1 | Julho de 2017 |

Para versões de pacote por versão, consulte a versão mapear [componentes atualizar R e Python](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md#version-map).

## <a name="portability-and-related-products"></a>Portabilidade e produtos relacionados

Portabilidade do código do R e Python personalizado é tratada por meio de distribuição de pacote e intérpretes que são criados em vários produtos. Os mesmos pacotes que são fornecidos no SQL Server também estão disponíveis em vários outros produtos e serviços Microsoft, incluindo uma versão de não-SQL chamada [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/). 

Clientes livres que incluem nossa interpretadores de R e Python estão [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) e o [bibliotecas Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

No Azure, pacotes R e Python e interpretadores da Microsoft também estão disponíveis no Azure Machine Learning e serviços do Azure, como [HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight), e [máquinas virtuais do Azure](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux). O [máquina de Virtual de ciência de dados](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) inclui uma estação de trabalho de desenvolvimento totalmente equipado com ferramentas de vários fornecedores, bem como as bibliotecas e interpretadores da Microsoft.

## <a name="see-also"></a>Confira também

[Instalar serviços de aprendizado de máquina do SQL Server](install/sql-machine-learning-services-windows-install.md)