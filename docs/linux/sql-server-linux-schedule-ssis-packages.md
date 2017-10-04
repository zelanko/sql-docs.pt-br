---
title: Agendar pacotes do SSIS no Linux com cron | Microsoft Docs
description: "Este artigo mostra como agendar pacotes do SQL Server Integration Services no Linux com o serviço de cron."
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 31d5fb63a9c2a4d8825aa39c6fa7e3377ddc8d91
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>A execução no Linux com cron do pacote de agendamento SQL Server Integration Services

Quando você executa o SQL Server Integration Services (SSIS) e o SQL Server no Windows, você pode automatizar a execução de pacotes SSIS usando o SQL Server Agent. Quando você executa o SQL Server e do SSIS no Linux, no entanto, o utilitário do SQL Server Agent não está disponível para agendar trabalhos no Linux. Em vez disso, você usar **Cron** serviço que é amplamente usado em plataformas Linux para automatizar a execução do pacote.

Este artigo fornece exemplos que mostram como automatizar a execução de pacotes do SSIS. Os exemplos foram criados para serem executados no Red Hat Enterprise. O código é semelhante para outras distribuições do Linux como Ubuntu.

## <a name="prerequisites"></a>Pré-requisitos

Antes de usar o serviço de Cron para executar trabalhos, você precisa verificar se o serviço de Cron está em execução no seu computador.

Use o seguinte comando para verificar o status do serviço Cron.

`systemctl status crond.service`

Se o serviço não está ativo (ou seja, não está em execução), consulte o administrador para instalar e configurar o serviço de Cron corretamente.

## <a name="create-jobs"></a>Criar trabalhos

Um trabalho Cron é uma tarefa que você pode configurar para ser executado regularmente em um intervalo especificado. O trabalho pode ser tão simple quanto um comando que normalmente digite diretamente no console ou executado como um script de shell.

Para fins de manutenção e facilidade de gerenciamento, é recomendável colocar seus comandos de execução do pacote em um script com um nome descritivo.

Aqui está um exemplo simples de um script de shell que contém apenas um único comando para executar um pacote. Você pode adicionar mais comandos conforme necessário.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Agendar trabalhos com o serviço de Cron

Depois que você definiu os trabalhos, você pode agendar sejam executados automaticamente, usando o serviço de Cron.

Para adicionar seu trabalho para Cron executar, você precisa adicionar o trabalho no `crontab` arquivo. Para abrir o `crontab` arquivo em um editor, onde você pode adicionar ou atualizar o trabalho, use o seguinte comando:

`crontab -e`

Para agendar o trabalho descrito anteriormente para executar diariamente às 2:10:00, adicionar os seguintes linha para o `crontab` arquivo:

```
# run SSIS package Name at 2:10AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Salve o `crontab` de arquivo e saia do editor.

Para entender o formato do comando de exemplo, revise as informações na seção a seguir.
 
## <a name="format-of-a-crontab-file"></a>Formato de um arquivo Crontab

A imagem a seguir mostra a descrição do formato da linha do trabalho adicionada para o `crontab` arquivo.

![Descrição do formato de entrada no arquivo crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Para obter uma descrição mais detalhada do `crontab` formato de arquivo, use o seguinte comando:

`man 5 crontab`

Aqui está um exemplo parcial da saída que ajuda a explicar o exemplo neste artigo:

![Descrição detalhada de parcial do formato crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

