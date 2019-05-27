---
title: Agendar pacotes do SSIS no Linux com cron | Microsoft Docs
description: Este artigo descreve como agendar pacotes do SQL Server Integration Services (SSIS) no Linux com o serviço de cron.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 2e3c9f6ee7a02fcdfe1bb2888832b156669cbc11
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014996"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>SQL Server Integration Services de agenda a execução no Linux com cron do pacote

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Quando você executa o SQL Server Integration Services (SSIS) e o SQL Server no Windows, você pode automatizar a execução de pacotes do SSIS usando o SQL Server Agent. Quando você executa o SQL Server e o SSIS no Linux, no entanto, o utilitário do SQL Server Agent não está disponível para agendar trabalhos em Linux. Em vez disso, você pode usar o serviço de cron, que é amplamente usado nas plataformas Linux para automatizar a execução do pacote.

Este artigo fornece exemplos que mostram como automatizar a execução de pacotes do SSIS. Os exemplos são gravados para ser executado no Red Hat Enterprise. O código é semelhante para outras distribuições do Linux, como o Ubuntu.

## <a name="prerequisites"></a>Prerequisites

Antes de usar o serviço de cron para executar trabalhos, verifique se ele está em execução no seu computador.

Para verificar o status do serviço cron, use o seguinte comando: `systemctl status crond.service`.

Se o serviço não está ativo (ou seja, ele não está em execução), consulte o administrador para instalar e configurar o serviço de cron corretamente.

## <a name="create-jobs"></a>Criar trabalhos

Um trabalho cron é uma tarefa que você pode configurar para executar regularmente em um intervalo especificado. O trabalho pode ser tão simple quanto um comando que normalmente seria digitar diretamente no console do ou executado como um script de shell.

Para fins de manutenção e de fácil gerenciamento, é recomendável que você coloque seus comandos de execução do pacote em um script que contém um nome descritivo.

Aqui está um exemplo de um script de shell simples para executar um pacote. Ele contém apenas um único comando, mas você pode adicionar mais comandos conforme necessário.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Agendar trabalhos com o serviço de cron

Depois de definir seus trabalhos, você pode agendá-los para serem executados automaticamente usando o serviço de cron.

Para adicionar seu trabalho de cron executar, adicione o trabalho no arquivo crontab. Para abrir o arquivo crontab em um editor no qual você pode adicionar ou atualizar o trabalho, use o seguinte comando: `crontab -e`.

Para agendar o trabalho descrito anteriormente para executar diariamente às 2H: 10, adicione a seguinte linha ao arquivo crontab:

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Salve o arquivo de crontab e, em seguida, feche o editor.

Para entender o formato do comando de exemplo, examine as informações na seção a seguir.
 
## <a name="format-of-a-crontab-file"></a>Formato de um arquivo crontab

A imagem a seguir mostra a descrição do formato da linha de trabalho que é adicionada ao arquivo crontab.

![Descrição do formato de entrada no arquivo crontab.](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Para obter uma descrição mais detalhada do formato de arquivo crontab, use o seguinte comando: `man 5 crontab`.

Aqui está um exemplo parcial da saída que ajuda a explicar o exemplo neste artigo:

![Descrição detalhada de parcial do formato crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre SSIS no Linux
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)
-   [Configurar o SQL Server Integration Services no Linux com o ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
