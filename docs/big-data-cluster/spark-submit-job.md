---
title: Executar trabalhos do Spark no estúdio de dados do Azure
titleSuffix: SQL Server 2019 big data clusters
description: Envie trabalhos do Spark em clusters de grandes dados do SQL Server no estúdio de dados do Azure.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c1d439c13b06b305c814813eeca7cb9bf8aa53c5
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578236"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-azure-data-studio"></a>Enviar trabalhos do Spark em clusters de grandes dados do SQL Server no estúdio de dados do Azure

Um dos principais cenários para clusters de big data é a capacidade de enviar trabalhos do Spark para visualização do SQL Server de 2019. O recurso de envio de trabalho do Spark permite que você envie arquivos Jar ou Py locais com referências a cluster de big data do SQL Server de 2019. Ele também permite que você execute um arquivos Jar ou Py, que já estão localizados no sistema de arquivos HDFS. 

## <a name="prerequisites"></a>Prerequisites

- [Ferramentas de big data do SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensão do SQL Server de 2019**
   - **kubectl**

- [Conectar-se o Studio de dados do Azure para o gateway HDFS/Spark do seu cluster de big data](connect-to-big-data-cluster.md).

## <a name="open-spark-job-submission-dialog"></a>Abrir caixa de diálogo de envio de trabalho Spark
Há várias maneiras para abrir a caixa de diálogo de envio de trabalho Spark. As maneiras de incluem o painel, Menu de contexto no Pesquisador de objetos e paleta de comando.

+ Clique em **novo trabalho de Spark** no painel para abrir a caixa de diálogo de envio de trabalho do Spark.

    ![Enviar menu clicando em Painel](./media/submit-spark-job/new-spark-job.png)
 
+ Clique com botão direito no cluster no Pesquisador de objetos e selecione **enviar trabalho do Spark** no menu de contexto. Caixa de diálogo de envio de trabalho Spark será aberta.  
 
    ![Enviar menu pelo cluster do botão direito do mouse](./media/submit-spark-job/submit-spark-job.png)

+ Clique duas vezes em um arquivo Jar/Py no Pesquisador de objetos e selecione **enviar trabalho do Spark** no menu de contexto. Diálogo de envio de trabalho do Spark com o campo de Jar/Py ser previamente preenchido será aberta. 
 
    ![Enviar menu pelo arquivo de atalho](./media/submit-spark-job/submit-spark-job-2.png)

+ Use o comando **enviar trabalho do Spark** da paleta de comandos, digitando Ctrl + Shift + P (no Windows) e o Cmd + Shift + P (no Mac).

    ![Enviar a paleta de comandos de menu no windows](./media/submit-spark-job/submit-spark-job-3.png)

    ![Enviar a paleta de comandos de menu no mac](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Enviar trabalho do Spark 
A caixa de diálogo de envio de trabalho do Spark é exibida como a seguir. Insira o nome do trabalho, caminho do arquivo JAR/Py, classe principal e outros campos. O arquivo Jar / Py fonte de arquivo pode ser do Local ou do HDFS. Se o trabalho tem do Spark fazem referência Jars, Py arquivos ou arquivos adicionais, clique em **avançado** guia e insira os caminhos de arquivo correspondente. Clique em **enviar** ao enviar o trabalho do Spark.
 
![Nova caixa de diálogo de trabalho do spark](./media/submit-spark-job/submit-spark-job-section.png)

![Caixa de diálogo avançada](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Monitorar o envio de trabalho do Spark
Depois que o trabalho do Spark é enviado, as Spark trabalho execução e envio de informações de status são exibidos no histórico de tarefas à esquerda. E detalhes sobre o progresso e os logs também são exibidas na **saída** inferior da janela.
+ Quando o trabalho do Spark está em andamento, o **histórico de tarefa** painel e **saída** janela são atualizados com o andamento.

![Trabalho de monitor de spark em andamento](./media/submit-spark-job/monitor-spark-job-submission.png)

+ Quando o trabalho do Spark está em concluída com êxito, você pode ver links da interface do usuário do Spark e Yarn da interface do usuário na **saída** janela. Você pode clicar nos links para obter mais informações.

![Link de trabalho do Spark na saída](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o cluster de big data do SQL Server e cenários relacionados, consulte [o que é o cluster de big data do SQL Server](big-data-cluster-overview.md)?

