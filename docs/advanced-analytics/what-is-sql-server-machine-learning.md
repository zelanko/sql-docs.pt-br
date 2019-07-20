---
title: Visão geral do SQL Server Serviços de Machine Learning (R, Python)
description: Visão geral do recurso de Serviços de Machine Learning no SQL Server, onde você pode integrar o Python e o R com dados relacionais para ciência de dados e modelagem estatística, modelos de aprendizado de máquina, análise preditiva, visualização de dados e muito mais.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
ms.openlocfilehash: f2bea677d6b87d7baa78fed28be82252c52a74c9
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345813"
---
# <a name="sql-server-machine-learning-services-r-python"></a>SQL Server Serviços de Machine Learning (R, Python)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Serviços de Machine Learning é um recurso do SQL Server, usado para executar scripts R e Python no banco de dados. O recurso inclui [pacotes Microsoft R e Python](#components) para análise preditiva de alto desempenho e aprendizado de máquina. Os dados relacionais podem ser usados em scripts R e Python por meio de procedimentos armazenados, script T-SQL contendo instruções R e Python ou código de R e Python que contém o T-SQL.

Se você usou anteriormente [SQL Server 2016 R Services](r/sql-server-r-services.md), Serviços de Machine Learning no SQL Server 2017 e posteriores é a próxima geração de suporte a R, com versões atualizadas de base r, RevoScaleR, MicrosoftML e outras bibliotecas introduzidas no 2016.

No banco de dados SQL do Azure, o [serviços de Machine Learning (com R)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) está atualmente em visualização pública.

## <a name="bring-compute-power-to-the-data"></a>Traga poder de computação para os dados

A principal proposta de valor da Serviços de Machine Learning é a potência de seus pacotes Enterprise R e Python para fornecer análises avançadas em escala e a capacidade de trazer cálculos e processamento para onde residem os dados, eliminando a necessidade de efetuar pull de dados a rede. Isso fornece várias vantagens:

+ Segurança de dados. Levar a uma execução de R e Python mais perto da fonte de dados evita desperdício ou insegurança de movimentação de dados.
+ Velocidade. Os bancos de dados são otimizados para operações baseadas em conjunto. Inovações recentes em bancos de dados, como tabelas na memória, tornam resumos e agregações relâmpagos e são um complemento perfeito para a ciência do dado.
+ Facilidade de implantação e integração. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]é o ponto central de operações para muitas outras tarefas e aplicativos de gerenciamento de dados. Usando dados que residem no banco de dados ou no depósito de relatórios, você garante que os dados usados pelas soluções de aprendizado de máquina sejam consistentes e atualizados. 
+ Eficiência na nuvem e no local. Em vez de processar dados em sessões de R ou Python, você pode contar com pipelines de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dados corporativos, incluindo e Azure data Factory. Comunicar resultados ou análises é fácil com o Power BI ou o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].

Usando a combinação certa de SQL e R para processamento de dados e tarefas analíticas diferentes, desenvolvedores e cientistas de dados podem ser mais produtivos.

<a name="components"></a>

## <a name="components"></a>Componentes

O SQL Server 2017 oferece suporte às linguagens R e Python. A tabela a seguir descreve os componentes do.

