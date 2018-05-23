---
title: Agendar pacotes do SSIS no Azure com o SSMS | Microsoft Docs
description: Descreve como agendar pacotes do SSIS implantados no Banco de Dados SQL do Azure usando o comando de agendamento no SSMS (SQL Server Management Studio).
ms.date: 05/09/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 72b20d4d42517555449f639cee398db4363d5735
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2018
---
# <a name="schedule-the-execution-of-an-ssis-package-in-azure-with-sql-server-management-studio-ssms"></a>Agendar a execução de um pacote SSIS no Azure com o SSMS (SQL Server Management Studio)

O SSMS (SQL Server Management Studio) oferece um recurso de agendamento de pacotes SSIS implantado no Banco de Dados SQL do Azure. O SQL Server local e a Instância Gerenciada do Banco de Dados SQL do Azure (versão prévia) têm o SQL Server Agent e o agente de instância gerenciada respectivamente como um agendador de trabalhos do SSIS de primeira classe. Por outro lado, o Banco de Dados SQL não tem um agendador interno de trabalhos do SSIS de primeira classe. O recurso do SSMS descrito neste artigo oferece uma interface do usuário familiar que é semelhante ao SQL Server Agent para agendar pacotes implantados no Banco de Dados SQL.

Se você estiver usando o Banco de Dados SQL para hospedar o banco de dados de catálogo SSIS, o `SSISDB`, poderá usar esse recurso do SSMS para gerar os pipelines de data factory, as atividades e os gatilhos necessários para agendar pacotes do SSIS. Em seguida, você pode editar e estender esses objetos no data factory.

Quando você usa o SSMS para agendar um pacote, o SSIS cria automaticamente três novos objetos data factory, com nomes com base no nome do pacote selecionado e no carimbo de data/hora. Por exemplo, se o nome do pacote SSIS for **MyPackage**, o SSMS criará novos objetos data factory semelhantes ao seguinte:

| Object | Nome |
|---|---|
| Pipeline | **Pipeline_MyPackage_2018-05-08T09_00_00Z** |
| Executar a atividade do pacote SSIS | **Activity_MyPackage_2018-05-08T09_00_00Z** |
| Gatilho | **Trigger_MyPackage_2018-05-08T09_00_00Z** |
|||

## <a name="prerequisites"></a>Prerequisites

O recurso descrito neste artigo exige o SQL Server Management Studio versão 17.7 ou superior. Para obter a versão mais recente do SSMS, confira [Baixar o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md).

## <a name="schedule-a-package-in-ssms"></a>Agendar um pacote no SSMS

1. No SSMS, no Pesquisador de Objetos, selecione o banco de dados do SSISDB, uma pasta, um projeto e, em seguida, selecione um pacote. Clique com o botão direito do mouse no pacote e selecione **Agendar**.

    ![Selecione um pacote a ser agendado.](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image1-schedule.png)

2. A caixa de diálogo **Novo Agendamento** é aberta. Na página **Geral** da caixa de diálogo **Novo Agendamento**, forneça um nome e uma descrição para o novo trabalho agendado.

    ![Página Geral da caixa de diálogo Novo Agendamento](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image2-new-schedule.png)

3. Na página **Pacote** da caixa de diálogo **Novo Agendamento**, selecione configurações de tempo de execução opcionais e um ambiente de tempo de execução.

    ![Página Pacote da caixa de diálogo Novo Agendamento](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image3-new-schedule2.png)

4. Na página **Agendamento** da caixa de diálogo do **Novo Agendamento**, forneça as configurações de agendamento, como a frequência, a hora do dia e a duração.

    ![Página Agendamento da caixa de diálogo Novo Agendamento](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image4-new-schedule3.png)

5. Depois que você criar o trabalho na caixa de diálogo **Novo Agendamento**, uma confirmação será exibida para lembrá-lo dos novos objetos data factory que o SSMS vai criar. Se você selecionar **Sim** na caixa de diálogo de confirmação, o novo pipeline de data factory será aberto no portal do Azure para ser analisado e personalizado.

    ![Confirmação do novo agendamento](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image5-confirmation.png)

6. Para personalizar o gatilho de agendamento, selecione **Novo/Editar** no menu **Gatilho**.

    ![Se preferir, edite o novo pipeline](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image6-edit.png)

    A folha **Editar Gatilho** é aberta para que você personalize as opções de agendamento.

    ![Editar Gatilho](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image7-edit2.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre outros métodos para agendar um pacote SSIS, veja [Agendar a execução de um pacote SSIS no Azure](ssis-azure-schedule-packages.md).

Para saber mais sobre pipelines do Azure Data Factory, atividades e gatilhos, confira os seguintes artigos:
-   [Pipelines e atividades no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities)
-   [Execução de pipelines e gatilhos no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers)
