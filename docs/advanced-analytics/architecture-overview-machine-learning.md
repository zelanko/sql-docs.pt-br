---
title: "Visão geral da arquitetura de serviços de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: c81f114f97dee97a37832201637ac5e17fe08794
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="architecture-overview-for-sql-server-machine-learning-services"></a>Visão geral da arquitetura de serviços de aprendizado de máquina do SQL Server 

Este tópico descreve as metas da estrutura de extensibilidade que dá suporte à execução de script de Python e R no SQL Server.

Ele também fornece uma visão geral de como a arquitetura é projetada para atender a essas metas, como R Python com suporte e é executado pelo SQL Server e os benefícios da integração.

Em geral, a estrutura de extensibilidade é quase idêntica para R e Python, com algumas pequenas diferenças na detalhes dos iniciadores que são chamados, opções de configuração e assim por diante. Para obter mais informações sobre a implementação para um idioma específico, consulte estes tópicos:

- [Visão geral da arquitetura do SQL Server R Services](r/architecture-overview-sql-server-r.md)
- [Visão geral da arquitetura de Python no SQL Server](python/architecture-overview-sql-server-python.md)


## <a name="background"></a>Plano de fundo

No SQL Server 2016, várias alterações foram introduzidas para o mecanismo de banco de dados para permitir a execução de scripts R usando o SQL Server. No SQL Server de 2017, essa infraestrutura subjacente foi aprimorada para adicionar suporte para a linguagem Python.

O objetivo da estrutura de extensibilidade era criar uma interface melhor entre o SQL Server e linguagens de ciência de dados, como R e Python, para reduzir a fricção que ocorre quando as soluções de ciência de dados são movidas para produção e para proteger os dados que podem ser exposto durante o processo de desenvolvimento de ciência de dados.

Executando uma linguagem de script confiável em uma estrutura segura gerenciada pelo SQL Server, o desenvolvedor de banco de dados pode manter a segurança ao mesmo tempo, permitindo que os cientistas de dados usar dados corporativos.

  ![Metas da integração com o SQL Server](media/ml-service-value-add.png "Machine Learning serviços de valor agregado")

- Os usuários atuais de R ou Python devem ser capazes de porta de seu código e executá-lo no SQL Server com relativamente pequenas modificações.
- O modelo de segurança de dados no SQL Server é estendido para os dados usados por linguagens de script externo. Em outras palavras, uma pessoa executar script R ou Python não poderá usar nenhum dado não pôde ser acessado pelo usuário em uma consulta SQL.
- O administrador de banco de dados deve ser capaz de gerenciar recursos usados por scripts externos, gerenciar usuários, gerenciar e monitorar as bibliotecas de código externo.
- O sistema deve dar suporte a soluções inteiramente com base nos distribuições de código aberto do R e Python, mas use proprietárias componentes desenvolvidos pela Microsoft para fornecer maior segurança e desempenho.

## <a name="architecture-core-concepts"></a>Conceitos básicos de arquitetura

Para atender a essas metas, a arquitetura do SQL Server 2016 R Services e serviços de aprendizado de máquina do SQL Server 2017 para R e Python é baseada nesses conceitos básicos:

+ **Arquitetura de vários processo**

  R e Python é linguagens de código-fonte aberto com suporte da comunidade entusiastas e Avançado. Portanto, é importante manter total interoperabilidade com R de software livre e Python.

  Distribuições de código aberto do R e Python são instaladas com o SQL Server sob licença e podem funcionar independentemente do SQL Server, se necessário.

   Além disso, a Microsoft fornece um conjunto de bibliotecas proprietárias que fornecem integração com o SQL Server, incluindo a conversão de dados, a compactação e a otimização voltada para cada idioma com suporte.

+ **Segurança**

   Melhor segurança significa suporte para autenticação integrada do Windows e logons do SQL com base em senha, como também como proteger manipulação de credenciais, depende do SQL Server para proteção de dados e o uso do SQL Server confiável barra para gerenciar o script externo a execução e proteger os dados usados em scripts.

