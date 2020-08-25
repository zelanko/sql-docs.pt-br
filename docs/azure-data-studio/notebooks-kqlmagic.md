---
title: Notebooks com Kqlmagic (Linguagem de Consulta Kusto) no Azure Data Studio
description: Este tutorial mostra como criar e executar Kqlmagic no Azure Data Studio.
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: 0f05030869b66ca0d2f57000aa85f02c93079f08
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766825"
---
# <a name="kqlmagic-extension-in-azure-data-studio"></a>Extensão Kqlmagic no Azure Data Studio

**Kqlmagic** é um comando que estende os recursos do kernel de Python nos **[Notebooks do Azure Data Studio](notebooks-guidance.md)** . Você pode combinar o Python e o **[KQL (linguagem de consulta Kusto)](/azure/data-explorer/kusto/query)** para consultar e visualizar dados usando a avançada biblioteca Plot.ly integrada com comandos `render`. O Kqlmagic traz o benefício dos notebooks, da análise de dados e dos recursos avançados de Python, tudo isso no mesmo lugar. As fontes de dados com suporte para Kqlmagic incluem o **[Azure Data Explorer](/azure/data-explorer/data-explorer-overview)** , o **[Application Insights](/azure/azure-monitor/app/app-insights-overview)** e os **[Logs do Azure Monitor](/azure/azure-monitor/platform/data-platform-logs)** .

Este artigo mostra como criar e executar um notebook no Azure Data Studio usando a extensão Kqlmagic para um cluster do Azure Data Explorer, um log do Application Insights e logs do Azure Monitor.

## <a name="prerequisites"></a>Pré-requisitos

