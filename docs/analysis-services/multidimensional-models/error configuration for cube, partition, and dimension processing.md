---
title: "Configura&#231;&#227;o de erros para cubo, parti&#231;&#227;o e processamento da dimens&#227;o (SSAS - multidimensional) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.sqlserverstudio.cubeproperties.errorconfiguration.f1"
  - "sql13.asvs.sqlserverstudio.partitionproperties.errorconfiguration.f1"
  - "sql13.asvs.sqlserverstudio.dimensionproperties.errorconfiguration.f1"
ms.assetid: 3f442645-790d-4dc8-b60a-709c98022aae
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Configura&#231;&#227;o de erros para cubo, parti&#231;&#227;o e processamento da dimens&#227;o (SSAS - multidimensional)
  As propriedades de configuração de erro no cubo, na partição ou nos objetos de dimensão determinam como o servidor responde quando ocorrem erros de integridade de dados durante o processamento. As chaves duplicadas, chaves ausentes e os valores nulos em uma coluna de chave normalmente disparam esses erros, e embora o registro que cause o erro não seja adicionado ao banco de dados, você pode definir propriedades que determinam o que acontece em seguida. Por padrão, o processamento para. No entanto, durante o desenvolvimento do cubo, talvez você queira que o processamento continue quando ocorrerem os erros de forma que você possa testar comportamentos do cubo com dados importados, mesmo se estiverem incompletos.  
  
 Este tópico inclui as seguintes seções:  
  
