---
title: "Implantar e consumir análises usando mrsdeploy | Microsoft Docs"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2bc4b09d02f5058a466a18823ae8bfb70b3f625b
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="deploy-and-consume-analytics-using-mrsdeploy"></a>Implantar e consumir análises usando mrsdeploy

Microsoft R Server inclui um recurso de operacionalização, **mrsdeploy**, que oferece suporte a essas tarefas:

+ Publicar e gerenciar modelos de R e Python e código na forma de serviços web
+ Consumir esses serviços em aplicativos cliente

Este tópico fornece informações sobre como habilitar e configurar o recurso.

Para obter informações gerais sobre os cenários com suporte pelo **mrsdeploy**, consulte [operacionalização com R Server](https://docs.microsoft.com/r-server/what-is-operationalization).

## <a name="using-mrsdeploy-for-operationalization"></a>Usando mrsdeploy para operacionalização

A palavra *operacionalização* pode significar muitas coisas:

+ A capacidade de publicar modelos em um serviço da web para uso por aplicativos
+ Suporte para a computação distribuída ou escalonável
+ Uma vez de desenvolver, implantar várias vezes
+ Pontuação rápida para ambas as linha única e pontuação de lote

Se você tiver instalado os serviços de aprendizado de máquina com o SQL Server, *operacionalização* é uma questão de encapsular seu código R ou Python em um procedimento armazenado. Qualquer aplicativo, em seguida, pode chamar o procedimento armazenado para treinar novamente um modelo, gerar pontuações ou criar relatórios. Você também pode automatizar trabalhos usando mecanismos de agendamento existentes no SQL Server.

No entanto, o Microsoft R Server fornece um mecanismo diferente para o suporte de implantação, usando os serviços da web que oferecem suporte à publicação de trabalhos em R e um utilitário administrativo para executar trabalhos de R distribuídos. Microsoft R Server usa as funções de **mrsdeploy** pacote para estabelecer uma sessão conosco de computação remoto e execute o código R em um aplicativo de console.

Esse recurso de implantação de R Server oferece estes benefícios:

+ Controle de acesso baseado em função para serviços web analítico

    Determinar quem pode publicar, atualizar e excluir seus próprios serviços web, aqueles que também pode atualizar e excluir os serviços web publicaram por outros usuários e que a lista somente pode e consumirem serviços web.

+ Mais rápido de pontuação
  
  Você pode usar em tempo real com um objeto de modelo de R com suporte de pontuação para melhorar a velocidade de operações de pontuação.

+ Publicar o código Python como um serviço web

  Para obter exemplos, consulte [publicar e consumir o código Python](./python/publish-consume-python-code.md).

+ Consumo assíncrona em lotes

  Serviços Web que chamam para dados de entrada grandes agora podem ser consumidos assíncrona por meio da execução do lote.

+ Dimensionamento automático de uma grade de nós de computação e da web

  Um modelo de script é fornecido para permitir que você facilmente criar um conjunto de VMs de servidor do R no Azure e, em seguida, configurá-los como uma grade para operacionalização de análise e execução remota. Essa grade pode ser expandida ou para baixo com base no uso da CPU.

+ Execução remota assíncrona

    Agora com suporte usando o **mrsdeploy** pacote R. Para continuar trabalhando no seu ambiente de desenvolvimento durante a execução de script remoto, execute o script de R usando de forma assíncrona o `async` parâmetro. Isso é particularmente útil quando você executa scripts que têm tempos de execução.

## <a name="requirements-and-configuration"></a>Requisitos e configuração

SQL Server 2017 CTP 2.0 e posterior inclui esse recurso, que anteriormente estava disponível somente com o servidor de R e não é instalado com o SQL Server R Services. O **mrsdeploy** pacote está instalado no computador do SQL Server, se você selecionar a opção para instalar **Microsoft Server de aprendizado de máquina**, do **recursos compartilhados** seção de instalação do SQL Server.

Normalmente, é recomendável não instalar o servidor de aprendizado de máquina no mesmo computador que está executando serviços de aprendizado de máquina do SQL Server. Recomendamos que você instale **Microsoft Server de aprendizado de máquina** em um computador separado do SQL Server e, em seguida, configure os recursos de operacionalização nesse computador.

No entanto, se você precisa instalá-los juntos, siga estas etapas adicionais para configurar com êxito o serviço.

1. Instalar DotNetCore 1.1

    Se o .NET Core não foi instalado como parte do SQL Server, instale-o antes de iniciar a instalação do R Server.

2. Instale o servidor de aprendizado de máquina da Microsoft.

3. Após concluir a instalação do **Microsoft Server de aprendizado de máquina**, manualmente adicione a seguinte chave do registro para **mrsdeploy**, que especifica a pasta base para os arquivos R_SERVER. 

    + Crie uma nova chave de registro`H_KEY_LOCAL_MACHINE\SOFTWARE\R Server\Path`
    + Defina o valor da chave `"C:\Program Files\Microsoft SQL Server\140\R_SERVER"`.

4. Quando terminar, abra o [utilitário Administrador](https://docs.microsoft.com/r-server/operationalize/configure-use-admin-utility).

5. Continue a configurar o **mrsdeploy** de serviço conforme descrito aqui: [configuração para administradores](https://docs.microsoft.com/r-server/operationalize/configure-start-for-administrators)

6. Para obter mais informações, consulte [mrsdeploy funções](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package).