- [Azure Data Studio](download-azure-data-studio.md)
- [Python](https://www.python.org/downloads/)

## <a name="install-and-set-up-kqlmagic-in-a-notebook"></a>Instalar e configurar Kqlmagic em um notebook

Todas as etapas nesta seção são executadas dentro de um notebook do Azure Data Studio.

1. Crie um notebook e altere o **Kernel** para *Python 3*.

   ![Novo Notebook](media/notebooks-kql-magic/install-new-notebook.png)

2. Quando solicitado, selecione **Sim** para atualizar os pacotes de Python.

   ![Sim](media/notebooks-kql-magic/install-python-yes.png)

3. Instale Kqlmagic:

   ```python
   !pip install Kqlmagic --no-cache-dir --upgrade
   ```

   Verifique se ele está instalado:

   ```python
   !pip list
   ```

   ![Lista](media/notebooks-kql-magic/install-list.png)

4. Carregue Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   > [!Note]
   > Se essa etapa falhar, feche o arquivo e abra-o novamente.

   ![Carregar a extensão Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

5. Você pode testar se Kqlmagic foi carregado corretamente navegando pela documentação de ajuda ou verificando a versão.

   ```python
   %kql --help "help"
   ```

   > [!Note]
   > Se `Samples@help` solicitar uma senha, deixe-a em branco e pressione **Enter**.

   ![Ajuda](media/notebooks-kql-magic/install-help.png)

   Para ver qual versão de Kqlmagic está instalada, execute o comando a seguir.

   ```python
   %kql --version
   ```

## <a name="kqlmagic-with-an-azure-data-explorer-cluster"></a>Kqlmagic com um cluster do Azure Data Explorer

Esta seção explica como executar a análise de dados usando Kqlmagic com um cluster do Azure Data Explorer.

### <a name="load-and-authenticate-kqlmagic-for-azure-data-explorer"></a><a name="ade-load-auth"></a> Carregar e autenticar Kqlmagic para o Azure Data Explorer

   > [!Note]
   > Sempre que criar um notebook no Azure Data Studio, você precisará carregar a extensão Kqlmagic.

1. Verifique se o **Kernel** está definido como *Python3*.

   ![Novo Notebook](media/notebooks-kql-magic/change-kernel.png)

2. Carregue Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Carregar a extensão Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

3. Conectar-se ao cluster e autenticar:

   ```python
   %kql azureDataExplorer://code;cluster='help';database='Samples'
   ```

   Use o Logon do Dispositivo para se autenticar. Copie o código da saída e selecione **autenticar**, que abre um navegador no qual você precisa colar o código. Após autenticar-se com êxito, você pode voltar para o Azure Data Studio para continuar com o restante do script.

   ![Autenticação do Azure Data Explorer](media/notebooks-kql-magic/ade-auth.png)

### <a name="query-and-visualize-for-azure-data-explorer"></a>Consultar e visualizar no Azure Data Explorer

Consulte de dados usando o [operador renderizar](/azure/data-explorer/kusto/query/renderoperator) e visualize dados usando a biblioteca ploy.ly. Essa consulta e visualização fornece uma experiência integrada que usa um KQL nativo.

1. Analise os 10 principais eventos de tempestade por estado e frequência:

   ```python
   %kql StormEvents | summarize count() by State | sort by count_ | limit 10
   ```

   Se estiver familiarizado com o KQL (Linguagem de Consulta Kusto), digite a consulta após `%kql`.

   ![Analisar eventos de tempestade](media/notebooks-kql-magic/ade-analyze-storm-events.png)

2. Visualize um gráfico de linha do tempo:

   ```python
   %kql StormEvents \
   | summarize event_count=count() by bin(StartTime, 1d) \
   | render timechart title= 'Daily Storm Events'
   ```

   ![visualizar gráfico de tempo](media/notebooks-kql-magic/ade-visualize-timechart.png)

3. Exemplo de Consulta Multilinha usando `%%kql`.

   ```python
   %%kql
   StormEvents
   | summarize count() by State
   | sort by count_
   | limit 10
   | render columnchart title='Top 10 States by Storm Event count'
   ```

   ![Exemplo de Consulta Multilinha](media/notebooks-kql-magic/ade-multiline-query-sample.png)

## <a name="kqlmagic-with-application-insights"></a>Kqlmagic com Application Insights

### <a name="load-and-authenticate-kqlmagic-for-application-insights"></a><a name="appin-load-auth"></a> Carregar e autenticar Kqlmagic para o Application Insights

1. Verifique se o **Kernel** está definido como *Python3*.

   ![Novo Notebook](media/notebooks-kql-magic/change-kernel.png)

2. Carregue Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Carregar a extensão Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

   > [!Note]
   > Sempre que criar um notebook no Azure Data Studio, você precisará carregar a extensão Kqlmagic.

3. Conectar e autenticar.

   Primeiro será necessário gerar uma chave de API para seu recurso do Application Insights. Em seguida, use a ID do aplicativo e a chave de API para se conectar ao Application Insights do notebook:

   ```python
   %kql appinsights://appid='DEMO_APP';appkey='DEMO_KEY'
   ```


### <a name="query-and-visualize-for-application-insights"></a>Consultar e visualizar no Application Insights

Consulte de dados usando o [operador renderizar](/azure/data-explorer/kusto/query/renderoperator) e visualize dados usando a biblioteca ploy.ly. Essa consulta e visualização fornece uma experiência integrada que usa um KQL nativo.

1. Mostrar as Exibições de Página:

   ```python
   %%kql
   pageViews
   | limit 10
   ```

   ![Visualizações de página](media/notebooks-kql-magic/appin-page-views.png)

   > [!Note]
   > Use o mouse para arrastar em uma área do gráfico para ampliar as datas específicas.

2. Mostrar as exibições de página em um gráfico de linha do tempo:

   ```python
   %%kql
   pageViews
   | summarize event_count=count() by name, bin(timestamp, 1d)
   | render timechart title= 'Daily Page Views'
   ```

   ![Gráfico de linha do tempo](media/notebooks-kql-magic/appin-timechart.png)

## <a name="kqlmagic-with-azure-monitor-logs"></a>Kqlmagic com logs do Azure Monitor

### <a name="load-and-authenticate-kqlmagic-for-azure-monitor-logs"></a><a name="aml-load-auth"></a> Carregar e autenticar Kqlmagic para logs do Azure Monitor

1. Verifique se o **Kernel** está definido como *Python3*.

   ![Novo Notebook](media/notebooks-kql-magic/change-kernel.png)

2. Carregue Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Carregar a extensão Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

   > [!Note]
   > Sempre que criar um notebook no Azure Data Studio, você precisará carregar a extensão Kqlmagic.

3. Conectar-se e autenticar:

   ```python
   %kql loganalytics://workspace='DEMO_WORKSPACE';appkey='DEMO_KEY';alias='myworkspace'
   ```

   ![Autenticação do Log Analytics](media/notebooks-kql-magic/aml-auth.png)

### <a name="query-and-visualize-for-azure-monitor-logs"></a>Consultar e visualizar nos Logs do Azure Monitor

Consulte de dados usando o [operador renderizar](/azure/data-explorer/kusto/query/renderoperator) e visualize dados usando a biblioteca ploy.ly. Essa consulta e visualização fornece uma experiência integrada que usa um KQL nativo.

1. Exiba um gráfico de linha do tempo:

   ```python
   %%kql
   KubeNodeInventory
   | summarize event_count=count() by Status, bin(TimeGenerated, 1d)
   | render timechart title= 'Daily Kubernetes Nodes'
   ```

   ![Gráfico de tempo dos Nós de Kubernetes Diários do Log Analytics](media/notebooks-kql-magic/aml-timechart-daily-kubernetes-nodes.png)

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os notebooks e Kqlmagic:

- [Usar um Jupyter Notebook e a extensão Kqlmagic para analisar dados no Azure Data Explorer](/azure/data-explorer/Kqlmagic)
- [Extensão (Magic) para o Jupyter Notebook e o Jupyter Lab, que habilita a experiência de notebook trabalhando com o uso de dados do Kusto, do Application Insights e do LogAnalytics](https://github.com/Microsoft/jupyter-Kqlmagic)
- [Kqlmagic](https://pypi.org/project/Kqlmagic/)
- [KustoMagicSamples](https://notebooks.azure.com/RknDzgn/projects/KustoMagicSamples/html/Getting%20Started%20with%20Kqlmagic%20on%20Azure%20Data%20Explorer-Copy.ipynb)
- [Como usar notebooks no Azure Data Studio](notebooks-guidance.md)