| Componente | Descrição |
|-----------|-------------|
| Serviço de SQL Server Launchpad | Um serviço que gerencia as comunicações entre os tempos de execução externos do R e do Python e a instância do mecanismo de banco de dados. |
| Pacotes do R | [**RevoScaleR**](r/ref-r-revoscaler.md) é a biblioteca principal para R escalonáveis. as funções nessa biblioteca estão entre as mais amplamente usadas. Transformações e manipulação de dados, Resumo Estatístico, visualização e muitas formas de modelagem e análise são encontrados nessas bibliotecas. Além disso, as funções nessas bibliotecas distribuem automaticamente cargas de trabalho entre núcleos disponíveis para processamento paralelo, com a capacidade de trabalhar em partes de dados que são coordenadas e gerenciadas pelo mecanismo de cálculo.  <br/>O [**MicrosoftML (R)** ](r/ref-r-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. <br/>o [**sqlRUtils**](r/ref-r-sqlrutils.md) fornece funções auxiliares para colocar scripts R em um procedimento armazenado T-SQL, registrar um procedimento armazenado com um banco de dados e executar o procedimento armazenado de um ambiente de desenvolvimento de R.<br/>[**olapr**](r/ref-r-olapr.md) é para compilar ou executar uma consulta MDX no script R.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) é a distribuição de R de código aberto da Microsoft. O pacote e o intérprete estão incluídos. Sempre use a versão do MRO instalada pela instalação. |
| Ferramentas de R | As janelas do console R e os prompts de comando são ferramentas padrão em uma distribuição do R.  |
| Scripts e exemplos de R |  Os pacotes R e RevoScaleR de software livre incluem conjuntos de dados internos para que você possa criar e executar scripts usando dados pré-instalados. |
| Pacotes do Python | [**revoscalepy**](python/ref-py-revoscalepy.md) é a biblioteca principal para Python escalonável com funções para manipulação, transformação, visualização e análise de dados. <br/>o [**microsoftml (Python)** ](python/ref-py-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos.  |
| Ferramentas Python | A ferramenta de linha de comando interna do Python é útil para tarefas e testes ad hoc.  |
| Anaconda | O Anaconda é uma distribuição de software livre de pacotes do Python e essenciais. |
| Exemplos e scripts do Python | Assim como acontece com o R, o Python inclui conjuntos de dados internos e scripts.  |
| Modelos pré-treinados em R e Python | Modelos pré-treinados são criados para casos de uso específicos e mantidos pela equipe de engenharia de ciência de dados na Microsoft. Você pode usar os modelos pré-treinados como estão para pontuar sentimentos positivos e negativos no texto ou detectar recursos em imagens, usando novas entradas de dados que você fornecer. Os modelos são executados no Serviços de Machine Learning, mas não podem ser instalados por meio da instalação do SQL Server. Para obter mais informações, consulte [instalar modelos de aprendizado de máquina pré-treinados em SQL Server](install/sql-pretrained-models-install.md). |

## <a name="using-sql-mls"></a>Usando o SQL MLS

Os desenvolvedores e analistas geralmente têm código em execução sobre uma instância de SQL Server local. Ao adicionar Serviços de Machine Learning e habilitar a execução de script externo, você obterá a capacidade de executar o código R e Python em SQL Server modalidades: encapsulando o script em procedimentos armazenados, armazenando modelos em uma tabela SQL Server ou combinando funções T-SQL e R ou Python em consultas.

A execução do script está dentro dos limites do modelo de segurança de dados: as permissões no banco de dados relacional são a base do acesso a dados em seu script. Um usuário executando um script R ou Python não deve ser capaz de usar nenhum dado que não possa ser acessado por esse usuário em uma consulta SQL. Você precisa das permissões de leitura e gravação do banco de dados padrão, além de uma permissão adicional para executar o script externo. Os modelos e o código que você escreve para dados relacionais são encapsulados em procedimentos armazenados, ou serializados para um formato binário e armazenados em uma tabela, ou carregados do disco se você serializasse o fluxo de bytes brutos para um arquivo.

A abordagem mais comum para análise no banco de dados é usar o [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), passando o script R ou Python como um parâmetro de entrada.

As interações clássicas de cliente-servidor são outra abordagem. Em qualquer estação de trabalho cliente que tenha um IDE, você pode instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) ou as [bibliotecas Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)e, em seguida, escrever o código que envia a execução (conhecida como um *contexto de computação remota*) para dados e operações em um SQL Server remoto. 

Por fim, se você estiver usando um [servidor autônomo](r/r-server-standalone.md) e a edição Developer, poderá criar soluções em uma estação de trabalho cliente usando as mesmas bibliotecas e intérpretes e, em seguida, implantar o código de produção em SQL Server serviços de Machine Learning (no banco de dados). 

