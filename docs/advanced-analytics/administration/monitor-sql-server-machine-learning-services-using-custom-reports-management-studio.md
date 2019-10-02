---
title: Monitorar a execução de script do Python e do R usando relatórios personalizados no SSMS
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 549cdcd35b939b2247b14817271e3d1063fab1e0
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714390"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>Monitorar a execução de script do Python e do R usando relatórios personalizados no SQL Server Management Studio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use relatórios personalizados no SQL Server Management Studio (SSMS) para monitorar a execução de scripts externos (Python e R), os recursos usados, diagnosticar problemas e ajustar o desempenho no SQL Server Serviços de Machine Learning.

Nesses relatórios, você pode exibir detalhes como:

- Sessões ativas do Python ou do R
- Definições de configuração para a instância
- Estatísticas de execução para trabalhos do Machine Learning
- Eventos estendidos para o R Services
- Pacotes python ou R instalados na instância atual

Este artigo explica como instalar e usar os relatórios personalizados fornecidos para SQL Server Serviços de Machine Learning.

Para obter mais informações sobre relatórios no SQL Server Management Studio, consulte [relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Como instalar os relatórios

Os relatórios são criados usando SQL Server Reporting Services, mas podem ser usados diretamente do SQL Server Management Studio. O Reporting Services não precisa ser instalado em sua instância do SQL Server.

Para usar esses relatórios, siga estas etapas:

1. Baixe os [relatórios personalizados do SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) para SQL Server serviços de Machine Learning do github.

2. Copie os relatórios para o Management Studio

    1. Localize a pasta de relatórios personalizados usada pelo SQL Server Management Studio. Por padrão, os relatórios personalizados são armazenados nessa pasta (em que **user_name** é o nome de usuário do Windows):

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       Você também pode especificar uma pasta diferente ou criar subpastas.

    2. Copie o *. Arquivos RDL que você baixou para a pasta relatórios personalizados.

3. Executar os relatórios no Management Studio

    1. No Management Studio, clique com botão direito do mouse do nó **Databases** para a instância em que você deseja executar os relatórios.

    2. Clique em **relatórios**e, em seguida, clique em **relatórios personalizados**.

    3. Na caixa de diálogo **Abrir arquivo** , localize a pasta de relatórios personalizados.

    4. Selecione um dos arquivos RDL baixados e, em seguida, clique em **Abrir**.

## <a name="reports"></a>Relatórios

O [repositório de relatórios personalizados do SSMS no GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) inclui os seguintes relatórios:

| Relatório | Descrição |
|-|-|
| Sessões ativas | Os usuários que estão conectados à instância do SQL Server e executando um script Python ou R no momento. |
| Configuração | Configurações de instalação de Serviços de Machine Learning e propriedades do tempo de execução do Python ou do R. |
| Configurar instância | Configurar Serviços de Machine Learning. |
| Estatísticas de execução | Estatísticas de execução dos serviços de Machine Learning. Por exemplo, você pode obter o número total de execuções de scripts externos e o número de execuções paralelas. |
| Eventos estendidos | Eventos estendidos que estão disponíveis para obter mais informações sobre a execução de scripts externos. |
| Packages | Liste os pacotes R ou Python instalados na instância de SQL Server e suas propriedades, como a versão e o nome. |
| Uso de recurso | Exibir a CPU, a memória, o consumo de e/s de SQL Server e a execução de scripts externos. Você também pode exibir a configuração de memória para pools de recursos externos. |

## <a name="next-steps"></a>Próximas etapas

- [Monitorar SQL Server Serviços de Machine Learning usando DMVs (exibições de gerenciamento dinâmico)](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [Eventos estendidos para serviços R](../r/extended-events-for-sql-server-r-services.md)
