---
title: Downloads do CAB para as atualizações cumulativas do SQL Server | Microsoft Docs
description: Downloads do CAB para serviços de aprendizado de máquina do SQL Server 2017 e o SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e1586f94e21304ce994e5e14bf1b4a57ee796a83
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152527"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>Downloads do CAB para atualizações cumulativas de análise do SQL Server no banco de dados de instâncias

Instâncias do SQL Server configuradas para análise no banco de dados incluem recursos de R e Python que são enviados em arquivos CAB, instalado e atendidos por meio de instalação do SQL Server. 

Em servidores conectados à internet, o CAB atualizações normalmente são aplicadas por meio do Windows Update. Desconectado de servidores devem ser atualizados manualmente. Para obter instruções sobre instalações offline, consulte [componentes sem acesso à internet de aprendizado de máquina de instalar o SQL Server](sql-ml-component-install-without-internet-access.md).

Este artigo fornece links de download para os arquivos CAB para cada atualização cumulativa do SQL Server 2017 serviços Machine Learning (R e Python) - ou SQL Server 2016 R Services - para que você pode atualizar manualmente os servidores desconectados da internet. 

## <a name="prerequisites"></a>Prerequisites

Comece com uma instalação de linha de base.

+ Em serviços do SQL Server 2017 Machine Learning, a versão inicial é a instalação de linha de base. 
+ No SQL Server 2016 R Services, você pode iniciar com a versão inicial, SP1 ou SP2. 

Em seguida, aplique [atualizações cumulativas](https://support.microsoft.com/help/4047329) para instância do mecanismo de banco de dados do SQL Server.

Depois de ter uma instalação de linha de base e tiver aplicado as atualizações cumulativas para o SQL Server, você pode executar uma [a instalação integrada de atualização](sql-ml-component-install-without-internet-access.md#slipstream-upgrades) para instalar os arquivos CAB com atualizada recursos de aprendizado de máquina.

Arquivos CAB são listados em ordem cronológica inversa. Quando você baixar os arquivos CAB e transferi-las para o computador de destino, colocá-los em uma pasta conveniente, como **Downloads** ou pasta do usuário da instalação % temp %.

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 CABs

Versão  |Link de download  | Problemas resolvidos | 
---------|---------------|-------|
**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração. Esta é uma versão anterior. |
R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| Correções secundárias.|
Python de Microsoft Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração. Esta é uma versão anterior. |
Servidor do Python    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| Python rx_data_step perde a ordem de linha quando as duplicatas são removidas. <br/>SPEE Falha na detecção de tipo de dados em um índice columnstore clusterizado. <br/>Retorna uma tabela vazia quando as colunas contêm todos os valores nulos. |
**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração. Esta é uma versão anterior. |
R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
Python de Microsoft Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração. Esta é uma versão anterior. |
Servidor do Python    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração. Esta é uma versão anterior. |
R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
Python de Microsoft Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração. Esta é uma versão anterior. |
Servidor do Python    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| Tipos de dados de data e hora na consulta SPEES.<br/>aprimorada a mensagens de erro em microsoftml quando modelos previamente treinados estão ausentes.<br/> Correções para revoscalepy transformam funções e variáveis.|
**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração. Esta é uma versão anterior. |
R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| Erros de caminho longo relacionados no rxInstallPackages.<br/>Conexões em um loopback para RxExec.
Python de Microsoft Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração. Esta é uma versão anterior. |
Servidor do Python    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Conexões em um loopback para rx_exec.
**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Nenhuma alteração. Esta é uma versão anterior. |
R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Python de Microsoft Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração. Esta é uma versão anterior. |
 Servidor do Python    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Python de Microsoft Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração. Esta é uma versão anterior. |
Servidor do Python    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Revoscalepy, a serialização do modelo de Python usando o [rx_serialize_model função](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/>[Pontuação nativa](../sql-native-scoring.md) suporte, além de aprimoramentos [em tempo real de pontuação](../real-time-scoring.md). 
**SQL Server 2017 [CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |
Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| Nenhuma alteração. Esta é uma versão anterior. |
R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Python de Microsoft Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Nenhuma alteração. Esta é uma versão anterior. 
Servidor do Python    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | Adiciona rx_create_col_info para retornar informações de esquema. <br/>Aprimoramentos [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para dar suporte a cenários paralelos usando o `RxLocalParallel` contexto de computação.|
**Versão inicial** |  |  |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Python de Microsoft Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Servidor do Python    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |


<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 CABs

Para SQL Server 2016 R Services, as versões de linha de base são a versão RTM ou uma versão de service pack.

Versão  |Link de download  |
---------|---------------|
**SQL Server 2016 SP2 CU1-CU2**     |
Microsoft R Open     |[SRO_3.2.2.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039)|
Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
**SQL Server 2016 SP1 CU4-CU10**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP1 CU1-CU3**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 CU4-CU9**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU2-CU3**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**Atualização cumulativa 1 para do SQL Server 2016**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)

> [!NOTE]
> 
> Ao instalar o SQL Server 2016 SP1 CU4 ou SP1 CU5 offline, faça o download SRO_3.2.2.16000_1033.cab. Se você baixou SRO_3.2.2.13000_1033.cab da 831785 FWLINK conforme indicado na caixa de diálogo de instalação, renomeie o arquivo como SRO_3.2.2.16000_1033.cab antes de instalar a atualização cumulativa.

Se você quiser exibir o código-fonte para o Microsoft R, ela está disponível para download como um arquivo no formato. tar: [instaladores de baixar o Microsoft R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

# <a name="see-also"></a>Confira também

[Instalar componentes sem acesso à internet de aprendizado de máquina do SQL Server](sql-ml-component-install-without-internet-access.md)
