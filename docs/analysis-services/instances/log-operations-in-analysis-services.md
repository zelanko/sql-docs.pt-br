---
title: "Log de operações no Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aa1db060-95dc-4198-8aeb-cffdda44b140
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e23d96e675fba4ed740b8adbb8402d3ae7fd06e2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="log-operations-in-analysis-services"></a>Operações de log no Analysis Services
  Uma instância do Analysis Services registrará notificações do servidor, erros e avisos no arquivo msmdsrv.log, um para cada instância instalada. Os administradores consultam esse log para compreender eventos de rotina e extraordinários. Nas versões mais recentes, o registro em log foi aprimorado para incluir mais informações. Registros de log agora incluem informações de versão e edição do produto, bem como processador, memória, conectividade e eventos de bloqueio. Você pode revisar a lista inteira de alterações em [Aprimoramentos de log](http://support.microsoft.com/kb/2965035).  
  
 Além do recurso de registro em log integrado, muitos administradores e desenvolvedores também usam ferramentas fornecidas pela comunidade do Analysis Services para coletar dados sobre as operações do servidor, tal como o **ASTrace**. Consulte [Microsoft SQL Server Community Samples: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/) (Exemplos da Comunidade do Microsoft SQL Server: Analysis Services) para obter os links de download.  
  
 Este tópico contém as seguintes seções:  
  
-   [Local e tipos de logs](#bkmk_location)  
  
-   [Informações gerais sobre definições de configuração do arquivo de log](#bkmk_general)  
  
-   [Arquivo de log do serviço MSMDSRV](#bkmk_msmdsrv)  
  
-   [Logs de consulta](#bkmk_querylog)  
  
-   [Arquivos de minidespejo (.mdmp)](#bkmk_mdmp)  
  
-   [Dicas e práticas recomendadas](#bkmk_tips)  
  
> [!NOTE]  
>  Se você estiver procurando informações sobre o registro em log, talvez também esteja interessado no rastreamento de operações que mostram o processamento e caminhos de execução de consulta. Objetos de rastreamento para rastreamento ad hoc e persistente (como a auditoria de acesso de cubo), bem como recomendações sobre como usar melhor o Flight Recorder, SQL Server Profiler e xEvents, podem ser encontrados usando os links nesta página: [Monitorar uma instância do Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md).  
  
##  <a name="bkmk_location"></a> Local e tipos de logs  
 O Analysis Services fornece os logs descritos abaixo.  
  
|Nome ou local do arquivo|Tipo|Usado para|Ativado por padrão|  
|---------------------------|----------|--------------|-------------------|  
|Msmdsrv.log|Log de erros|Monitoramento de rotina e solução de problemas básicos|Sim|  
|Tabela OlapQueryLog em um banco de dados relacional|Log de consultas|Coletar entradas para o Assistente de Otimização do Uso|Não|  
|SQLDmp\<guid >. mdmp arquivos|Falhas e exceções|Solução de problemas detalhada|Não|  
  
 O link a seguir é altamente recomendável para a obtenção de recursos de informações adicionais que não são abordados neste tópico: [Dicas para coleta de dados inicial do Suporte da Microsoft](http://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx).  
  
##  <a name="bkmk_general"></a> Informações gerais sobre definições de configuração do arquivo de log  
 Você pode encontrar as seções para cada log no arquivo de configuração do servidor msmdsrv.ini, localizado na pasta \Arquivos de Programas\Microsoft SQL Server\MSAS13.MSSQLSERVER\OLAP\Config. Consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md) para obter instruções sobre como editar o arquivo.  
  
 Sugerimos que, se possível, defina as propriedades de log na página de propriedades de servidor do Management Studio. Exceto alguns casos, você deve editar o arquivo msmdsrv.ini diretamente para definir as configurações que não são visíveis nas ferramentas administrativas.  
  
 ![Seção do arquivo config mostrando as configurações de log](../../analysis-services/instances/media/ssas-logfilesettings.png "seção do arquivo config mostrando as configurações de log")  
  
##  <a name="bkmk_msmdsrv"></a> Arquivo de log do serviço MSMDSRV  
 Operações de servidor de logs do Analysis Services para o arquivo msmdsrv.log, um por instância, localizado em \arquivos de programas\Microsoft SQL Server\\<instância\>\Olap\Log.  
  
 Esse arquivo de log é esvaziado em cada reinicialização do serviço. Em versões anteriores, os administradores às vezes reiniciavam o serviço com o único propósito de eliminar o arquivo de log antes que ele crescesse excessivamente a ponto de se tornar inutilizável. Isso não é mais necessário. As definições de configuração, apresentadas no SQL Server 2012 SP2 e versões posteriores, oferecem controle sobre o tamanho do arquivo de log e seu histórico:  
  
-   O**MaxFileSizeMB** especifica o tamanho máximo do arquivo de log em megabytes. O padrão é 256. Um valor de substituição válido deve ser um inteiro positivo. Quando **MaxFileSizeMB** é atingido, o Analysis Services renomeia o arquivo atual como um arquivo do msmdsrv{carimbo de data e hora atual}.log e inicia um novo arquivo msmdsrv.log.  
  
-   O**MaxNumberFiles** especifica a retenção de arquivos de log antigos. O padrão é 0 (desabilitado). Você pode alterá-lo como um inteiro positivo para manter as versões do arquivo de log. Quando **MaxNumberFiles** é atingido, o Analysis Services exclui o arquivo com o carimbo de date e hora mais antigo em seu nome.  
  
 Para usar essas configurações, faça o seguinte:  
  
1.  Abra o msmdsrv.ini no Bloco de Notas.  
  
2.  Copie as duas linhas a seguir:  
  
    ```  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    ```  
  
3.  Cole as duas linhas na seção de Log do msmdsrv.ini, abaixo do nome de arquivo para msmdsrv.log. Ambas as configurações devem ser adicionadas manualmente. Não há nenhum espaço reservado para eles no arquivo msmdsrv.ini.  
  
     O arquivo de configuração alterado deve se parecer com o seguinte:  
  
    ```  
    <Log>  
    <File>msmdsrv.log</File>  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    <FileBufferSize>0</FileBufferSize>  
  
    ```  
  
4.  Edite os valores se aqueles fornecidos forem diferentes do esperado.  
  
5.  Salve o arquivo.  
  
6.  Reinicie o serviço.  
  
##  <a name="bkmk_querylog"></a> Logs de consulta  
 O log de consulta é um nome um tanto inapropriado, pois ele não registra a atividade de consulta MDX ou DAX dos usuários. Em vez disso, ele coleta dados sobre consultas geradas pelo Analysis Services, que são subsequentemente utilizadas como entrada de dados no Assistente de Otimização com Base no Uso. Os dados coletados no log de consultas não se destina à análise direta. Especificamente, os conjuntos de dados são descritos em matrizes de bits, com um zero ou um que indica as partes do conjunto de dados incluídas na consulta. Novamente, esses dados destinam-se ao assistente.  
  
 Para monitorar e solucionar problemas de consulta, muitos desenvolvedores e administradores usam uma ferramenta da comunidade, **ASTrace**, para monitorar consultas. Você também pode usar o SQL Server Profiler, xEvents ou um rastreamento do Analysis Services. Consulte [Monitorar uma instância do Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md) para ver links com mais informações sobre rastreamento.  
  
 Quando você deve usar o log de consulta? É recomendável habilitar o log de consulta como parte de um exercício de ajuste de desempenho de consulta que inclui o Assistente de Otimização com Base no Uso. O log de consultas não existe até você habilitar o recurso, criar as estruturas de dados para dar suporte a ele e definir as propriedades usadas pelo Analysis Services para localizar e preencher o log.  
  
 Para habilitar o log de consulta, siga estas etapas:  
  
1.  Crie um banco de dados relacional do SQL Server para armazenar o log de consulta.  
  
2.  Conceda permissões suficientes à conta de serviço do Analysis Services no banco de dados. A conta precisa de permissão para criar uma tabela, gravar na tabela e ler da tabela.  
  
3.  No SQL Server Management Studio, clique com o botão direito do mouse em **Analysis Services** | **Propriedades** | **Geral**, então defina **CreateQueryLogTable** como verdadeiro.  
  
4.  Opcionalmente, altere **QueryLogSampling** ou **QueryLogTableName** se desejar ver exemplos de consultas em uma taxa diferente ou use um nome diferente para a tabela.  
  
 A tabela de log de consulta não será criada até você executar consultas MDX suficientes para cumprir os requisitos de amostragem. Por exemplo, se você mantiver o valor padrão de 10, deverá executar pelo menos 10 consultas antes que a tabela seja criada.  
  
 Configurações de log de consulta são do servidor inteiro. As configurações que você especifica serão usadas por todos os bancos de dados em execução neste servidor.  
  
 ![Consultar as configurações de log no Management Studio](../../analysis-services/instances/media/ssas-querylogsettings.png "configurações de log de consulta no Management Studio")  
  
 Após as definições de configurações serem especificadas, execute uma consulta MDX várias vezes. Se a amostragem for definida como 10, execute a consulta 11 vezes.Verifique se que a tabela é criada. No Management Studio, conecte-se ao mecanismo de banco de dados relacional, abra a pasta do banco de dados, abra a pasta **Tabelas** e verifique se **OlapQueryLog** existe. Se você não puder encontrar a tabela imediatamente, atualize a pasta para acompanhar as alterações no seu conteúdo.  
  
 Permita que o log de consulta acumule dados suficientes para o Assistente de Otimização com Base no Uso. Se os volumes de consulta forem cíclicos, capture tráfego suficiente para ter um conjunto representativo dos dados. Consulte [Assistente de Otimização com Base no Uso](https://msdn.microsoft.com/library/ms189706.aspx) para obter instruções sobre como executar o assistente.  
  
 Consulte [Configurando o log de consulta do Analysis Services](http://technet.microsoft.com/library/Cc917676) para saber mais sobre a configuração de logs de consulta. Embora o documento seja bastante antigo, a configuração de logs de consulta não foi alterada nas versões recentes e as informações que ele contém ainda se aplicam.  
  
##  <a name="bkmk_mdmp"></a> Arquivos de minidespejo (.mdmp)  
 Arquivos de despejo capturam dados usados para analisar eventos extraordinários. O Analysis Services gera minidespejos (.mdmp) automaticamente em resposta a uma falha do servidor, exceções e alguns erros de configuração. O recurso está habilitado, mas não envia automaticamente relatórios de falha.  
  
 Relatórios de falha são configurados por meio da seção Exceção no arquivo Msmdsrv.ini. Essas configurações controlam a criação do arquivo de despejo de memória. O trecho de código a seguir mostra os valores padrão:  
  
```  
<Exception>  
<CreateAndSendCrashReports>1</CreateAndSendCrashReports>  
<CrashReportsFolder/>  
<SQLDumperFlagsOn>0x0</SQLDumperFlagsOn>  
<SQLDumperFlagsOff>0x0</SQLDumperFlagsOff>  
<MiniDumpFlagsOn>0x0</MiniDumpFlagsOn>  
<MiniDumpFlagsOff>0x0</MiniDumpFlagsOff>  
<MinidumpErrorList>0xC1000000, 0xC1000001, 0xC102003F, 0xC1360054, 0xC1360055</MinidumpErrorList>  
<ExceptionHandlingMode>0</ExceptionHandlingMode>  
<CriticalErrorHandling>1</CriticalErrorHandling>  
<MaxExceptions>500</MaxExceptions>  
<MaxDuplicateDumps>1</MaxDuplicateDumps>  
</Exception>  
```  
  
 **Configurar relatórios de falha**  
  
 Salvo orientação em contrário pelo Suporte da Microsoft, a maioria dos administradores usam as configurações padrão. Este artigo mais antigo da Base de Dados de Conhecimento ainda é usado para fornecer instruções sobre como configurar arquivos de despejo: [Como configurar o Analysis Services para gerar arquivos de despejo de memória](http://support.microsoft.com/kb/919711).  
  
 A definição de configuração tem mais probabilidade de ser modificada é a **CreateAndSendCrashReports** usada para determinar se um arquivo de despejo de memória será gerado.  
  
|Value|Descrição|  
|-----------|-----------------|  
|0|Desativa o arquivo de despejo de memória. Todas as outras configurações na seção Exceção são ignoradas.|  
|1|(Padrão) Habilita, mas não envia o arquivo de despejo de memória.|  
|2|Habilita e envia automaticamente um relatório de erros à Microsoft.|  
  
 **CrashReportsFolder** é o local dos arquivos de despejo de memória. Por padrão, um arquivo .mdmp e os registros de log associados podem ser encontrados na pasta \Olap\Log.  
  
 **SQLDumperFlagsOn** é usado para gerar um despejo completo. Por padrão, os despejos completos não estão habilitados. Você pode definir essa propriedade para **0x34**.  
  
 Os links a seguir fornecem mais informações:  
  
-   [Procurando mais profundo no SQL Server usando minidespejos](http://blogs.msdn.com/b/sqlcat/archive/2009/09/11/looking-deeper-into-sql-server-using-minidumps.aspx)  
  
-   [Como criar um arquivo de despejo do modo de usuário](http://support.microsoft.com/kb/931673)  
  
-   [Como usar o utilitário Sqldumper.exe para gerar um arquivo de despejo no SQL Server](http://support.microsoft.com/kb/917825)  
  
##  <a name="bkmk_tips"></a> Dicas e práticas recomendadas  
 Esta seção é uma recapitulação das dicas mencionadas neste artigo.  
  
-   Configure o arquivo msmdsrv.log para controlar o tamanho e o número de arquivos de log msmdsrv. As configurações não estão habilitadas por padrão, portanto certifique-se de adicioná-las como uma etapa pós-instalação. Consulte [Arquivo de log do serviço MSMDSRV](#bkmk_msmdsrv) neste tópico.  
  
-   Examine esta postagem de blog do Atendimento ao Cliente da Microsoft para saber quais recursos eles usam para obter informações sobre as operações do servidor: [Coleta inicial de dados](http://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)  
  
-   Use ASTrace2012 em vez de um log de consulta para descobrir o que está consultando cubos. O log de consultas normalmente é usado para fornecer sugestões para o Assistente de Otimização com Base no Uso e os dados capturados não são fácil de ler ou interpretar. O ASTrace2012 é uma ferramenta de comunidade, amplamente utilizada, que captura as operações de consulta. Consulte [Microsoft SQL Server Community Samples: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/)(Exemplos da comunidade do Microsoft SQL Server: Analysis Services).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de instância do Analysis Services](../../analysis-services/instances/analysis-services-instance-management.md)   
 [Introdução ao monitoramento do Analysis Services com o SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)   
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  