-   [Ordem de execução](#bkmk_exec)  
  
-   [Comportamentos padrão](#bkmk_default)  
  
-   [Propriedades de configuração do erro](#bkmk_props)  
  
-   [Onde definir as propriedades de configuração do erro](#bkmk_tools)  
  
-   [Chaves ausentes (KeyNotFound)](#bkmk_missing)  
  
-   [Chaves estrangeiras nulas em uma tabela de fato (KeyNotFound)](#bkmk_nullfact)  
  
-   [Chaves nulas em uma dimensão](#bkmk_nulldim)  
  
-   [Relações inconsistentes resultantes de chaves duplicadas (KeyDuplicate)](#bkmk_dupe)  
  
-   [Modificar o limite do erro ou a ação de limite do erro](#bkmk_limit)  
  
-   [Definir o caminho do log de erros](#bkmk_log)  
  
-   [Próxima etapa](#bkmk_next)  
  
##  <a name="bkmk_exec"></a> Ordem de execução  
 O servidor sempre executa as regras de **NullProcessing** antes das regras de **ErrorConfiguration** para cada registro. Isso é importante entender porque as propriedades de processamento nulo que convertem nulos em zeros podem introduzir subsequentemente erros de chave duplicada quando dois ou mais registros de erro têm zero em uma coluna de chave.  
  
##  <a name="bkmk_default"></a> Comportamentos padrão  
 Por padrão, o processamento para no primeiro erro que implica uma coluna de chave. Esse comportamento é controlado por um limite de erros que especifica zero como o número de erros permitido e a política Parar processamento que diz ao servidor para parar o processamento quando o limite de erro é atingido.  
  
 Os registros que disparam um erro, devido aos valores nulos, ausentes ou duplicados, são convertidos para o membro desconhecido ou descartado. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não importará dados que violam restrições de integridade de dados.  
  
-   A conversão para o membro desconhecido ocorre por padrão, devido à configuração de **ConvertToUnknown** para **KeyErrorAction**. Os registros alocados para o membro desconhecido são colocados em quarentena no banco de dados como evidência de um problema que você pode querer investigar depois que o processamento for concluído.  
  
     Os membros desconhecidos são excluídos das cargas de trabalho de consulta, mas serão visíveis em alguns aplicativos cliente se **UnknownMember** for definido como **Visible**.  
  
     Se você quiser acompanhar quanto nulos foram convertidos para o membro desconhecido, poderá modificar a propriedade **NullKeyConvertedToUnknown** para relatar esses erros no log ou na janela Processamento.  
  
-   O descarte ocorre quando você define manualmente a propriedade **KeyErrorAction** como **DiscardRecord**.  
  
 Pelas propriedades da configuração de erro, você poderá determinar como o servidor responde quando ocorre um erro. As opções incluem parar o processamento imediatamente, continuar o processamento, mas parando de registrar em log ou continuar o processamento e o log de erros. As opções variam de acordo com a severidade do erro.  
  
 A contagem de erros controla o número de erros. Quando você define um limite superior, a resposta do servidor muda quando o limite é atingido. Por padrão, o servidor para o processamento depois que o limite é atingido. O limite padrão é 0, fazendo o processamento parar no primeiro erro que é contado.  
  
 Os erros de impacto alto, como uma chave ausente ou valor nulo em um campo de chave, devem ser resolvidos rapidamente. Por padrão, esses erros seguem os comportamentos do servidor **ReportAndContinue**, em que o servidor captura o erro, adiciona-o à contagem de erros e continua o processamento (a não ser que o limite de erros seja zero e, portanto, o processamento é interrompido imediatamente).  
  
 Outros erros são gerados, mas não são contados nem registrados em log por padrão (esta é a configuração **IgnoreError**), porque o erro não representa necessariamente um problema de integridade de dados.  
  
 As contagens de erro são afetadas pelas configurações de processamento nulo. Para atributos de dimensão, as opções de processamento nulo determinam como o servidor responde quando os valores nulos são encontrados. Por padrão, os nulos em uma coluna numérica são convertidos em zeros, enquanto que nulos em uma coluna de cadeia de caracteres são processados como cadeias de caracteres em branco. Você pode substituir as propriedades **NullProcessing** para capturar valores nulos antes que eles se transformem em erros **KeyNotFound** ou **KeyDuplicate**. Consulte [Chaves nulas em uma dimensão](#bkmk_nulldim) para obter detalhes.  
  
 Os erros são registrados na caixa de diálogo Processar, mas não são salvos. Você pode especificar um nome de arquivo de log de erros de chave para coletar erros em um arquivo de texto.  
  
##  <a name="bkmk_props"></a> Propriedades de configuração do erro  
 Há nove propriedades de configuração de erro. Cinco são usadas para determinar a resposta do servidor quando ocorre um erro específico. Os outros quatro seguem o escopo das cargas de trabalho da configuração de erro, como, por exemplo, quantos erros permitir, o que fazer quando o limite é atingido, se deve coletar erros em um arquivo de log.  
  
 **Resposta do servidor para erros específicos**  
  
|Propriedade|Default|Outros valores|  
|--------------|-------------|------------------|  
|**CalculationError**<br /><br /> Ocorre ao inicializar a configuração de erros.|**IgnoreError** não registra em log nem conta erros; o processamento continuará desde que a contagem de erro esteja abaixo do limite máximo.|**ReportAndContinue** registra em log e conta o erro.<br /><br /> **ReportAndStop** relata o erro e interrompe o processamento imediatamente, independentemente do limite de erros.|  
|**KeyNotFound**<br /><br /> Ocorre quando uma chave estrangeira em uma tabela de fatos não tem uma chave primária correspondente em uma tabela de dimensões relacionada (por exemplo, uma tabela de fatos de vendas tem um registro com uma ID de produto que não existe na tabela de dimensões de produto). Esse erro pode ocorrer durante o processamento da partição ou o processamento de dimensões floco de neve.|**ReportAndContinue** registra em log e conta o erro.|**ReportAndStop** relata o erro e interrompe o processamento imediatamente, independentemente do limite de erros.<br /><br /> **IgnoreError** não registra em log nem conta erros; o processamento continuará desde que a contagem de erro esteja abaixo do limite máximo. Os registros que disparam esse erro são convertidos para o membro desconhecido por padrão, mas você pode alterar a propriedade **KeyErrorAction** para rejeitá-los.|  
|**KeyDuplicate**<br /><br /> Ocorre quando as chaves de atributo duplicadas são encontradas em uma dimensão. Na maioria dos casos, é aceitável ter chaves de atributo duplicadas, mas esse erro informa sobre as duplicatas para que você possa verificar se há falhas de design na dimensão que possam resultar em relações inconsistentes entre atributos.|**IgnoreError** não registra em log nem conta erros; o processamento continuará desde que a contagem de erro esteja abaixo do limite máximo.|**ReportAndContinue** registra em log e conta o erro.<br /><br /> **ReportAndStop** relata o erro e interrompe o processamento imediatamente, independentemente do limite de erros.|  
|**NullKeyNotAllowed**<br /><br /> Ocorre quando **NullProcessing** = **Error** é definido em um atributo de dimensão ou quando há valores nulos em uma coluna de chave de atributo usados exclusivamente para identificar um membro.|**ReportAndContinue** registra em log e conta o erro.|**ReportAndStop** relata o erro e interrompe o processamento imediatamente, independentemente do limite de erros.<br /><br /> **IgnoreError** não registra em log nem conta erros; o processamento continuará desde que a contagem de erro esteja abaixo do limite máximo. Os registros que disparam esse erro são convertidos para o membro desconhecido por padrão, mas você pode definir a propriedade **KeyErrorAction** para descartá-los.|  
|**NullKeyConvertedToUnknown**<br /><br /> Ocorre quando os valores nulos são convertidos subsequentemente para o membro desconhecido. A configuração de **NullProcessing** = **ConvertToUnknown** em um atributo de dimensão disparará esse erro.|**IgnoreError** não registra em log nem conta erros; o processamento continuará desde que a contagem de erro esteja abaixo do limite máximo.|Se você considerar que esse erro é informativo, mantenha o padrão. Caso contrário, você pode escolher **ReportAndContinue** para relatar o erro para a janela Processamento e contar o erro até o limite de erros.<br /><br /> **ReportAndStop** relata o erro e interrompe o processamento imediatamente, independentemente do limite de erros.|  
  
 **Propriedades gerais**  
  
|**Propriedade**|**Valores**|  
|------------------|----------------|  
|**KeyErrorAction**|Esta é a ação executada pelo servidor quando um erro **KeyNotFound** ocorre. Respostas válidas para esse erro incluem **ConvertToUnknown** ou **DiscardRecord**.|  
|**KeyErrorLogFile**|Esse é um nome de arquivo definido pelo usuário que deve ter uma extensão de arquivo .log, localizado em uma pasta na qual a conta de serviço tem permissões de leitura/gravação. Este arquivo de log conterá somente os erros gerados durante o processamento. Use o Flight Recorder se precisar de informações mais detalhadas.|  
|**KeyErrorLimit**|Esse é o número máximo de erros de integridade de dados que o servidor permitirá antes da falha do processamento. Um valor -1 indica que não há limite. O padrão é 0, o que significa parar o processamento depois do primeiro erro. Você também pode defini-lo como um número inteiro.|  
|**KeyErrorLimitAction**|Esta é a ação executada pelo servidor quando o número de erros de chave atingiu o limite superior. Com a opção **Parar Processamento**, o processamento é encerrado imediatamente. Com a opção **Parar Log**, o processamento continuará, mas os erros não serão mais relatados nem contados.|  
  
##  <a name="bkmk_tools"></a> Onde definir as propriedades de configuração do erro  
 Use as páginas de propriedades de qualquer [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] depois que o banco de dados for implantado ou no projeto de modelo do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. As mesmas propriedades são encontradas em ambas as ferramentas. Você também poderá definir as propriedades de configuração de erro no arquivo msmdrsrv.ini para alterar os padrões do servidor para a configuração de erro e nos comandos **Batch** e **Process** se o processamento for executado como uma operação com script.  
  
 Você pode definir a configuração de erro em qualquer objeto que possa ser processado como uma operação autônoma.  
  
#### SQL Server Management Studio  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em **Propriedades** em um desses objetos: dimensão, cubo ou partição.  
  
2.  Em Propriedades, clique em **Configuração de Erro**.  
  
#### SQL Server Data Tools  
  
1.  Em Gerenciador de Soluções, clique duas vezes em uma dimensão ou cubo. **ErrorConfiguration** aparecerá nas Propriedades, no painel abaixo.  
  
2.  Como alternativa, para uma única dimensão, clique com o botão direito do mouse na dimensão no Gerenciador de Soluções e escolha **Processar** e **Alterar Configurações** na caixa de diálogo Processar Dimensão. As opções de configuração de erro aparecem na guia Erros de chave de dimensão.  
  
##  <a name="bkmk_missing"></a> Chaves ausentes (KeyNotFound)  
 Os registros com um valor de chave ausente não podem ser adicionados ao banco de dados, nem mesmo quando erros são ignorados ou o limite de erros é ilimitado.  
  
 O servidor gera o erro **KeyNotFound** durante o processamento da partição quando uma tabela no registro de fatos contém um valor de chave estrangeira, mas a chave estrangeira não tem nenhum registro correspondente na tabela de dimensões relacionada. Esse erro também ocorre ao processar as tabelas de dimensões relacionadas ou floco de neve, onde um registro em uma dimensão especifica uma chave estrangeira que não existe na dimensão relacionada.  
  
 Quando ocorre um erro **KeyNotFound**, o registro com problema é alocado para o membro desconhecido. Este comportamento é controlado por meio da **Ação da Tecla** definida como **ConvertToUnknown**, de modo que você possa exibir os registros alocados para realizar uma investigação extra.  
  
##  <a name="bkmk_nullfact"></a> Chaves estrangeiras nulas em uma tabela de fato (KeyNotFound)  
 Por padrão, um valor nulo em uma coluna de chave estrangeira de uma tabela de fatos é convertido em zero. Supondo que zero não seja um valor de chave estrangeira válido, o erro **KeyNotFound** será registrado e contado até o limite de erros, que é zero por padrão.  
  
 Para permitir que o processamento continue, você pode tratar o nulo antes de ser convertido e verificado em busca de erros. Para fazer isso, defina **NullProcessing** como **Error**.  
  
#### Definir a propriedade NullProcessing em uma medida  
  
1.  No SQL Server Data Tools, no Gerenciador de Soluções, clique duas vezes no cubo para abri-lo no Designer de Cubo.  
  
2.  Clique com o botão direito do mouse no painel Medidas e escolha **Propriedades**.  
  
3.  Em Propriedades, expanda **Origem** para exibir a propriedade **NullProcessing**. É definido como **Automático** por padrão, o que, para itens OLAP, converte valores nulos em zeros para os campos que contêm dados numéricos.  
  
4.  Altere o valor para **Erro** para excluir todos os registros que têm um valor nulo, impedindo a conversão nulo para numérico (zero). Essa modificação permite a prevenção de erros de chave duplicada relacionados a vários registros que têm zero na coluna de chave, além de erros **KeyNotFound** quando uma chave estrangeira de valor zero não tem nenhuma chave primária equivalente em uma tabela de dimensões relacionada.  
  
##  <a name="bkmk_nulldim"></a> Chaves nulas em uma dimensão  
 Para continuar o processamento quando forem encontrados valores nulos em chaves estrangeiras em uma dimensão floco de neve, trate primeiro os valores nulos definindo **NullProcessing** na **KeyColumn** do atributo de dimensão. Isso descarta ou converte o registro, antes que o erro **KeyNotFound** ocorra.  
  
 Você tem duas opções para tratar nulos no atributo de dimensão:  
  
-   Defina **NullProcessing**=**UnknownMember** para alocar registros com valores nulos para o membro desconhecido. Isso gera o erro **NullKeyConvertedToUnknown**, que é ignorado por padrão.  
  
-   Defina **NullProcessing**=**Error** para excluir registros com valores nulos. Isso gera o erro **NullKeyNotAllowed**, que é registrado e contado até o limite de erros de chave. Você pode definir a propriedade de configuração de erro em **Chave Nula Não Permitida** como **IgnoreError** para permitir que o processamento continue.  
  
 Os nulos podem ser problema para campos de não chave, porque as consultas MDX retornam resultados diferentes dependendo se o nulo é interpretado como zero ou vazio. Por esse motivo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece as opções de processamento nulo que permitem predefinir o comportamento de conversão que você deseja. Consulte [Definindo o membro desconhecido e as propriedades de processamento nulo](../../analysis-services/defining-the-unknown-member-and-null-processing-properties.md) e <xref:Microsoft.AnalysisServices.NullProcessing> para obter detalhes.  
  
#### Definir a propriedade NullProcessing em um atributo de dimensão  
  
1.  No SQL Server Data Tools, no Gerenciador de Soluções, clique duas vezes na dimensão para abri-lo no Designer de Dimensão.  
  
2.  Clique com o botão direito do mouse em um atributo do painel Atributos e escolha **Propriedades**.  
  
3.  Em Propriedades, expanda **KeyColumns** para exibir a propriedade **NullProcessing**. É definido como **Automático** por padrão, o que converte valores nulos em zeros para os campos que contêm dados numéricos. Altere o valor para **Error** ou **UnknownMember**.  
  
     Essa modificação remove as condições subjacentes que disparam **KeyNotFound**, descartando ou convertendo o registro antes que seja verificado em busca de erros.  
  
     Dependendo da configuração de erro, qualquer uma destas ações pode resultar em um erro que é relatado e contado. Talvez seja necessário ajustar propriedades adicionais, como definir **KeyNotFound** como **ReportAndContinue** ou **KeyErrorLimit** como um valor diferente de zero, para permitir que o processamento continue quando esses erros forem relatados e contados.  
  
##  <a name="bkmk_dupe"></a> Relações inconsistentes resultantes de chaves duplicadas (KeyDuplicate)  
 Por padrão, a presença de uma chave duplicada não para o processamento, mas o erro será ignorado e o registro duplicado será excluído do banco de dados.  
  
 Para alterar esse comportamento, defina **KeyDuplicate** como **ReportAndContinue** ou **ReportAndStop** para relatar o erro. Você pode examinar o erro para determinar as falhas potenciais no design da dimensão.  
  
##  <a name="bkmk_limit"></a> Modificar o limite do erro ou a ação de limite do erro  
 Você pode aumentar o limite de erros para permitir mais erros durante o processamento. Não há nenhuma orientação para aumentar o limite de erros; o valor apropriado variará dependendo de seu cenário. Os limites de erro são especificados como **KeyErrorLimit** nas propriedades de **ErrorConfiguration** no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou como **Número de erros** na guia Configuração de Erros das propriedades de dimensões, cubos ou grupos de medidas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Quando o limite de erros é atingido, você pode especificar que o processamento ou o registro em log pare. Por exemplo, suponha que você defina a ação como **StopLogging** em um limite de erros de 100. No erro de número 101, o processamento continuará, mas os erros não serão registrados ou contados. As ações de limites de erro são especificadas como **KeyErrorLimitAction** nas propriedades de **ErrorConfiguration** no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou como **Ação se houver erro** na guia Configuração de Erros das propriedades de dimensões, cubos ou grupos de medidas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="bkmk_log"></a> Definir o caminho do log de erros  
 Você pode especificar um arquivo para armazenar as mensagens de erro relacionadas à chave que são relatadas durante o processamento. Por padrão, os erros são visíveis durante o processamento interativo na janela Processar e, em seguida, rejeitado quando você fecha a janela ou sessão. O log conterá apenas as informações de erros relacionadas às chaves, idênticas aos erros que você vê relatado nas caixas de diálogo de processamento.  
  
 Os erros serão registrados em um arquivo de texto e devem ter a extensão de arquivo .log. O arquivo estará vazio a menos que ocorram erros. Por padrão, um arquivo será criado na pasta DATA. Você pode especificar outra pasta contanto que a conta de serviço do Analysis Services possa ser gravada nesse local.  
  
##  <a name="bkmk_next"></a> Próxima etapa  
 Decida se os erros pararão o processamento ou serão ignorados. Lembre-se de que somente o erro será ignorado. O registro que causou o erro não é ignorado; ele é descartado ou convertido em um membro desconhecido. Os registros que violam as regras de integridade de dados nunca são adicionados ao banco de dados. Por padrão, o processamento para quando o primeiro erro ocorre, mas você pode alterar isso aumentando o limite de erros. No desenvolvimento do cubo, poderá ser útil relaxar as regras de configuração de erro, permitindo que o processamento continue, de modo que haja dados para testar.  
  
 Decida se deseja alterar os comportamentos padrão de processamento de nulos. Por padrão, os nulos em uma coluna de cadeia de caracteres são processados como valores vazios, enquanto que os nulos em uma coluna numérica são processados como zero. Consulte [Definindo o membro desconhecido e as propriedades de processamento nulo](../../analysis-services/defining-the-unknown-member-and-null-processing-properties.md) para obter instruções sobre como definir o processamento nulo em um atributo.  
  
## Consulte também  
 [Propriedades do log ](../../analysis-services/server-properties/log-properties.md)   
 [Definindo o membro desconhecido e as propriedades de processamento nulo](../../analysis-services/defining-the-unknown-member-and-null-processing-properties.md)  
  
  