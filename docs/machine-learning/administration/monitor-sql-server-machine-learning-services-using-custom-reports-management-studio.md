---
title: Monitorar scripts com relatórios personalizados
description: Use relatórios personalizados no SSMS (SQL Server Management Studio) para monitorar a execução de scripts externos (do Python e do R), os recursos usados, diagnosticar problemas e ajustar o desempenho nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/17/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 878c83f76a0235a43bcc22bb65e10dfa9eceb1b1
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179648"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>Monitorar a execução de script do Python e do R usando relatórios personalizados no SQL Server Management Studio
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Use relatórios personalizados no SSMS (SQL Server Management Studio) para monitorar a execução de scripts externos (do Python e do R), os recursos usados, diagnosticar problemas e ajustar o desempenho nos Serviços de Machine Learning do SQL Server.

Nesses relatórios, você pode exibir detalhes como:

- Sessões ativas do Python ou do R
- Definições de configuração para a instância
- Estatísticas de execução para trabalhos de aprendizado de máquina
- Eventos estendidos para serviços de R
- Pacotes de Python ou R instalados na instância atual

Este artigo explica como instalar e usar os relatórios personalizados fornecidos para os Serviços de Machine Learning do SQL Server.

Para obter mais informações sobre relatórios no SQL Server Management Studio, confira [Relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Como instalar os relatórios

Os relatórios são criados usando o SQL Server Reporting Services, mas podem ser usados diretamente no SQL Server Management Studio. O Reporting Services não precisa ser instalado em sua instância do SQL Server.

Para usar esses relatórios, siga estas etapas:

1. Baixe os [Relatórios personalizados do SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) para Serviços de Machine Learning do SQL Server no GitHub.

2. Copie os relatórios para o Management Studio

    1. Localize a pasta de relatórios personalizados usada pelo SQL Server Management Studio. Por padrão, os relatórios personalizados são armazenados nessa pasta (em que **user_name** é o seu nome de usuário do Windows):

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       Você também pode especificar uma pasta diferente ou criar subpastas.

    2. Copie os arquivos *.RDL que você baixou para a pasta de relatórios personalizados.

3. Executar os relatórios no Management Studio

    1. No Management Studio, clique com botão direito do mouse do nó **Databases** para a instância em que você deseja executar os relatórios.

    2. Clique em **relatórios**e, em seguida, clique em **relatórios personalizados**.

    3. Na caixa de diálogo **Abrir arquivo** , localize a pasta de relatórios personalizados.

    4. Selecione um dos arquivos RDL baixados e, em seguida, clique em **Abrir**.

## <a name="reports"></a>Relatórios

O [Repositório de relatórios personalizados do SSMS no GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) inclui os seguintes relatórios:

| Relatório | Descrição |
|-|-|
| Sessões ativas | Os usuários que estão conectados à instância do SQL Server e executando um script de Python ou R no momento. |
| Configuração | Configurações de instalação de Serviços de Machine Learning e propriedades do runtime do Python ou do R. |
| Configurar instância | Configurar Serviços de Machine Learning. |
| Estatísticas de execução | Estatísticas de execução dos Serviços de Machine Learning. Por exemplo, você pode obter o número total de execuções de scripts externos e o número de execuções paralelas. |
| Eventos estendidos | Eventos estendidos que estão disponíveis para obter mais insights sobre a execução de scripts externos. |
| Pacotes | Liste os pacotes R ou Python instalados na instância do SQL Server e suas propriedades, como a versão e o nome. |
| Uso de recurso | Exiba a CPU, a memória, o consumo de E/S do SQL Server e a execução de scripts externos. Você também pode exibir a configuração de memória para pools de recursos externos. |

## <a name="next-steps"></a>Próximas etapas

- [Monitorar os Serviços de Machine Learning do SQL Server usando DMVs (exibições de gerenciamento dinâmico)](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [Monitorar scripts do Python e do R com eventos estendidos nos Serviços de Machine Learning do SQL Server](extended-events.md)
