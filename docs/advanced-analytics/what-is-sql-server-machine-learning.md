---
title: "O que é o serviços de aprendizado de máquina do SQL Server? | Microsoft Docs"
ms.date: 03/07/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: 
ms.openlocfilehash: ccba60d0a3e0fe45f82215a045e53a265d6c0a92
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2018
---
# <a name="what-is-sql-server-machine-learning-services"></a>O que é o serviços de aprendizado de máquina do SQL Server?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Serviços de aprendizado de máquina do SQL Server é um incorporado, previsão análises e dados de ciências mecanismo que pode executar o código de R e Python dentro de um banco de dados do SQL Server, como procedimentos armazenados, como o script T-SQL que contém instruções de R ou Python ou como contendo o código R ou Python T-SQL. 

A proposição de valor de chave dos serviços de aprendizado de máquina é a potência de seus proprietários pacotes para oferecer uma análise avançada em escala e a capacidade de trazer os cálculos e processamento para onde os dados residem, eliminando a necessidade de efetuar pull de dados entre o rede.

Há duas opções para o uso de recursos de aprendizado de máquina no SQL Server: 

+ [**Serviços de aprendizado de máquina do SQL Server (no banco de dados)** ](r/sql-server-r-services.md) opera na instância do mecanismo de banco de dados, em que o mecanismo de cálculo é totalmente integrado com o mecanismo de banco de dados. A maioria das instalações são essa opção.
+ [**O servidor de aprendizado de máquina do SQL Server (autônomo)** ](r/r-server-standalone.md) é uma instalação de não-SQL. Apesar de você usar a instalação do SQL Server para instalar o servidor, ele será desacoplado completamente do SQL Server. Funcionalmente, é equivalente a não-SQL [Microsoft Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

## <a name="r-and-python-packages"></a>Pacotes de R e Python

Suporte para cada idioma é por meio de pacotes de proprietárias da Microsoft usados para criar e modelos de treinamento de vários tipos, classificação de dados e processamento paralelo usando os recursos do sistema subjacente.

Porque os pacotes proprietários baseiam-se em distribuições de software livre R e Python, script ou código que é executado no SQL Server pode também chamadas de funções de base e usar pacotes de terceiros compatíveis com a versão de idioma fornecida no SQL Server (3.5 Python e versões recentes do R, atualmente 3.3.3).

| R  | Python | Description |
|-----------|----------------|-------------|
| [RevoScaleR](r/revoscaler-overview.md) | [revoscalepy](python/what-is-revoscalepy.md)   | Funções essas bibliotecas estão entre mais amplamente utilizadas. Transformações de dados e manipulação, estatísticas de resumo, visualização e muitas formas de modelagem e análise são encontradas nessas bibliotecas. Além disso, essas bibliotecas de funções automaticamente distribuem cargas de trabalho entre núcleos disponíveis para processamento paralelo, com a capacidade de trabalhar em partes de dados coordenados e gerenciados pelo mecanismo de cálculo. |
| [MicrosoftML](using-the-microsoftml-package.md) | [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Líder de mercado algoritmos aprendizado de máquina para personalização de imagem, problemas de classificação e muito mais. |
| [olapR](r/how-to-create-mdx-queries-using-olapr.md) | none | Criar ou executar uma consulta MDX no script R.
| [sqlRUtils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) | none | Funções para colocar os scripts R em um T-SQL procedimento armazenado, registrando um procedimento armazenado com um banco de dados e a execução do procedimento armazenado de um ambiente de desenvolvimento de R.
| [mrsdeploy](operationalization-with-mrsdeploy.md) | none | Usado principalmente em uma instalação de não-SQL do servidor de aprendizado de máquina, como o [(autônomo) versão](r/r-server-standalone.md). Use esse pacote para implantar e hospedar serviços da web, topologias de expansão com web dedicada de compilação e nós de computação, alternar entre as sessões locais e remotas, execute o diagnóstico e muito mais. Para uma instalação (no banco de dados), use esse pacote em uma capacidade de cliente: por exemplo acessar um serviço da web em um servidor remoto dedicado à execução de cargas de trabalho apenas serviços de aprendizado de máquina. |

Portabilidade do código R e Python personalizado é tratada por meio de distribuição do pacote e intérpretes que são incorporados a vários produtos. Os mesmos pacotes que são fornecidos no SQL Server também estão disponíveis em vários outros produtos e serviços Microsoft, incluindo uma versão de não-SQL chamada [Microsoft Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/). Incluem clientes livres que incluem nossas interpretadores R e Pyton [o cliente do Microsoft R](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) e [bibliotecas Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

Também estão disponíveis em vários pacotes e interpretadores [máquinas virtuais do Azure](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux), aprendizado de máquina do Azure e os serviços do Azure como [HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight). 


## <a name="use-cases"></a>Casos de uso

**No banco de dados análise**

Analistas e desenvolvedores geralmente têm código em execução na parte superior de uma instância local do SQL Server. Se tiver como o SQL Server e um IDE [Visual Studio com R](https://docs.microsoft.com/visualstudio/rtvs/) ou [Visual Studio com o Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio) no mesmo computador, você pode criar, treinar e testar modelos localmente em qualquer idioma. Acesso local simplifica o gerenciamento de pacotes: como um administrador, você pode carregar outros pacotes de terceiros usando permissões internas para essa função.

A abordagem mais comum para análise no banco de dados é usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar script R ou Python. Os tutoriais listados na [próximas etapas](#next-steps) iniciarão.

**Configurações de cliente-servidor**

Em qualquer estação de trabalho cliente que tenha um IDE, instalar [o cliente do Microsoft R](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) ou [bibliotecas Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)e, em seguida, escrever código que leva a execução (conhecido como um *contexto de computação remota*) para dados e as operações em um servidor SQL remoto. 

Da mesma forma, se você estiver usando a edição de desenvolvedor, você pode criar soluções em uma estação de trabalho do cliente usando as mesmas bibliotecas e interpretadores e, em seguida, implante o código de produção nos serviços de aprendizado de máquina do SQL Server (no banco de dados). 

## <a name="version-history"></a>Histórico de versão

Serviços de aprendizado de máquina do SQL Server 2017 é a próxima geração de SQL Server 2016 R Services, aprimoradas para incluir Python. A tabela a seguir é uma lista completa de todas as versões, desde a criação para a versão atual. 

| Nome do produto | Versão do mecanismo | Data de lançamento |
|--------------|---------|--------------|
| Serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados) | R Server 9.2.1 <br/> Python Server 9.2 | Outubro de 2017 |
| Servidor de aprendizado de máquina do SQL Server de 2017 (autônomo) | R Server 9.2.1 <br/> Python Server 9.2 | Outubro de 2017 |
| SQL Server 2016 R Services (no banco de dados) | R Server 9.1  | Julho de 2017  |
| SQL Server 2016 R Server (autônomo)  |  R Server 9.1 | Julho de 2017 |



## <a name="documentation-for-each-version"></a>Documentação para cada versão

Versões recentes de documentação do SQL Server são independentes de versão. Para serviços de aprendizado de máquina do SQL Server, Python só está disponível em 2017 e posterior, enquanto o suporte de R está em todas as versões. A menos que indicado de outra forma, você pode presumir documentação R se aplica a versões de 2016 e 2017.


## <a name="related-machine-learning-products"></a>Produtos de aprendizado de máquina relacionada

 +  [Provisionar uma máquina Virtual do Azure](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  O Azure marketplace inclui várias imagens de máquina virtual que incluem o servidor de aprendizado de máquina ou R. Criar uma máquina virtual no Microsoft Azure é a maneira mais rápida de obter para desenvolvimento e implantação de modelos de previsão. Imagens vêm com recursos para o dimensionamento e compartilhamento já configurado, que torna mais fácil para inserir a análise de dentro de aplicativos e a integração com sistemas de back-end.

+ [Máquinas virtuais de ciência de dados](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)

  A versão mais recente da máquina Virtual de ciência de dados inclui o servidor de aprendizado de máquina, SQL Server, além de uma matriz das ferramentas mais populares para aprendizado de máquina, todos os pré-instalado e testado. Criar blocos de anotações do Jupyter, desenvolver soluções em Julia e usar bibliotecas de aprendizado habilitado GPU como MXNet, CNTK e TensorFlow.

<a name="next-steps"></a>

## <a name="next-steps"></a>Próximas etapas

**Etapa 1:** instalar e configurar o software. 

+ [Instale os serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados)](install/sql-machine-learning-services-windows-install.md)

**Etapa 2:** começar com o código usando um destes tutoriais:

+ [Tutorial: Executar Python em T-SQL](tutorials/run-python-using-t-sql.md)
+ [Tutorial: Executar R no T-SQL](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

**Etapa 3:** adicionar seus pacotes de R e Python Favoritos e usá-los junto com os pacotes fornecidos pela Microsoft

+ [Gerenciamento de pacotes de R para o SQL Server](r/r-package-management-for-sql-server-r-services.md)