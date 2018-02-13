---
title: Agendar pacotes do SSIS no Linux com cron | Microsoft Docs
description: "Este artigo descreve como agendar pacotes do SQL Server Integration Services (SSIS) no Linux com o serviço de cron."
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 005757c0a1b1f4309201fc7b7c63987f4ff3bcb8
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>A execução no Linux com cron do pacote de agendamento SQL Server Integration Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Quando você executa o SQL Server Integration Services (SSIS) e o SQL Server no Windows, você pode automatizar a execução de pacotes SSIS usando o SQL Server Agent. Quando você executa o SQL Server e do SSIS no Linux, no entanto, o utilitário do SQL Server Agent não está disponível para agendar trabalhos no Linux. Em vez disso, você pode usar o serviço de cron, que é amplamente usado em plataformas Linux para automatizar a execução do pacote.

Este artigo fornece exemplos que mostram como automatizar a execução de pacotes do SSIS. Os exemplos são criados para serem executados no Red Hat Enterprise. O código é semelhante para outras distribuições do Linux, como Ubuntu.

## <a name="prerequisites"></a>Prerequisites

Antes de usar o serviço de cron para executar trabalhos, verifique se ele está em execução no seu computador.

Para verificar o status do serviço cron, use o seguinte comando: `systemctl status crond.service`.

Se o serviço não está ativo (ou seja, ele não está funcionando), consulte o administrador para instalar e configurar o serviço de cron corretamente.

## <a name="create-jobs"></a>Criar trabalhos

Um trabalho cron é uma tarefa que você pode configurar para ser executado regularmente em um intervalo especificado. O trabalho pode ser tão simple quanto um comando que normalmente digite diretamente no console ou executado como um script de shell.

Para fins de manutenção e facilidade de gerenciamento, é recomendável que você coloque seus comandos de execução do pacote em um script que contém um nome descritivo.

Aqui está um exemplo de um script de shell simples para executar um pacote. Ele contém apenas um único comando, mas você pode adicionar mais comandos conforme necessário.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Agendar trabalhos com o serviço de cron

Depois que você definiu os trabalhos, você pode agendar sejam executados automaticamente, usando o serviço de cron.

Para adicionar seu trabalho para cron executar, adicione o trabalho no arquivo crontab. Para abrir o arquivo crontab em um editor, onde você pode adicionar ou atualizar o trabalho, use o seguinte comando: `crontab -e`.

Para agendar o trabalho descrito anteriormente para executar diariamente às 2:10, adicione a seguinte linha ao arquivo crontab:

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Salve o arquivo crontab e, em seguida, feche o editor.

Para entender o formato do comando de exemplo, revise as informações na seção a seguir.
 
## <a name="format-of-a-crontab-file"></a>Formato de um arquivo crontab

A imagem a seguir mostra a descrição do formato da linha de trabalho que é adicionada ao arquivo crontab.

![Descrição do formato de entrada no arquivo crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Para obter uma descrição mais detalhada do formato de arquivo crontab, use o seguinte comando: `man 5 crontab`.

Aqui está um exemplo parcial da saída que ajuda a explicar o exemplo neste artigo:

![Descrição detalhada de parcial do formato crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)
