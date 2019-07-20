---
title: Monitorar o R Services usando relatórios personalizados no Management Studio
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: d8768532e3891183d82cbb2273ded8dcc378b1fc
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345301"
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>Monitorar os Serviços de Machine Learning usando relatórios personalizados no Management Studio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para facilitar o gerenciamento da instância usada para o aprendizado de máquina, a equipe de produto forneceu vários exemplos de relatórios personalizados que você pode adicionar ao SQL Server Management Studio. Nesses relatórios, você pode exibir detalhes como:

- Sessões ativas do R ou do Python
- Definições de configuração para a instância
- Estatísticas de execução para trabalhos do Machine Learning
- Eventos estendidos para o R Services
- Pacotes R ou Python instalados na instância atual

Este artigo explica como instalar e usar os relatórios personalizados fornecidos especificamente para o Machine leaerning. 

Para obter uma introdução geral aos relatórios no Management Studio, consulte [relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Como instalar os relatórios

Os relatórios são criados usando o SQL Server Reporting Services, mas podem ser usados diretamente no SQL Server Management Studio, mesmo se o Reporting Services não está instalado em sua instância. 

Para usar esses relatórios:

* Baixe os arquivos RDL do repositório GitHub para exemplos de produto do SQL Server.
* Adicione os arquivos na pasta de relatórios personalizados usada pelo SQL Server Management Studio.
* Abra os relatórios no SQL Server Management Studio.


### <a name="step-1-download-the-reports"></a>Etapa 1. Baixe os relatórios

1. Abra o repositório GitHub que contém [SQL Server exemplos de produtos](https://github.com/Microsoft/sql-server-samples)e baixe os relatórios de exemplo. 

    + [Relatórios personalizados do SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

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

O repositório de exemplos de produtos no GitHub atualmente inclui os seguintes relatórios:

+ **Serviços R – sessões ativas**

  Use este relatório para exibir os usuários que estão conectados à instância do SQL Server e executando trabalhos do Machine Learning no momento. 
  
+ **Serviços R – configuração**

  Use esse relatório para exibir a configuração do tempo de execução de script externo e os serviços relacionados. O relatório indica se uma reinicialização é necessária e verificará se há protocolos de rede necessários. 
  
  A autenticação implícita é necessária para tarefas de aprendizado de máquina que são executadas no SQL Server como um contexto de computação. Para verificar se a autenticação implícita está configurada, o relatório verifica se existe um logon de banco de dados para o grupo SQLRUserGroup.

 + **Serviços R – configurar instância** 

   Este relatório destina-se a ajudá-lo a configurar o aprendizado de máquina. Você também pode executar esse relatório para corrigir erros de configuração encontrados no relatório anterior.
 
+ **Serviços R – Estatísticas de execução**

  Use este relatório para exibir estatísticas de execução para trabalhos do Machine Learning. Por exemplo, você pode obter o número total de scripts R que foram executados, o número de execuções paralelas e as funções de RevoScaleR usadas com mais frequência. Clique em **Exibir script SQL** para obter o código T-SQL completo por trás deste relatório.

  Atualmente o relatório monitora somente as estatísticas para funções do pacote RevoScaleR.

+ **Serviços R – eventos estendidos**

  Use este relatório para exibir uma lista dos eventos estendidos que estão disponíveis para monitorar tarefas relacionadas a tempos de execução de script externo. Clique em **Exibir script SQL** para obter o código T-SQL completo por trás deste relatório.

+ **Serviços R – pacotes**

  Use este relatório para exibir uma lista dos pacotes R ou Python instalados na instância do SQL Server.

+ **Serviços R – utilização de recursos**

  Use este relatório para exibir o consumo de CPU, memória e recursos de e/s por execução de script externo. Você também pode exibir a configuração de memória de pools de recursos externos.

## <a name="see-also"></a>Confira também

[Serviços de monitoramento](managing-and-monitoring-r-solutions.md)

[Eventos estendidos para serviços R](extended-events-for-sql-server-r-services.md)
