---
title: Enviar trabalhos do Spark em clusters de Big Data do SQL Server no Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Enviar trabalhos do Spark em [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Azure Data Studio.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3c7d346148d7967543e334af07d6f06402d72a0d
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844245"
---
# <a name="submit-spark-jobs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-azure-data-studio"></a>Enviar trabalhos do Spark em [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Um dos principais cenários para clusters de Big Data é a capacidade de enviar trabalhos do Spark para o SQL Server. O recurso de envio de trabalhos do Spark permite que você envie arquivos Jar ou Py locais com referências a clusters de Big Data do SQL Server 2019. Ele também permite que você execute arquivos Jar ou Py, que já estão localizados no sistema de arquivos HDFS. 

## <a name="prerequisites"></a>Prerequisites

- [Ferramentas de Big Data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
   - **kubectl**

- [Conectar o Azure Data Studio ao gateway do HDFS/Spark de seu cluster de Big Data](connect-to-big-data-cluster.md).

## <a name="open-spark-job-submission-dialog"></a>Abrir caixa de diálogo de envio de trabalho do Spark

Há várias maneiras de abrir a caixa de diálogo de envio de trabalho do Spark. As maneiras incluem o Painel, o Menu de Contexto no Pesquisador de Objetos e a Paleta de Comandos.

- Para abrir a caixa de diálogo de envio de trabalho do Spark, clique em **Novo Trabalho do Spark** no painel.

    ![Menu de envio clicando no painel](./media/submit-spark-job/new-spark-job.png)

- Ou clique com o botão direito do mouse no cluster no Pesquisador de Objetos e selecione **Enviar Trabalho do Spark** no menu de contexto.

    ![Menu de envio clicando com o botão direito do mouse no arquivo](./media/submit-spark-job/submit-spark-job-1.png)


- Para abrir a caixa de diálogo de envio de trabalho do Spark com os campos Jar/Py preenchidos, clique com o botão direito do mouse em um arquivo Jar/Py no Pesquisador de Objetos e selecione **Enviar Trabalho do Spark** no menu de contexto.  

    ![Menu de envio clicando com o botão direito do mouse no cluster](./media/submit-spark-job/submit-spark-job.png)

- Use **Enviar Trabalho do Spark** na paleta de comandos digitando **Ctrl+Shift+P** (no Windows) e **Cmd+Shift+P** (no Mac).

    ![Envio com paleta de comandos de menu no Windows](./media/submit-spark-job/submit-spark-job-3.png)

    ![Envio com paleta de comandos de menu no Mac](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Enviar trabalho do Spark 

A caixa de diálogo de envio de trabalho do Spark é exibida da seguinte forma. Insira o nome do trabalho, o caminho do arquivo JAR/Py, a classe principal e os dados dos demais campos. A origem do arquivo JAR/Py pode ser local ou o HDFS. Se o trabalho do Spark tiver Jars de referência, arquivos Py ou arquivos adicionais, clique na guia **AVANÇADO** e insira os caminhos dos arquivos correspondentes. Clique em **Enviar** para enviar o trabalho do Spark.

![Caixa de diálogo Novo trabalho do Spark](./media/submit-spark-job/submit-spark-job-section.png)

![Caixa de diálogo Avançado](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Monitorar envio de trabalho do Spark

Após o trabalho do Spark ser enviado, as informações de status do envio e da execução do trabalho do Spark serão exibidas no Histórico de Tarefas à esquerda. Os detalhes sobre o progresso e os logs também são exibidos na janela de **SAÍDA** na parte inferior.

- Quando o trabalho do Spark estiver em andamento, o painel **Histórico de Tarefas** e a janela de **SAÍDA** serão atualizados com o progresso.

    ![Monitorar trabalhos do Spark em andamento](./media/submit-spark-job/monitor-spark-job-submission.png)

- Quando o trabalho do Spark é concluído com êxito, os links das interfaces do usuário do Spark e do YARN aparecem na janela de **SAÍDA**. Clique nos links para obter mais informações.

    ![Link do trabalho do Spark na saída](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os clusters de Big Data do SQL Server e os cenários relacionados, confira [O que são clusters de Big Data do SQL Server?](big-data-cluster-overview.md)