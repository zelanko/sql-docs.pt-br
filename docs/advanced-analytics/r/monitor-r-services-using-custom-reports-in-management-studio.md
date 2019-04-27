---
title: Monitorar o R Services usando relatórios personalizados no Management Studio - serviços do SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 55fcb4e145481f98b0cba065ddab75e7cfa0a538
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641978"
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>Monitorar os Serviços de Machine Learning usando relatórios personalizados no Management Studio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para tornar mais fácil de gerenciar a instância usada para aprendizado de máquina, a equipe de produto forneceu um número de exemplos de relatórios personalizados que você pode adicionar ao SQL Server Management Studio. Esses relatórios, você pode exibir detalhes como:

- Sessões de R ativas ou Python
- Definições de configuração para a instância
- Estatísticas de execução de trabalhos de aprendizado de máquina
- Eventos estendidos para serviços de R
- Pacotes de R ou Python instalados na instância atual

Este artigo explica como instalar e usar os relatórios personalizados fornecidos especificamente para leaerning de máquina. 

Para obter uma introdução geral para relatórios no Management Studio, consulte [relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Como instalar os relatórios

Os relatórios são criados usando o SQL Server Reporting Services, mas podem ser usados diretamente no SQL Server Management Studio, mesmo se o Reporting Services não está instalado em sua instância. 

Para usar esses relatórios:

* Baixe os arquivos RDL do repositório GitHub para exemplos de produto do SQL Server.
* Adicione os arquivos na pasta de relatórios personalizados usada pelo SQL Server Management Studio.
* Abra os relatórios no SQL Server Management Studio.


### <a name="step-1-download-the-reports"></a>Etapa 1. Baixe os relatórios

1. Abra o repositório do GitHub que contém [amostras de produto do SQL Server](https://github.com/Microsoft/sql-server-samples)e baixe os relatórios de exemplo. 

    + [Relatórios personalizados SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > Os relatórios podem ser usados com o SQL Server 2017 Machiine Learning Services ou SQL Server 2016 R Services.

2. Para baixar os exemplos, você também pode fazer logon no GitHub e fazer uma bifurcação local dos exemplos. 

### <a name="step-2-copy-the-reports-to-management-studio"></a>Etapa 2. Copie os relatórios para o Management Studio

3. Localize a pasta de relatórios personalizados usada pelo SQL Server Management Studio. Por padrão, os relatórios personalizados são armazenados nessa pasta:
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   No entanto, você pode especificar uma pasta diferente ou criar subpastas.

4. Copie os arquivos *. RDL para a pasta de relatórios personalizados.


### <a name="step-3-run-the-reports"></a>Etapa 3. Execute os relatórios

5. No Management Studio, clique com botão direito do mouse do nó **Databases** para a instância em que você deseja executar os relatórios.
6. Clique em **relatórios**e, em seguida, clique em **relatórios personalizados**.
7. Na caixa de diálogo **Abrir arquivo** , localize a pasta de relatórios personalizados.
8. Selecione um dos arquivos RDL baixados e, em seguida, clique em **Abrir**.

> [!IMPORTANT]
> Em alguns computadores, como aqueles com dispositivos com alto DPI ou maior que a resolução de 1080p de exibição ou em algumas sessões da área de trabalho remota, esses relatórios não podem ser usados. Há um bug no controle do Visualizador de Relatórios no SSMS que trava o relatório.

## <a name="report-list"></a>Lista de relatórios

O repositório de amostras de produto no GitHub atualmente inclui os seguintes relatórios:

+ **Serviços R – sessões ativas**

  Use esse relatório para exibir os usuários atualmente conectados à instância do SQL Server e trabalhos de aprendizagem de máquina em execução. 
  
+ **Serviços R – configuração**

  Use este relatório para exibir a configuração de tempo de execução do script externo e serviços relacionados. O relatório indica se uma reinicialização é necessária e verificará se há protocolos de rede necessários. 
  
  Autenticação implícita é necessária para tarefas de aprendizado de máquina que são executados no SQL Server como um contexto de computação. Para verificar que a autenticação implícita é configurada, o relatório verifica se existe um logon de banco de dados para o grupo SQLRUserGroup.

 + **Serviços R – configurar instância** 

   Este relatório destina-se a ajudá-lo a configurar o aprendizado de máquina. Você também pode executar esse relatório para corrigir erros de configuração encontrados no relatório anterior.
 
+ **Serviços R – Estatísticas de execução**

  Use esse relatório para exibir estatísticas de execução de trabalhos de aprendizado de máquina. Por exemplo, você pode obter o número total de scripts R que foram executados, o número de execuções paralelas e as funções de RevoScaleR usadas com mais frequência. Clique em **Exibir SQL Script** para obter o código T-SQL completo por trás desse relatório.

  Atualmente o relatório monitora somente as estatísticas para funções do pacote RevoScaleR.

+ **Serviços R – eventos estendidos**

  Use este relatório para exibir uma lista de eventos estendidos que estão disponíveis para monitorar as tarefas relacionadas a tempos de execução do script externo. Clique em **Exibir SQL Script** para obter o código T-SQL completo por trás desse relatório.

+ **Serviços R – pacotes**

  Use esse relatório para exibir uma lista dos pacotes de R ou Python instalado na instância do SQL Server.

+ **Serviços R – utilização de recursos**

  Use esse relatório para exibir o consumo de recursos de CPU, memória e e/s por execução de script externo. Você também pode exibir a configuração de memória de pools de recursos externos.

## <a name="see-also"></a>Confira também

[Serviços de monitoramento](managing-and-monitoring-r-solutions.md)

[Eventos estendidos para serviços R](extended-events-for-sql-server-r-services.md)
