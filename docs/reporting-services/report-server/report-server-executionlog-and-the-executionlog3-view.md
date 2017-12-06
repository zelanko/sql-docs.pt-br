---
title: "ExecutionLog do servidor de relatório e exibição do ExecutionLog3 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [Reporting Services], execution
- execution logs [Reporting Services]
ms.assetid: a7ead67d-1404-4e67-97e7-4c7b0d942070
caps.latest.revision: "41"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 8458127daae58d63376f80dc1b67302928f9f943
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="report-server-executionlog-and-the-executionlog3-view"></a>ExecutionLog do servidor de relatório e exibição do ExecutionLog3
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o log de execução do servidor de relatório contém informações sobre os relatórios executados no servidor ou em vários servidores em uma implantação em expansão no modo nativo ou no farm do SharePoint. É possível usar o log de execução de relatório para descobrir a frequência na qual um relatório é solicitado, quais são os formatos de saída mais usados e qual é o tempo de processamento em milissegundos em cada fase do processamento. O log contém informações sobre o período de tempo gasto na execução da consulta do conjunto de dados de um relatório e a hora gasta no processamento dos dados. Se você for um administrador de servidor de relatório, poderá revisar as informações de log, identificar tarefas demoradas e dar sugestões aos autores de relatório sobre as áreas do relatório (conjunto de dados ou processamento) que eles podem melhorar.  
  
 Os servidores de relatório configurados no modo do SharePoint também podem utilizar os logs ULS do SharePoint. Para obter mais informações, consulte [Ativar eventos do Reporting Services para o log de rastreamento do SharePoint &#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)  
  
##  <a name="bkmk_top"></a> Exibindo as informações do log  
 A execução do servidor de relatório registra dados sobre execução de relatório em uma tabela de banco de dados interna. As informações da tabela estão disponíveis nas exibições do SQL Server.  
  
 O log de execução de relatório é armazenado no banco de dados do servidor de relatório que, por padrão, é denominado **ReportServer**. As exibições SQL fornecem as informações do log de execução. As exibições “2” e “3” foram adicionadas às versões mais recentes e contêm novos campos ou contêm campos com nomes mais amigáveis que as versões anteriores. As exibições mais antigas permanecem no produto; portanto, os aplicativos que dependem delas não são impactados. Se você não tem uma dependência em uma exibição mais antiga, por exemplo, ExecutionLog, é recomendável que use a exibição mais recente, ExecutionLog**3**.  
  
 Neste tópico:  
  
-   [Configurações de um servidor de relatório no modo SharePoint](#bkmk_sharepoint)  
  
-   [Configurações de um servidor de relatório no modo nativo](#bkmk_native)  
  
-   [Campos de log (ExecutionLog3)](#bkmk_executionlog3)  
  
-   [O campo AdditionalInfo](#bkmk_additionalinfo)  
  
-   [Campos de log (ExecutionLog2)](#bkmk_executionlog2)  
  
-   [Campos de log (ExecutionLog)](#bkmk_executionlog)  
  
##  <a name="bkmk_sharepoint"></a> Configurações de um servidor de relatório no modo SharePoint  
 Você pode ativar ou desativar a execução de relatório nas configurações de sistema de um aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Por padrão, as entradas de log são mantidas por 60 dias. Entradas que excedem essa data são removidas às 2h00 diariamente. Em uma instalação madura, somente 60 dias de informações estarão disponíveis em um dado momento.  
  
 Não é possível definir limites para o número de linhas ou o tipo de entradas registradas.  
  
 **Para habilitar o log de execução:**  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar aplicativos de serviço** no grupo **Gerenciamento de Aplicativos** .  
  
2.  Clique no nome do aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a ser configurado.  
  
3.  Clique em **Configurações do Sistema**.  
  
4.  Selecione **Habilitar Log de Execução** na seção **Log** .  
  
5.  Clique em **OK**.  
  
 **Para habilitar o log detalhado:**  
  
 Você precisa habilitar o log conforme descrito nas etapas anteriores e concluir as seguintes etapas:  
  
1.  Na página **Configurações do Sistema** do aplicativo de serviços [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , localize a seção **Definido pelo usuário** .  
  
2.  Altere o **ExecutionLogLevel** para **detalhado**. Esse é um campo de entrada de texto, e os dois valores possíveis são **detalhado** e **normal**.  
  
##  <a name="bkmk_native"></a> Configurações de um servidor de relatório no modo nativo  
 Você pode ativar ou desativar o log de execução de relatório na página de Propriedades do Servidor do SQL Server Management Studio. O **EnableExecutionLogging** é uma propriedade avançada.  
  
 Por padrão, as entradas de log são mantidas por 60 dias. Entradas que excedem essa data são removidas às 2h00 diariamente. Em uma instalação madura, somente 60 dias de informações estarão disponíveis em um dado momento.  
  
 Não é possível definir limites para o número de linhas ou o tipo de entradas registradas.  
  
 **Para habilitar o log de execução:**  
  
1.  Inicie o SQL Server Management Studio com privilégios administrativos. Por exemplo, clique com o botão direito do mouse no ícone do Management Studio e clique em ‘Executar como administrador’.  
  
2.  Conecte-se ao servidor de relatório desejado.  
  
3.  Clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**. Se a opção Propriedades for desabilitada, verifique se você executou o SQL Server Management Studio com privilégios administrativos.  
  
4.  Clique na página **Log** .  
  
5.  Selecione **Habilitar log de execução de relatório**.  
  
 **Para habilitar o log detalhado:**  
  
 Você precisa habilitar o log conforme descrito nas etapas anteriores e concluir as seguintes etapas:  
  
1.  Na caixa de diálogo **Propriedades do Servidor** , clique na página **Avançado** .  
  
2.  Na seção **Definido pelo usuário** , altere o **ExecutionLogLevel** para **detalhado**. Esse é um campo de entrada de texto, e os dois valores possíveis são **detalhado** e **normal**.  
  
##  <a name="bkmk_executionlog3"></a> Campos de log (ExecutionLog3)  
 Esta exibição adicionou o nó de diagnóstico de desempenho adicional à coluna **AdditionalInfo** baseada em XML. A coluna AdditionalInfo contém uma estrutura XML de 1 para muitos campos adicionais de informação. Este é um exemplo de instrução Transact-SQL para recuperar linhas da exibição ExecutionLog3. O exemplo presume que o nome do banco de dados do servidor de relatório seja **ReportServer**:  
  
```  
Use ReportServer  
select * from ExecutionLog3 order by TimeStart DESC  
```  
  
 A tabela a seguir descreve os dados capturados no log de execução de relatório  
  
|Coluna|Description|  
|------------|-----------------|  
|InstanceName|Nome da instância de servidor de relatório que manipulou a solicitação. Se seu ambiente tiver mais de um servidor de relatório, você poderá analisar a distribuição de InstanceName para monitorar e determinar se o balanceador da carga de rede distribui solicitações pelos servidores de relatório conforme esperado.|  
|ItemPath|Caminho onde um relatório ou item de relatório é armazenado.|  
|UserName|Identificador do usuário.|  
|ExecutionID|O identificador interno associado a uma solicitação. Solicitações nas mesmas sessões de usuário compartilham a mesma id de execução.|  
|RequestType|Valores possíveis:<br /><br /> Interativo<br /><br /> Assinatura<br /><br /> <br /><br /> A análise dos dados de log filtrados por RequestType=Subscription e classificados por TimeStart pode revelar períodos de uso de assinatura pesados e talvez você queira modificar algumas assinaturas de relatório para um horário diferente.|  
|Formato|Formato de renderização.|  
|Parâmetros|Valores de parâmetro usados em uma execução de relatório.|  
|ItemAction|Valores possíveis:<br /><br /> Renderizar<br /><br /> Sort<br /><br /> BookMarkNavigation<br /><br /> DocumentNavigation<br /><br /> GetDocumentMap<br /><br /> Findstring<br /><br /> Execute (executar)<br /><br /> RenderEdit|  
|TimeStart|Horas de início e parada que indicam a duração de um processo de relatório.|  
|TimeEnd||  
|TimeDataRetrieval|Número de milissegundos gastos na recuperação dos dados.|  
|TimeProcessing|Número de milissegundos gastos no processamento do relatório.|  
|TimeRendering|Número de milissegundos gastos na renderização do relatório.|  
|Origem|Fonte da execução de relatório. Valores possíveis:<br /><br /> Dinâmica<br /><br /> Cache: indica uma execução em cache, por exemplo, consultas do conjunto de dados não são executadas ao vivo.<br /><br /> Instantâneo<br /><br /> Histórico<br /><br /> AdHoc: indica um modelo de relatório gerado dinamicamente com base no relatório detalhado ou um relatório do Construtor de Relatórios que é visualizado em um cliente utilizando o servidor de relatório para processamento e renderização.<br /><br /> Sessão: indica uma solicitação de acompanhamento em uma sessão já estabelecida.  Por exemplo, a solicitação inicial é exibir página 1 e a solicitação de acompanhamento é exportar para o Excel com o estado de sessão atual.<br /><br /> Rdce: indica uma extensão de personalização de definição de relatório. Uma extensão personalizada RDCE pode personalizar uma definição de relatório dinamicamente antes de ela ser passada ao mecanismo de processamento mediante a execução do relatório.|  
|Status|Status (rsSuccess ou um código de erro; se vários erros ocorrerem, só o primeiro erro será registrado).|  
|ByteCount|Tamanho de relatórios renderizados em bytes.|  
|RowCount|Número de linhas retornadas pelas consultas.|  
|AdditionalInfo|Um conjunto de propriedades XML contendo informações adicionais sobre a execução. O conteúdo pode ser diferente para cada linha.|  
  
##  <a name="bkmk_additionalinfo"></a> O campo AdditionalInfo  
 O campo AdditionalInfo é uma estrutura ou um conjunto de propriedades XML contendo informações adicionais sobre a execução. O conteúdo pode ser diferente para cada linha do log.  
  
 A seguir estão exemplos de conteúdo do campo AddtionalInfo para registro em log padrão e detalhado:  
  
 **Exemplo de registro em log padrão de AddtionalInfo**  
  
```  
<AdditionalInfo>  
  <ProcessingEngine>2</ProcessingEngine>  
  <ScalabilityTime>  
    <Pagination>0</Pagination>  
    <Processing>0</Processing>  
  </ScalabilityTime>  
  <EstimatedMemoryUsageKB>  
    <Pagination>0</Pagination>  
    <Processing>6</Processing>  
  </EstimatedMemoryUsageKB>  
  <DataExtension>  
    <SQL>1</SQL>  
  </DataExtension>  
  <Connections>  
    <Connection>  
      <ConnectionOpenTime>147</ConnectionOpenTime>  
      <DataSets>  
        <DataSet>  
          <Name>DataSet1</Name>  
          <RowsRead>16</RowsRead>  
          <TotalTimeDataRetrieval>642</TotalTimeDataRetrieval>  
          <ExecuteReaderTime>63</ExecuteReaderTime>  
        </DataSet>  
        <DataSet>  
          <Name>DataSet2</Name>  
          <RowsRead>3</RowsRead>  
          <TotalTimeDataRetrieval>157</TotalTimeDataRetrieval>  
          <ExecuteReaderTime>60</ExecuteReaderTime>  
        </DataSet>  
      </DataSets>  
    </Connection>  
  </Connections>  
</AdditionalInfo>  
  
```  
  
 **Exemplo de registro em log detalhado de AdditionalInfo**  
  
```  
<AdditionalInfo>  
  <ProcessingEngine>2</ProcessingEngine>  
  <ScalabilityTime>  
    <Pagination>0</Pagination>  
    <Processing>0</Processing>  
  </ScalabilityTime>  
  <EstimatedMemoryUsageKB>  
    <Pagination>0</Pagination>  
    <Processing>6</Processing>  
  </EstimatedMemoryUsageKB>  
  <DataExtension>  
    <SQL>1</SQL>  
  </DataExtension>  
  <Connections>  
    <Connection>  
      <ConnectionOpenTime>127</ConnectionOpenTime>  
      <DataSource>  
        <Name>DataSource1</Name>  
        <DataExtension>SQL</DataExtension>  
      </DataSource>  
      <DataSets>  
        <DataSet>  
          <Name>DataSet1</Name>  
          <RowsRead>16</RowsRead>  
          <TotalTimeDataRetrieval>655</TotalTimeDataRetrieval>  
          <QueryPrepareAndExecutionTime>94</QueryPrepareAndExecutionTime>  
          <ExecuteReaderTime>33</ExecuteReaderTime>  
          <DataReaderMappingTime>30</DataReaderMappingTime>  
          <DisposeDataReaderTime>1</DisposeDataReaderTime>  
        </DataSet>  
        <DataSet>  
          <Name>DataSet2</Name>  
          <RowsRead>3</RowsRead>  
          <TotalTimeDataRetrieval>16</TotalTimeDataRetrieval>  
          <QueryPrepareAndExecutionTime>2</QueryPrepareAndExecutionTime>  
          <ExecuteReaderTime>1</ExecuteReaderTime>  
          <DataReaderMappingTime>0</DataReaderMappingTime>  
          <DisposeDataReaderTime>0</DisposeDataReaderTime>  
        </DataSet>  
      </DataSets>  
    </Connection>  
  </Connections>  
</AdditionalInfo>  
  
```  
  
 A seguir está alguns dos valores que você verá no campo AdditionalInfo:  
  
-   **ProcessingEngine**  
  
     1=SQL Server 2005, 2=O novo Mecanismo de Processamento sob Demanda. Se a maioria de seus relatórios ainda estiver mostrando o valor 1, você poderá investigar como reprojetá-los para que utilizem o mecanismo de processamento sob demanda mais novo e eficiente.  
  
     `<ProcessingEngine>2</ProcessingEngine>`  
  
-   **ScalabilityTime**  
  
     O número de milissegundos gastos na execução de operações de escala relacionadas no mecanismo de processamento. O valor 0 indica que nenhuma hora adicional foi gasta em operações de escala; indica também que a solicitação não estava sob pressão de memória.  
  
    ```  
    <ScalabilityTime>  
        <Processing>0</Processing>  
    </ScalabilityTime>  
    ```  
  
-   **EstimatedMemoryUsageKB**  
  
     Uma estimativa da quantidade máxima de memória, em quilobytes, consumida por cada componente durante uma solicitação específica.  
  
    ```  
    <EstimatedMemoryUsageKB>  
        <Processing>38</Processing>  
    </EstimatedMemoryUsageKB>  
    ```  
  
-   **DataExtension**  
  
     Os tipos de extensões de dados ou fontes de dados usados no relatório. O número é uma contagem do número de ocorrências da fonte de dados específica.  
  
    ```  
    <DataExtension>  
       <DAX>2</DAX>  
    </DataExtension>  
    ```  
  
-   **ExternalImages**  
  
     Adicionado [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
     O valor está em milissegundos. Esses dados podem ser usados para diagnosticar problemas de desempenho. A hora necessária para recuperar imagens de um servidor Web externo pode tornar lenta a execução de relatório geral.  
  
    ```  
    <ExternalImages>  
        <Count>3</Count>  
        <ByteCount>9268</ByteCount>  
        <ResourceFetchTime>9</ResourceFetchTime>  
    </ExternalImages>  
    ```  
  
-   **Conexões**  
  
     Adicionado [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
     Uma estrutura em vários níveis  
  
    ```  
    <Connections>  
        <Connection>  
          <ConnectionOpenTime>127</ConnectionOpenTime>  
          <DataSource>  
            <Name>DataSource1</Name>  
            <DataExtension>SQL</DataExtension>  
          </DataSource>  
          <DataSets>  
            <DataSet>  
              <Name>DataSet1</Name>  
              <RowsRead>16</RowsRead>  
              <TotalTimeDataRetrieval>655</TotalTimeDataRetrieval>  
              <QueryPrepareAndExecutionTime>94</QueryPrepareAndExecutionTime>  
              <ExecuteReaderTime>33</ExecuteReaderTime>  
              <DataReaderMappingTime>30</DataReaderMappingTime>  
              <DisposeDataReaderTime>1</DisposeDataReaderTime>  
            </DataSet>  
            <DataSet>  
              <Name>DataSet2</Name>  
              <RowsRead>3</RowsRead>  
              <TotalTimeDataRetrieval>16</TotalTimeDataRetrieval>  
              <QueryPrepareAndExecutionTime>2</QueryPrepareAndExecutionTime>  
              <ExecuteReaderTime>1</ExecuteReaderTime>  
              <DataReaderMappingTime>0</DataReaderMappingTime>  
              <DisposeDataReaderTime>0</DisposeDataReaderTime>  
            </DataSet>  
          </DataSets>  
        </Connection>  
    </Connections>  
  
    ```  
  
##  <a name="bkmk_executionlog2"></a> Campos de log (ExecutionLog2)  
 Esta exibição adicionou alguns campos novos e renomeou outros. Este é um exemplo de instrução Transact-SQL para recuperar linhas da exibição ExecutionLog2. O exemplo presume que o nome do banco de dados do servidor de relatório seja **ReportServer**:  
  
```  
Use ReportServer  
select * from ExecutionLog2 order by TimeStart DESC  
```  
  
 A tabela a seguir descreve os dados capturados no log de execução de relatório  
  
|Coluna|Description|  
|------------|-----------------|  
|InstanceName|Nome da instância de servidor de relatório que manipulou a solicitação.|  
|ReportPath|A estrutura de caminho para o relatório.  Por exemplo, um relatório chamado ”test”, que está na pasta raiz do Gerenciador de Relatórios, teria um ReportPath “/test”.<br /><br /> Um relatório chamado “test”, salvo na pasta “samples” do Gerenciador de Relatórios, terá o ReportPath “/Samples/test/”|  
|UserName|Identificador do usuário.|  
|ExecutionID||  
|RequestType|Tipo de solicitação (usuário ou sistema).|  
|Formato|Formato de renderização.|  
|Parâmetros|Valores de parâmetro usados em uma execução de relatório.|  
|ReportAction|Valores possíveis: Render, Sort, BookMarkNavigation, DocumentNavigation, GetDocumentMap, Findstring|  
|TimeStart|Horas de início e parada que indicam a duração de um processo de relatório.|  
|TimeEnd||  
|TimeDataRetrieval|Número de milissegundos gastos na recuperação dos dados, no processamento do relatório e na renderização do relatório.|  
|TimeProcessing||  
|TimeRendering||  
|Origem|Fonte da execução de relatório (1=Ativo, 2=Cache, 3=Instantâneo, 4=Histórico).|  
|Status|Status (rsSuccess ou um código de erro; se vários erros ocorrerem, só o primeiro erro será registrado).|  
|ByteCount|Tamanho de relatórios renderizados em bytes.|  
|RowCount|Número de linhas retornadas pelas consultas.|  
|AdditionalInfo|Um conjunto de propriedades XML contendo informações adicionais sobre a execução.|  
  
##  <a name="bkmk_executionlog"></a> Campos de log (ExecutionLog)  
 Este é um exemplo de instrução Transact-SQL para recuperar linhas da exibição ExecutionLog. O exemplo presume que o nome do banco de dados do servidor de relatório seja **ReportServer**:  
  
```  
Use ReportServer  
select * from ExecutionLog order by TimeStart DESC  
  
```  
  
 A tabela a seguir descreve os dados capturados no log de execução de relatório  
  
|Coluna|Description|  
|------------|-----------------|  
|InstanceName|Nome da instância de servidor de relatório que manipulou a solicitação.|  
|ReportID|Identificador do relatório.|  
|UserName|Identificador do usuário.|  
|RequestType|Valores possíveis:<br /><br /> True = Uma solicitação de assinatura<br /><br /> False = Uma solicitação interativa|  
|Formato|Formato de renderização.|  
|Parâmetros|Valores de parâmetro usados em uma execução de relatório.|  
|TimeStart|Horas de início e parada que indicam a duração de um processo de relatório.|  
|TimeEnd||  
|TimeDataRetrieval|Número de milissegundos gastos na recuperação dos dados, no processamento do relatório e na renderização do relatório.|  
|TimeProcessing||  
|TimeRendering||  
|Origem|Fonte da execução de relatório. Valores possíveis: (1=Ativo, 2=Cache, 3=Instantâneo, 4=Histórico, 5=Adhoc, 6=Sessão, 7=RDCE).|  
|Status|Valores possíveis: rsSuccess, rsProcessingAborted ou um código de erro. Se vários erros ocorrerem, só o primeiro erro será registrado.|  
|ByteCount|Tamanho de relatórios renderizados em bytes.|  
|RowCount|Número de linhas retornadas pelas consultas.|  
  
## <a name="see-also"></a>Consulte também  
 [Ativar eventos do Reporting Services para o log de rastreamento do SharePoint &#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)   
 [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Referência de erros e eventos &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
