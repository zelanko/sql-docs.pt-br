---
title: Agendar pacotes do SSIS no Linux com cron
description: Este artigo descreve como agendar pacotes SSIS (SQL Server Integration Services) no Linux com o serviço cron.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ac7648287b4e4b609f4dd4f25b1b07a512065364
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68065158"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>Agendar a execução de pacotes do SQL Server Integration Services no Linux com cron

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Ao executar o SSIS (SQL Server Integration Services) e o SQL Server no Windows, você pode automatizar a execução de pacotes do SSIS usando o SQL Server Agent. No entanto, quando você executa o SQL Server e o SSIS no Linux, o utilitário de SQL Server Agent não está disponível para agendar trabalhos no Linux. Em vez disso, você usa o serviço cron, que é amplamente usado em plataformas Linux para automatizar a execução do pacote.

Este artigo apresenta exemplos que mostram como automatizar a execução de pacotes SSIS. Os exemplos são escritos para serem executados no Red Hat Enterprise. O código é semelhante para outras distribuições do Linux, como o Ubuntu.

## <a name="prerequisites"></a>Prerequisites

Antes de usar o serviço cron para executar trabalhos, verifique se ele está em execução no computador.

Para verificar o status do serviço cron, use o seguinte comando: `systemctl status crond.service`.

Se o serviço não estiver ativo (ou seja, não estiver em execução), fale com o administrador para instalar e configurar o serviço cron corretamente.

## <a name="create-jobs"></a>Criar trabalhos

Um trabalho cron é uma tarefa que você pode configurar para ser executada regularmente a um intervalo especificado. O trabalho pode ser tão simples quanto um comando que você normalmente digitaria diretamente no console ou executaria como um script de Shell.

Para facilitar o gerenciamento e a manutenção, recomendamos colocar seus comandos de execução de pacote em um script que contenha um nome descritivo.

Aqui está um exemplo de um script de shell simples para executar um pacote. Ele contém apenas um único comando, mas você pode adicionar mais comandos conforme necessário.

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Agendar trabalhos com o serviço cron

Depois de definir seus trabalhos, você pode agendá-los para execução automática usando o serviço cron.

Para adicionar seu trabalho para cron para ser executado, adicione o trabalho no arquivo crontab. Para abrir o arquivo crontab em um editor em que você pode adicionar ou atualizar o trabalho, use o seguinte comando: `crontab -e`.

Para agendar o trabalho descrito anteriormente para execução diária às 2:10, adicione a seguinte linha ao arquivo crontab:

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

Salve o arquivo crontab e saia do editor.

Para entender o formato do comando de exemplo, examine as informações na seção a seguir.
 
## <a name="format-of-a-crontab-file"></a>Formatos de um arquivo crontab

A imagem a seguir mostra a descrição do formato da linha de trabalho adicionada ao arquivo crontab.

![Descrição do formato para a entrada no arquivo crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

Para obter uma descrição mais detalhada do formato de arquivo crontab, use o seguinte comando: `man 5 crontab`.

Veja um exemplo parcial da saída que ajuda a explicar o exemplo neste artigo:

![Descrição parcial detalhada do formato crontab](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre o SSIS no Linux
-   [Extrair, transformar e carregar dados no Linux com o SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar o SSIS (SQL Server Integration Services) no Linux](sql-server-linux-setup-ssis.md)
-   [Configurar o SQL Server Integration Services no Linux com ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
