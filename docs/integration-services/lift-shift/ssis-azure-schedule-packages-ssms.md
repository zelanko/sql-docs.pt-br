---
title: Agendar pacotes do SSIS no Azure com o SSMS | Microsoft Docs
description: Descreve como agendar pacotes do SSIS implantados no Banco de Dados SQL do Azure usando o comando de agendamento no SSMS (SQL Server Management Studio).
ms.date: 09/23/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 2276b2d769128be1d8ce5cbd44c992f08ddf625b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786234"
---
# <a name="schedule-the-execution-of-ssis-packages-deployed-in-azure-with-sql-server-management-studio-ssms"></a>Agendar a execução de pacotes SSIS implantados no Azure com o SSMS (SQL Server Management Studio)

Você pode usar o SSMS (SQL Server Management Studio) para agendar pacotes SSIS implantados no Banco de Dados SQL do Azure. O SQL Server local e a Instância Gerenciada do Banco de Dados SQL do Azure têm o SQL Server Agent e o Agente de Instância Gerenciada, respectivamente, como um agendador de trabalhos do SSIS de primeira classe. Por outro lado, o Banco de Dados SQL não tem um agendador interno de trabalhos do SSIS de primeira classe. O recurso do SSMS descrito neste artigo oferece uma interface do usuário familiar que é semelhante ao SQL Server Agent para agendar pacotes implantados no Banco de Dados SQL.

Se estiver usando o Banco de Dados SQL para hospedar o Catálogo do SSIS, o `SSISDB`, você poderá usar esse recurso do SSMS para gerar os pipelines de Data Factory, as atividades e os gatilhos necessários para agendar pacotes SSIS. Posteriormente, você poderá opcionalmente editar e estender esses objetos no Data Factory.

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
