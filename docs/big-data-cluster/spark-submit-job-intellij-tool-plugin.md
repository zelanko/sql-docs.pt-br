---
title: 'Executar trabalhos do Spark: Kit de Ferramentas do Azure para IntelliJ'
titleSuffix: SQL Server Big Data Clusters
description: Enviar trabalhos do Spark em clusters de Big Data do SQL Server no Azure Toolkit for IntelliJ.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.topic: conceptual
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 70cdc7e9738abdde2dfaf479320b11a94469f661
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244079"
---
# <a name="submit-spark-jobs-on-big-data-clusters-2019-in-intellij"></a>Enviar trabalhos do Spark em [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no IntelliJ

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Um dos principais cenários para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] é a capacidade de enviar trabalhos do Spark. O recurso de envio de trabalhos do Spark permite que você envie arquivos Jar ou Py locais com referências a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]. Ele também permite que você execute arquivos Jar ou Py, que já estão localizados no sistema de arquivos HDFS. 

## <a name="prerequisites"></a>Prerequisites

- Cluster de Big Data do SQL Server.
- Kit de Desenvolvimento Java para Oracle. É possível instalá-lo do [site da Oracle](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. É possível instalá-lo do [site da JetBrains](https://www.jetbrains.com/idea/download/).
- Extensão do Azure Toolkit for IntelliJ. Para obter instruções de instalação, confira [Instalar o Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation).

## <a name="link-sql-server-big-data-cluster"></a>Link para o cluster de Big Data do SQL Server
1. Abra a ferramenta IntelliJ IDEA.

2. Se estiver usando um certificado autoassinado, desabilite a validação do certificado SSL no menu **Ferramentas**, selecione **Azure**, **Validar Certificado SSL do Cluster Spark** e, em seguida, **Desabilitar**.

    ![link para o cluster de Big Data do SQL Server – desabilitar SSL](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. Abra o Azure Explorer no menu **Exibir**, selecione **Janelas de Ferramentas** e, em seguida, selecione **Azure Explorer**.
4. Clique com o botão direito do mouse em **Cluster de Big Data do SQL Server**, selecione **Vincular Cluster de Big Data do SQL Server**. Insira o **Servidor**, o **Nome de Usuário** e a **Senha** e, então, clique em **OK**.

    ![vincular cluster de Big Data – caixa de diálogo](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. Quando a caixa de diálogo de certificado do servidor não confiável for exibida, clique em **Aceitar**. Você pode gerenciar o certificado mais tarde, confira [Certificados do Servidor](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html).

6. O cluster vinculado é listado em **Cluster de Big Data do SQL Server**. Você pode monitorar o trabalho do Spark abrindo a interface do usuário de histórico do Spark e a interface do usuário do YARN. Também pode desvincular o cluster clicando com o botão direito do mouse nele.

    ![vincular cluster de Big Data – menu de contexto](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-spark-template"></a>Criar um aplicativo Scala Spark usando um modelo do Spark

1. Inicie o IntelliJ IDEA e, em seguida, crie um projeto. Na caixa de diálogo **Novo Projeto**, siga estas etapas: 

   a. Selecione **Azure Spark/HDInsight** > **Projeto do Spark com Amostras (Scala)** .

   b. Na lista **Ferramenta de build**, selecione uma das opções a seguir de acordo com sua necessidade:

      * **Maven**, para suporte do assistente de criação de projeto do Scala
      * **SBT**, para gerenciar as dependências e compilações para o projeto do Scala

    ![A caixa de diálogo Novo Projeto](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. Selecione **Avançar**.

3. O assistente de criação de projeto do Scala detecta automaticamente se você instalou o plug-in do Scala. Selecione **Instalar**.

   ![Verificação de plug-do Scala](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Para baixar o plug-in do Scala, selecione **OK**. Siga as instruções para reiniciar o IntelliJ. 

   ![A caixa de diálogo de instalação do plug-in do Scala](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. Na janela **Novo Projeto**, execute as seguintes etapas:  

    ![Selecionando o SDK do Spark](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   a. Insira um nome e uma localização para o projeto.

   b. Na lista suspensa **SDK do Projeto**, selecione **Java 1.8** para o cluster do Spark 2.x ou selecione **Java 1.7** para o cluster do Spark 1.x.

   c. Na lista suspensa **Versão do Spark**, o assistente de criação de projeto do Scala integra a versão correta do SDK do Spark e do SDK do Scala. Se a versão do cluster do Spark for anterior à 2.0, selecione **Spark 1.x**. Caso contrário, selecione **Spark2.x**. Este exemplo usa o **Spark 2.0.2 (Scala 2.11.8)** .

6. Selecione **Concluir**.

7. O projeto do Spark cria automaticamente um artefato para você. Para exibir o artefato, execute as seguintes etapas:

   a. No menu **Arquivo**, selecione **Estrutura do Projeto**.

   b. Na caixa de diálogo **Estrutura do Projeto**, selecione **Artefatos** para exibir o artefato padrão que é criado. Você também pode criar seu próprio artefato selecionando o sinal de adição ( **+** ).

      ![Informações do artefato na caixa de diálogo](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>Enviar aplicativo ao cluster de Big Data do SQL Server
Após vincular um cluster de Big Data do SQL Server, você pode enviar o aplicativo para ele.

1. Defina a configuração na janela **Configurações de execução/depuração**, clique em +->**Apache Spark no SQL Server**, selecione a guia **Executar Remotamente no Cluster**, defina os parâmetros da seguinte forma e clique em OK.

    ![Adicionar entrada de configuração do console interativo](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![vincular cluster de Big Data – configuração](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * Para **Clusters do Spark (somente Linux**), selecione o cluster no qual deseja executar o aplicativo.

    * Selecione um artefato do projeto do IntelliJ ou selecione um no disco rígido.

    * Campo **Nome da classe principal**: O valor padrão é a classe principal do arquivo selecionado. Você pode alterar a classe selecionando as reticência ( **...** ) e escolhendo outra classe.   

    * Campo **Configurações do Trabalho**:  os valores padrão são definidos como na imagem mostrada acima. Você pode alterar o valor ou adicionar uma nova chave/valor para o envio do trabalho. Para mais informações: [API REST do Apache Livy](http://livy.incubator.apache.org./docs/latest/rest-api.html)

      ![O significado da configuração do trabalho da caixa de diálogo de Envio do Spark](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * Campo **Argumentos de linha de comando**: você pode inserir os valores dos argumentos divididos por espaço para a classe principal, se necessário.

    * Campos **Jars Referenciados** e **Arquivos Referenciados**: você pode inserir os caminhos para os Jars e os arquivos referenciados, se houver. Para mais informações: [Configuração do Apache Spark](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) 

      ![O significado dos arquivos Jar da caixa de diálogo de Envio do Spark](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > Para carregar os JARs referenciados e os Arquivos Referenciados, confira: [Como carregar recursos no cluster](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **Caminho de Upload**: você pode indicar a localização de armazenamento para envio de recursos de projeto do Jar ou Scala. Há vários tipos de armazenamento com suporte: **Usar a sessão interativa do Spark para carregar** e **Usar o WebHDFS para carregar**
    
2. Clique em **SparkJobRun** para enviar seu projeto para o cluster selecionado. A guia **Trabalho do Spark Remoto no Cluster** exibe o andamento da execução do trabalho na parte inferior. Você pode parar o aplicativo clicando no botão vermelho.  

    ![vincular cluster de Big Data – execução](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="spark-console"></a>Console do Spark
Você pode executar o Console Local do Spark (Scala) ou o Console de Sessão Interativa do Spark Livy (Scala).

### <a name="spark-local-consolescala"></a>Console Local do Spark (Scala)
Certifique-se de que você satisfez o pré-requisito do WINUTILS.EXE.

1. Na barra de menus, navegue até **Executar** > **Editar Configurações...** .

2. Na janela **Configurações de Execução/Depuração**, no painel esquerdo, navegue até **Cluster de Big Data do Apache Spark no SQL Server** >  **[Spark no SQL] myApp**.

3. Na janela principal, selecione a guia **Executar Localmente**.

4. Forneça os seguintes valores e, em seguida, selecione **OK**:

    |Propriedade |Valor |
    |----|----|
    |Classe principal do trabalho|O valor padrão é a classe principal do arquivo selecionado. Você pode alterar a classe selecionando as reticência ( **...** ) e escolhendo outra classe.|
    |Variáveis de ambiente|Verifique se o valor de HADOOP_HOME está correto.|
    |Localização de WINUTILS.exe|Verifique se o caminho está correto.|

    ![Configuração do conjunto de console local](./media/spark-submit-job-intellij-tool-plugin/console-set-configuration.png)

5. De Projeto, navegue até **myApp** > **src** > **main** > **scala** > **myApp**.  

6. Na barra de menus, navegue até **Ferramentas** > **Console do Spark** > **Executar Console Local do Spark (Scala)** .

7. Em seguida, duas caixas de diálogo poderão ser exibidas para perguntar se você deseja corrigir automaticamente as dependências. Em caso afirmativo, selecione **Autocorreção**.

    ![Autocorreção do Spark 1](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix1.png)

    ![Autocorreção do Spark 2](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix2.png)

8. O console deve ser semelhante à imagem abaixo. Na janela do console, digite `sc.appName` e pressione ENTER.  O resultado será exibido. Você pode encerrar o console local clicando no botão vermelho.

    ![Resultado do console local](./media/spark-submit-job-intellij-tool-plugin/local-console-result.png)


### <a name="spark-livy-interactive-session-consolescala"></a>Console de Sessão Interativa do Spark Livy (Scala)
O Console de Sessão Interativa do Spark Livy (Scala) tem suporte apenas no IntelliJ 2018.2 e 2018.3.

1. Na barra de menus, navegue até **Executar** > **Editar Configurações...** .

2. Na janela **Configurações de Execução/Depuração**, no painel esquerdo, navegue até **Cluster de Big Data do Apache Spark no SQL Server** >  **[Spark no SQL] myApp**.

3. Na janela principal, selecione a guia **Executar Remotamente no Cluster**.

4. Forneça os seguintes valores e, em seguida, selecione **OK**:

    |Propriedade |Valor |
    |----|----|
    |Clusters do Spark (somente Linux)|Selecione o cluster de Big Data do SQL Server no qual deseja executar o aplicativo.|
    |Nome da classe principal|O valor padrão é a classe principal do arquivo selecionado. Você pode alterar a classe selecionando as reticência ( **...** ) e escolhendo outra classe.|

    ![Configuração do conjunto de console interativo](./media/spark-submit-job-intellij-tool-plugin/interactive-console-configuration.png)

5. De Projeto, navegue até **myApp** > **src** > **main** > **scala** > **myApp**.  

6. Na barra de menus, navegue até **Ferramentas** > **Console do Spark** > **Executar Console de Sessão Interativa do Spark Livy (Scala)** .

7. O console deve ser semelhante à imagem abaixo. Na janela do console, digite `sc.appName` e pressione ENTER.  O resultado será exibido. Você pode encerrar o console local clicando no botão vermelho.

    ![Resultado do console interativo](./media/spark-submit-job-intellij-tool-plugin/interactive-console-result.png)

### <a name="send-selection-to-spark-console"></a>Enviar seleção ao console do Spark

Para sua conveniência, você pode ver o resultado do script enviando código ao Console Local ou ao Console de Sessão Interativa do Livy (Scala). Você pode realçar código no arquivo do Scala e, em seguida, clicar com o botão direito do mouse em **Enviar Seleção ao Console do Spark**. O código selecionado será enviado para o console e será executado. O resultado será exibido após o código no console. O console verificará erros, se houver.  

   ![Enviar seleção ao console do Spark](./media/spark-submit-job-intellij-tool-plugin/send-selection-to-console.png)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre os clusters de Big Data do SQL Server e os cenários relacionados, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)?