+ **Escalabilidade e desempenho**

  Integração com o SQL Server é importante para aumentar a utilidade de R e Python na empresa. Qualquer script R ou Python pode ser executado chamando um procedimento armazenado, e os resultados são retornados como resultados tabulares diretamente para o SQL Server, tornando mais fácil gerar ou consumir o aprendizado de máquina de qualquer aplicativo que possa enviar uma consulta SQL e lidar com os resultados.

  Otimização de desempenho se baseia em dois aspectos igualmente avançados da plataforma: controle de recursos e paralelo processamento usando o SQL Server e distributed computing fornecidos por algoritmos de **RevoScaleR** e **revoscalepy**.

## <a name="solution-development-and-deployment"></a>Implantação e desenvolvimento de soluções

Além dessas metas principais para a plataforma de extensibilidade, os serviços de aprendizado de máquina no SQL Server são projetados para fornecer forte integração com o mecanismo de banco de dados e a pilha de BI, com estes benefícios:

+ Desempenho e gerenciamento de recursos por meio de ferramentas de monitoramento tradicionais
+ Fácil utilização de dados Python e R por conjuntos de BI ou qualquer aplicativo que pode consumir os resultados da consulta SQL
+ Muito inferior barreira para desenvolvimento empresarial de soluções de aprendizado de máquina

Vamos ver como isso funciona na prática.

  ![Processo de desenvolvimento da solução ML](media/ml-solution-development-process.png "desenvolver e implantar usando serviços de aprendizado de máquina")

1. Os dados são mantidos dentro do limite de conformidade e uso de dados pode ser gerenciado e monitorado pelo SQL Server. Enquanto isso, o DBA tem total controle sobre quem pode instalar pacotes ou executar scripts no servidor. Se desejado, o DBA também pode delegar permissões em um nível de banco de dados para cientistas de dados ou os gerentes.
2. Os cientistas de dados podem compilar e testar soluções em seus ambientes R ou Python preferenciais, desconectados do servidor.
3. O desenvolvedor do SQL pode usar ferramentas familiares, como o Management Studio ou o Visual Studio para integrar o código de R ou Python com o SQL Server. A integração significa que o desenvolvedor experiente pode escolher a melhor ferramenta para otimizar a cada tarefa. Por exemplo, você pode usar o SQL para algumas tarefas de engenharia de recurso e R para outras pessoas. Você pode inserir o script Python em uma tarefa do Integration Services para executar uma análise sofisticada de texto.
4. Testado e pronto para implantar soluções podem ser otimizadas usando tecnologias do SQL Server, como índices columnstore, para melhorar o desempenho. Novos recursos permitem muitos modelos pequenos em paralelo no conjunto de dados particionado de trem de lote ou pontuação milhões de linhas usando código nativo do SQL otimizado para tarefas de aprendizado de máquina.
5. Pronto para projetará? Você pode expor facilmente suas soluções de previsão para a pilha de BI ou aplicativos externos usando procedimentos armazenados.

## <a name="related-products"></a>Produtos relacionados

Não tem certeza qual solução de aprendizado de máquina atende às suas necessidades? Além de análise incorporada no SQL Server 2016 e 2017 do SQL Server, a Microsoft fornece a seguinte serviços e plataformas de aprendizado de máquina:

+ [Microsoft R Server e o servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)

  Um ambiente de várias plataformas de desenvolvimento, distribuir e gerenciar trabalhos de aprendizado de máquina
+ [Máquinas virtuais de ciência de dados](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview)

  Todas as ferramentas que você precisa para aprendizado de máquina, pré-instalado. Use blocos de anotações do Jupyter, Python ou R.
  
  Experimente o novo [edição Windows 2016](http://aka.ms/dsvm/win2016), que inclui versões GPU de estruturas de aprendizado populares, como CNTK e mxNet, bem como suporte para contêineres do Windows!

+ [Serviços Cognitivos do Azure](https://azure.microsoft.com/services/cognitive-services/)

  Uma variedade de serviços de nuvem para adicionar AI e ML em seus aplicativos, incluindo a indexação de idioma natural de reconhecimento facial, vídeo, detecção de emoção, análises de texto, do computador tradução e muito mais
+ [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)

  Uma interface de arrastar e soltar baseado em nuvem para a criação de fluxos de trabalho aprendizado de máquina, juntamente com a capacidade de automatizar e integrar aplicativos por meio de serviços web e PowerShell

## <a name="see-also"></a>Consulte também

[Comparar os produtos de servidor de aprendizado de máquina e Microsoft R](https://docs.microsoft.com/machine-learning-server/what-is-r-server-interoperability)