## <a name="how-to-get-started"></a>Como começar

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

+ [SQL Server Serviços de Machine Learning (no banco de dados)](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Etapa 2: Configurar uma ferramenta de desenvolvimento

Os cientistas de dados normalmente usam R ou Python em sua própria estação de trabalho de laptop ou de desenvolvimento, para explorar dados e criar e ajustar modelos de previsão até que um bom modelo de previsão seja obtido. Com a análise no banco de dados no SQL Server, não é necessário alterar esse processo. Após a conclusão da instalação, você pode executar o código R ou Python no SQL Server local e remotamente.

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **Use o IDE que preferir**. Você pode vincular as bibliotecas R e Python à sua ferramenta de desenvolvimento de sua escolha. Para obter mais informações, consulte [Configurar ferramentas de R](r/set-up-a-data-science-client.md) e [Configurar ferramentas Python](python/setup-python-client-tools-sql.md).  

+ **Trabalhe remotamente ou localmente**. Os cientistas de dados podem se conectar a SQL Server e trazer os dados para o cliente para análise local, como de costume. No entanto, uma solução melhor é usar as APIs **RevoScaleR** ou **revoscalepy** para enviar cálculos para o computador SQL Server, evitando uma movimentação de dados dispendiosa e insegura.

+ **Insira scripts R ou Python em SQL Server procedimentos armazenados**. Quando seu código estiver totalmente otimizado, coloque-o em um procedimento armazenado para evitar a movimentação de dados desnecessária e otimizar as tarefas de processamento de dados.

### <a name="step-3-write-your-first-script"></a>Etapa 3: Escreva seu primeiro script

Chamar funções de R ou Python de dentro do script T-SQL:

+ [D Aprenda sobre análise no banco de dados usando o R](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [D Instruções completas de ponta a ponta com R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python Executar o Python usando o T-SQL](tutorials/run-python-using-t-sql.md)
+ [Python Aprenda sobre análise no banco de dados usando Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

Escolha o melhor idioma para a tarefa. O R é melhor para cálculos estatísticos que são difíceis de implementar usando SQL. Para operações baseadas em conjunto sobre dados, aproveite o poder da SQL Server para alcançar o desempenho máximo. Use o mecanismo de banco de dados na memória para computações muito rápidas sobre colunas.

### <a name="step-4-optimize-your-solution"></a>Etapa 4: Otimize sua solução

Quando o modelo está pronto para ser dimensionado em dados corporativos, o cientista de dados geralmente trabalha com o DBA ou o desenvolvedor do SQL para otimizar processos como:

+ Engenharia de recursos
+ Ingestão de dados e transformação de dados
+ Classificação

Tradicionalmente, os cientistas de dados que usam o R tiveram problemas com o desempenho e a escala, especialmente ao usar um grande conjunto de dados. Isso ocorre porque a implementação de tempo de execução comum é de thread único e pode acomodar somente os conjuntos de dados que se encaixam na memória disponível no computador local. A integração com o SQL Server Serviços de Machine Learning fornece vários recursos para melhor desempenho, com mais dados:

+ **RevoScaleR**: Este pacote R contém implementações de algumas das funções R mais populares, reprojetadas para fornecer paralelismo e escala. O pacote também inclui funções que aumentam ainda mais o desempenho e a escala enviando computações para o computador SQL Server, que normalmente tem muito mais memória e capacidade computacional.

+ **revoscalepy**. Essa biblioteca do Python implementa as funções mais populares no RevoScaleR, como contextos de computação remota e muitos algoritmos que dão suporte ao processamento distribuído.

Para obter mais informações sobre o desempenho, consulte este [estudo de caso de desempenho](r/performance-case-study-r-services.md) e otimização de dados e [R](r/r-and-data-optimization-r-services.md).

### <a name="step-5-deploy-and-consume"></a>Etapa 5: Implantar e consumir

Depois que o script ou o modelo estiver pronto para uso em produção, um desenvolvedor de banco de dados poderá inserir o código ou o modelo em um procedimento armazenado para que o código R ou Python salvo possa ser chamado a partir de um aplicativo. O armazenamento e a execução do código R a partir de SQL Server tem muitos benefícios: você pode usar a interface de SQL Server conveniente e todos os cálculos ocorrem no banco de dados, evitando a movimentação desnecessária.

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **Seguro e extensível**. O SQL Server usa uma nova arquitetura de extensibilidade que mantém o mecanismo de banco de dados seguro e isola as sessões de R e Python. Você também tem controle sobre os usuários que podem executar scripts e pode especificar quais bancos de dados podem ser acessados pelo código. Você pode controlar a quantidade de recursos alocados para o tempo de execução, a fim de evitar que computações maciças estejam em risco ao desempenho geral do servidor.

+ **Agendamento e auditoria**. Quando os trabalhos de script externo são executados no SQL Server, você pode controlar e auditar os dados usados por cientistas de dados. Você também pode agendar trabalhos e criar fluxos de trabalho que contenham scripts R ou Python externos, assim como você agendaria qualquer outro trabalho ou procedimento armazenado do T-SQL.

Para aproveitar os recursos de gerenciamento de recursos e segurança no SQL Server, o processo de implantação pode incluir estas tarefas:

+ Convertendo seu código para uma função que pode ser executada de forma ideal em um procedimento armazenado
+ Configurando os pacotes de segurança e bloqueio usados por uma tarefa específica
+ Habilitando a governança de recursos (requer a Enterprise Edition)

Para obter mais informações, consulte [governança de recursos para r](r/resource-governance-for-r-services.md) e [r gerenciamento de pacotes para SQL Server](r/install-additional-r-packages-on-sql-server.md).

## <a name="version-history"></a>Histórico de versão

SQL Server 2017 Serviços de Machine Learning é a próxima geração de SQL Server 2016 R Services, aprimorado para incluir o Python. A tabela a seguir é uma lista completa de todas as versões do produto, desde o início até a versão atual. 

| Nome do produto | Versão do mecanismo | Data de liberação |
|--------------|---------|--------------|
| SQL Server 2017 Serviços de Machine Learning (no banco de dados) | 9\.2.1 do R Server <br/> Servidor Python 9,2 | Outubro de 2017 |
| SQL Server 2017 Machine Learning Server (autônomo) | 9\.2.1 do R Server <br/> Servidor Python 9,2 | Outubro de 2017 |
| SQL Server 2016 R Services (no banco de dados) | R Server 9,1  | Julho de 2017  |
| SQL Server servidor R 2016 (autônomo)  |  R Server 9,1 | Julho de 2017 |

Para versões de pacote por versão, consulte o mapa de versão em [componentes R e Python de atualização](install/upgrade-r-and-python.md#version-map).

## <a name="portability-and-related-products"></a>Portabilidade e produtos relacionados

A portabilidade do seu código R e Python personalizado é abordada por meio da distribuição de pacotes e de intérpretes criados em vários produtos. Os mesmos pacotes fornecidos no SQL Server também estão disponíveis em vários outros produtos e serviços da Microsoft, incluindo uma versão não SQL chamada [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/). 

Os clientes gratuitos que incluem nossos interpretadores R e Python são [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) e as [bibliotecas do Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

No Azure, os pacotes e intérpretes de R e Python da Microsoft também estão disponíveis em Azure Machine Learning, e serviços do Azure como o [HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview)e [máquinas virtuais do Azure](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux). O [máquina virtual de ciência de dados](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) inclui uma estação de trabalho de desenvolvimento totalmente equipada com ferramentas de vários fornecedores, bem como as bibliotecas e os intérpretes da Microsoft.

## <a name="see-also"></a>Confira também

[Instalar SQL Server Serviços de Machine Learning](install/sql-machine-learning-services-windows-install.md)
