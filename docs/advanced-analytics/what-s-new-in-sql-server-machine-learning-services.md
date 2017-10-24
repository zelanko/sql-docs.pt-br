---
title: "O que &#39; s novo nos serviços de aprendizado de máquina | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 37f3b12dc792060b45e67264e49a4a6180167676
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="whats-new-in-machine-learning-services-in-sql-server"></a>O que há de novo nos serviços de aprendizado de máquina no SQL Server

No SQL Server 2016, a Microsoft introduziu o SQL Server R Services, um recurso que oferece suporte a ciência de dados de grande porte, integrando a linguagem R com o mecanismo de banco de dados do SQL Server.

No SQL Server de 2017, aprendizado de máquina se tornará ainda mais potente, com a adição de suporte para a linguagem Python popular. Com o suporte para novos idiomas é fornecido um novo nome: **serviços de aprendizado de máquina (no banco de dados)**.

Pegue o lançamento mais recente aqui! [Python no SQL Server 2017: aprimorada de aprendizado de máquina no banco de dados](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

[!NOTE]
> Agora você pode executar R em bancos de dados do SQL Azure! Para obter mais informações, consulte [neste artigo](r/using-r-in-azure-sql-database.md), ou este blog da equipe de desenvolvimento do SQL Server: [visualização de apresentação dos serviços de aprendizado de máquina com suporte de R no banco de dados do SQL Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-preview-of-machine-learning-services-with-r-support-in-azure-sql-database/).

## <a name="whats-new-in-sql-server-2017"></a>Novidades no SQL Server 2017

Servidor de aprendizado de máquina Microsoft no SQL Server agora fornece suporte abrangente para criar e implantar soluções de aprendizado de máquina em R ou Python. Aqui estão os destaques desta versão:

> [!IMPORTANT]
> 
> Serviços de aprendizado de máquina, incluindo o uso de R ou Python, atualmente não têm suporte durante a execução do SQL Server no Linux ou no banco de dados do SQL Azure. Procure as alterações em uma versão posterior.
> 
> Pontuação nativo usando a função de previsão é suportada atualmente na edição Linux.

### <a name="whats-new-in-cumulative-update-1-for-sql-server-2017"></a>Novidades na atualização cumulativa 1 para SQL Server 2017

Agora você pode atualizar os componentes do Python e R para o servidor de aprendizado de máquina 9.2.1. Esta versão apresenta vários aprimoramentos para **revoscalepy** e **RevoScaleR**, incluindo melhorias de desempenho.
 
### <a name="in-database-python-integration"></a>Integração de Python no banco de dados

Você pode executar o Python em procedimentos armazenados ou executar remotamente usando o computador do SQL Server como o contexto de computação de Python. Essa integração abre novos caminhos para a grande comunidade de desenvolvedores de Python e os cientistas de dados, use o poder do SQL Server. 

Os desenvolvedores do SQL Server acessar as bibliotecas Python abrangentes do ecossistema de software livre, incluindo estruturas conhecidas, como scikit-saiba, Tensorflow, Caffe e Theano/Keras. E certifique-se de explorar as inovações da Microsoft, como **revoscalepy** e **microsoftml**!

Python em execução no banco de dados não envolve apenas de aprendizado de máquina, a propósito. Há uma grande variedade de outros aplicativos potenciais para integrar o Python com SQL e usando a capacidade de cada linguagem para fornecer soluções mais inteligentes e eficientes.

+ **revoscalepy**

    Esta versão inclui a versão final do **revoscalepy**, que fornece os equivalentes de Python dos algoritmos em RevoScaleR. Você pode criar modelos de Python para árvores de decisão, regressão linear e logística, árvores aumentadas e florestas aleatórias, todos os paralelizáveis e é capazes de está sendo executado em contextos de computação remota.

    Para obter mais informações, consulte [novidades revoscalepy](python/what-is-revoscalepy.md).

+ Contextos de computação remota para Python

    Esta versão dá suporte ao uso de várias fontes de dados e contextos de computação remota. O cientista de dados ou o desenvolvedor pode executar o código Python em um servidor SQL remoto, para explorar dados ou criar modelos sem mover os dados. O uso de contextos de computação remota requer **revoscalepy**.

+ Suporte a Python no aprendizado de máquina do Microsoft Server (autônomo)

    SQL Server 2017 inclui a opção para instalar uma versão autônoma do servidor de aprendizado de máquina do Microsoft. Usando o servidor de aprendizado de máquina, você pode distribuir e dimensionar o código de R ou Python sem usar o SQL Server.

### <a name="linux-support"></a>Suporte para Linux

Aprendizado de máquina usando o R ou Python no banco de dados não é suportado atualmente no SQL Server no Linux. Procure os anúncios em uma versão posterior.

No entanto, no Linux você pode executar [pontuação nativo](sql-native-scoring.md) usando a função PREVER T-SQL. Pontuação nativo permite a pontuação de um modelo pré-treinado muito rápido, sem chamar ou até mesmo exigir um tempo de execução de R. Isso significa que você pode usar o SQL Server no Linux para gerar previsões muito rápidos, para atender a aplicativos cliente.

### <a name="new-algorithms"></a>Novos algoritmos

O **MicrosoftML** pacote de R e Python contém algoritmos de aprendizado de máquina de última geração e transformação de dados que pode ser remoto dimensionado ou executado em contextos de computação. Algoritmos incluem redes neurais profundas personalizáveis, árvores de decisão rápida e florestas de decisão, regressão linear e regressão logística.

O pacote MicrosoftML vem com interfaces de R e Python e é baseado em aprendizado de máquina do Microsoft Server versão 9.2.0.

Para obter mais informações, consulte [Introdução ao MicrosoftML](using-the-microsoftml-package.md) e [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="operationalization"></a>Operacionalização

Esta versão contém várias opções e recursos para ajudá-lo a implantar e distribuir as tarefas de aprendizado de máquina:

+ Implantar e integrar soluções de Python de máquina, usando o T-SQL

    A integração do Python com T-SQL significa que você pode chamar qualquer código Python usando `sp_execute_external_script`. Essa infraestrutura segura permite a implantação de nível empresarial de scripts que podem ser chamados a partir de um aplicativo usando um procedimento armazenado simples e modelos de Python. Desempenho adicional é por streaming de dados do SQL para paralelização do anel MPI e processos de Python.

+ **mrsdeploy** para Python

    O **mrsdeploy** do pacote para o Microsoft R Server agora dá suporte à implantação de modelos de Python e scripts, como serviços da web e está disponível como uma opção no servidor de aprendizado de máquina (autônomo). Para obter um exemplo de como isso funciona, consulte [publicar e consumir o código Python](python/publish-consume-python-code.md).

+ Desempenho

    Microsoft estende os limites de desempenho para pontuação. Com a pontuação no banco de dados, que processamos um milhão de linhas por segundo usando modelos de R. Nesta versão, novos recursos para **em tempo real de pontuação** e **pontuação nativo** dar suporte a melhor desempenho em linha única e pontuação de lote. 

### <a name="realtime-scoring-and-native-scoring"></a>Em tempo real de pontuação e pontuação nativo

A pontuação em tempo real depende de bibliotecas nativas C++ para ler um modelo armazenado em um formato binário otimizado e, em seguida, gerar previsões sem a necessidade de chamar o tempo de execução de R. Isso torna muito mais rápido de operações de pontuação.

Além disso, esta versão do SQL Server 2017 inclui uma função nativa do T-SQL para pontuação rápida que pode ser executada em qualquer edição do SQL Server, mesmo em Linux. A função não requer nenhuma instalação de R ou configuração adicional. Isso significa que você pode treinar um modelo em outro lugar, salvá-lo no SQL Server e, em seguida, executar pontuação sem nunca chamar R. Esse recurso é conhecido como _pontuação nativo_.

  - Pontuação nativo está disponível apenas no SQL Server 2017. Ele usa uma função de T-SQL que pode ser executados em qualquer edição do SQL Server, incluindo Linux.
 - Em tempo real de pontuação tem suporte no SQL Server 2017 e no servidor de aprendizado de máquina do Microsoft. Você pode executar um procedimento armazenado ou realizar em tempo real de pontuação do código R.
 - Em tempo real de pontuação também está disponível para o SQL Server 2016, se a instância é atualizada para a versão mais recente do Microsoft R Server.

Para obter mais informações, consulte estes tópicos:

 + [Em tempo real de pontuação](real-time-scoring.md)
 + [Pontuação nativa](sql-native-scoring.md)
 + [Como realizar em tempo real de pontuação ou pontuação nativo](r/how-to-do-realtime-scoring.md)

### <a name="upgrade-your-machine-learning-experience-and-get-pre-trained-models"></a>Atualizar sua experiência de aprendizado de máquina e obter modelos previamente treinados

Se você instalou uma versão anterior do SQL Server 2016 R Services, você pode atualizar agora para a versão mais recente, alternando o servidor para usar a política de ciclo de vida do Software moderno. Fazendo isso, você pode tirar proveito de um ciclo de lançamento mais rápido para R e atualizar automaticamente todos os componentes de R. Para saber mais, veja [Microsoft R Server 9.0.1](https://docs.microsoft.com/r-server/whats-new-in-r-server).

O instalador também oferece a opção para instalar uma coleção de modelos previamente treinados em formato binário. Esses modelos dão suporte a aprendizado de máquina em cenários como reconhecimento de imagem, onde podem ser difíceis de encontrar grandes conjuntos de dados para treinar um modelo. Depois de instalar um dos modelos previamente treinados, você pode usá-lo para previsão em seus próprios dados sem o tempo e as despesas envolvidas no treinamento esse modelo grande e complexo.

Para obter mais informações, consulte [instalar previamente treinados modelos no SQL Server](r/install-pretrained-models-sql-server.md)

### <a name="package-management"></a>Gerenciamento de pacotes

Esta versão inclui vários aprimoramentos no gerenciamento de pacotes do SQL Server. Eles incluem:

- funções de banco de dados para ajudar o DBA, gerenciar e permissões de auditoria
- A instrução Criar biblioteca externa no T-SQL, para ajudar a gerenciar pacotes sem precisar saber R DBAs
- Um conjunto avançado de funções de R para ajudar a instalar, remover ou listar pacotes pertencentes a usuários

Para obter mais informações, consulte [pacote de gerenciamento](r/r-package-management-for-sql-server-r-services.md).

### <a name="get-started"></a>Introdução

+ [Configurar o Python nos serviços de aprendizado de máquina do SQL Server](../advanced-analytics/python/setup-python-machine-learning-services.md)

+ [Configurar o R nos serviços de aprendizado de máquina do SQL Server](r/set-up-sql-server-r-services-in-database.md)

+ [Exemplos e tutoriais de aprendizado de máquina](tutorials/machine-learning-services-tutorials.md)

