---
title: "AMO outras Classes e métodos | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- restores [AMO]
- AMO, backup and restore
- capture logs [AMO]
- AmoException class [AMO]
- Analysis Management Objects, backup and restore
- assembly objects [AMO]
- traces [AMO]
- backups [AMO]
ms.assetid: 60ed5cfa-3a03-4161-8271-0a71a3ae363b
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f4de10c612f0338cecbfbd2e106bee41c6115905
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="amo-other-classes-and-methods"></a>Outras classes e métodos AMO
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Esta seção contém classes comuns que não são específicas ao OLAP ou à mineração de dados e que são úteis para administrar ou gerenciar objetos em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Essas classes abordam recursos como procedimentos armazenados, rastreamento, exceções e backup e restauração.  
  
 Este tópico contém as seguintes seções:  
  
-   [Objetos de assembly](#Assembly)  
  
-   [Métodos de backup e restauração](#Backup)  
  
-   [Objetos de rastreamento](#Traces)  
  
-   [Classe CaptureLog e atributo CaptureXML](#CaptureLog)  
  
-   [Classe de exceção AMOException](#AMO)  
  
 A ilustração a seguir mostra o relacionamento das classes explicadas neste tópico.  
  
 ![Outras Classes no AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-otherclasses.gif "outras Classes no AMO")  
  
##  <a name="Assembly"></a>Objetos de assembly  
 Um objeto <xref:Microsoft.AnalysisServices.Assembly> é criado ao ser adicionado à coleção de assemblies do servidor e pela atualização do objeto <xref:Microsoft.AnalysisServices.Assembly> para o servidor por meio do método Update.  
  
 Para remover um <xref:Microsoft.AnalysisServices.Assembly> do objeto, ele terá de ser descartado por meio do método Drop do <xref:Microsoft.AnalysisServices.Assembly> objeto. Remover um objeto <xref:Microsoft.AnalysisServices.Assembly> da coleção de assemblies do banco de dados não descartará o assembly, só impedirá que você o veja em seu aplicativo até a próxima vez em que ele for executado.  
  
 Para obter mais informações sobre os métodos e propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Assembly> em <xref:Microsoft.AnalysisServices> .  
  
> [!IMPORTANT]  
>  Os assemblies COM podem representar um risco à segurança. Devido a esse risco e outras considerações, os assemblies COM foram preteridos no [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]. Talvez não haja suporte para assemblies COM em versões futuras.  
  
##  <a name="Backup"></a>Métodos de backup e restauração  
 Backup e Restore são métodos que podem ser usados na criação de cópias de um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e na recuperação do banco de dados usando a cópia. O método Backup pertence ao objeto <xref:Microsoft.AnalysisServices.Database> e o método Restore pertence ao objeto <xref:Microsoft.AnalysisServices.Server>.  
  
 Somente os administradores de servidor e de banco de dados podem executar um backup de um banco de dados. Somente os administradores de servidor podem restaurar um banco de dados em um servidor diferente de onde foi feito o backup. Os administradores de banco de dados só poderão restaurar um banco de dados substituindo o banco de dados existente se forem proprietários do banco de dados que será substituído. Depois de uma restauração, o administrador de banco de dados poderá perder acesso ao banco de dados restaurado se ele for restaurado com suas definições de segurança originais.  
  
 Os arquivos de backup de banco de dados devem ter extensões .abf.  
  
### <a name="backup-method"></a>Método Backup  
 Para fazer backup de um banco de dados, use o método Backup do objeto de banco de dados com o nome do arquivo de backup como parâmetro.  
  
##### <a name="default-values"></a>Valores padrão:  
 AllowOverwrite =**false**  
  
 BackupRemotePartitions =**false**  
  
 Segurança =**CopyAll**  
  
 ApplyCompression =**true**  
  
### <a name="restore-method"></a>Método Restore  
 Para restaurar um banco de dados para um servidor, use o método Restore do servidor com o arquivo de backup como parâmetro.  
  
##### <a name="default-values"></a>Valores padrão:  
 AllowOverwrite =**false**  
  
 DataSourceType =**remoto**  
  
 Segurança =**CopyAll**  
  
##### <a name="restrictions"></a>Restrictions  
  
1.  Uma partição local não pode ser restaurada como partição remota.  
  
2.  Uma partição remota não pode ser restaurada como partição local, mas uma partição remota pode ser restaurada em um servidor diferente de onde foi feito seu backup.  
  
### <a name="common-parameters-and-properties-for-backup-and-restore-methods"></a>Parâmetros comuns e propriedades para os métodos Backup e Restore  
  
-   **Arquivo** é o nome do arquivo de backup (nome UNC) para/do.  
  
-   **Local** Especifica informações de backup específicas do servidor, como **BackupFile**. Isso permite que você especifique um arquivo de backup separado para um banco de dados remoto.  
  
-   **DatasourceID** Especifica a ID do banco de dados subordinado em um servidor remoto.  
  
-   **ConnectionString** permite que você ajuste a fonte de dados remoto, no caso do servidor remoto foi alterada. DatasourceID sempre deve ser especificado quando ConnectionString estiver presente.  
  
-   **Pasta** permite o remapeamento das pastas para partições no disco rígido local  
  
-   **Original** é a pasta original para partições locais.  
  
-   **Novo** é o novo local para o local das partições que costumavam residir na pasta antiga 'Original' correspondente.  
  
-   **Senha**, caso não esteja em branco, especifica que o servidor criptografará o arquivo de backup.  
  
##  <a name="Traces"></a>Objetos de rastreamento  
 O rastreamento é uma estrutura usada por monitorar, reproduzir novamente e gerenciar uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Um aplicativo cliente, como [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)], assina um rastreamento e o servidor retorna eventos de rastreamento como especificado na definição de rastreamento.  
  
 Cada evento é descrito por uma classe de evento. O tipo de classe de evento descreve o tipo de evento gerado. Em uma classe de evento, as subclasses descrevem um nível mais refinado de categorização. Cada evento é descrito por um número de colunas. As colunas que descrevem um evento de rastreamento são consistentes para todos os eventos e são compatíveis com a estrutura de rastreamento do SQL. As informações registradas em cada coluna podem variar dependendo da classe de evento; ou seja, um conjunto predefinido de colunas é definido para cada rastreamento, mas o significado da coluna pode variar dependendo da classe de evento. Por exemplo, a coluna TextData é usada para registrar a ASSL original para todos os eventos de instrução.  
  
 Uma definição de rastreamento pode incluir uma ou mais classes de evento a serem rastreadas simultaneamente. Para cada classe de evento, podem ser adicionadas uma ou mais colunas de dados à definição de rastreamento, mas nem todas as colunas de rastreamento devem ser usadas. O administrador de banco de dados pode decidir quais das colunas disponíveis serão incluídas em um rastreamento. Além disso, as classes de evento podem ser rastreadas seletivamente com base em critérios de filtragem em qualquer coluna no rastreamento.  
  
 Os rastreamentos podem ser iniciados e excluídos. Vários rastreamentos podem ser executados a qualquer momento. Os eventos de rastreamento podem ser capturados ao vivo ou direcionados a um arquivo para análise posterior ou para nova reprodução. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] é a ferramenta usada para analisar e para reproduzir novamente os eventos de rastreamento do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Várias conexões são permitidas para receber eventos do mesmo rastreamento.  
  
 Os rastreamentos podem ser divididos em dois grupos: rastreamentos de servidor e rastreamentos de sessão. Os rastreamentos de servidor informam todos os eventos do servidor; os rastreamentos de sessão só informam eventos da sessão atual.  
  
 Os rastreamentos, a partir da coleção de rastreamentos do servidor, são definidos da seguinte forma:  
  
1.  Crie um objeto <xref:Microsoft.AnalysisServices.Trace> e preencha seus dados básicos, incluindo a ID de rastreamento, o nome, o nome do arquivo de log, acrescentar|substituir e outros.  
  
2.  Adicione eventos a serem monitorados à coleção Events do objeto de rastreamento. Para cada evento, serão adicionadas colunas de dados.  
  
3.  Defina filtros para excluir linhas de dados desnecessárias adicionando-os à coleção de filtros.  
  
4.  Inicie o rastreamento; a criação do rastreamento não inicia a coleta de dados.  
  
5.  Pare o rastreamento.  
  
6.  Examine o arquivo de rastreamento com [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)].  
  
 Os rastreamentos, a partir do objeto de sessão, são obtidos da seguinte forma:  
  
1.  Defina funções para manipular os eventos de rastreamento gerados em seu aplicativo por SessionTrace. Eventos possíveis são OnEvent e Stopped.  
  
2.  Adicione as funções definidas por você ao manipulador de eventos.  
  
3.  Inicie o rastreamento de sessão.  
  
4.  Faça o seu processo e deixe que os seus manipuladores de função capturem os eventos.  
  
5.  Pare o rastreamento de sessão.  
  
6.  Prossiga com o seu aplicativo.  
  
##  <a name="CaptureLog"></a>Classe CaptureLog e atributo CaptureXML  
 Todas as ações a serem executadas pelo AMO são enviadas para o servidor como mensagens XMLA. O AMO oferece os meios para a captura de todas essas mensagens sem os cabeçalhos SOAP. Para obter mais informações, consulte [apresentando as Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md). CaptureLog é o mecanismo do AMO para a geração de scripts para objetos e operações; os objetos e as operações serão incluídos em scripts no XMLA.  
  
 Para iniciar a captura do XML, a propriedade do objeto de servidor CaptureXML precisa ser definido como **true**. Em seguida, todas as ações que precisam ser enviadas ao servidor começarão a ser capturadas na classe CaptureLog, sem serem enviadas ao servidor. CaptureLog é considerada como classe porque possui um método, Clear, usado para limpar o log de captura.  
  
 Para ler o log, obtenha a a coleção de cadeias de caracteres e inicie a iteração pelas cadeias de caracteres. Além disso, você pode concatenar todos os logs em uma cadeia de caracteres usando o método de objeto de servidor ConcatenateCaptureLog. ConcatenateCaptureLog possui três parâmetros, dois deles obrigatórios. Os parâmetros necessários são *transacional*, do tipo booliano, e *paralela*, do tipo booliano. Se *transacional* é definido como **true**, ele indica que o arquivo em lotes XML será criado como uma única transação em vez de cada comando ser tratado como uma transação separada. Se *paralela* é definido como **true**, ele indica que todos os comandos no arquivo de lote serão registrados para a execução simultânea em vez de sequencialmente como foram registrados.  
  
##  <a name="AMO"></a>Classe de exceção AMOException  
 Você pode usar a classe de exceção AMOException para capturar facilmente as exceções em seu lançadas em seu aplicativo pelo AMO.  
  
 O AMO lançará exceções quando problemas diferentes forem encontrados. A tabela a seguir lista o tipo de exceções manipuladas pelo AMO. As exceções são derivadas da classe de <xref:Microsoft.AnalysisServices.AmoException>.  
  
|Exceção|Origem|Description|  
|---------------|------------|-----------------|  
|<xref:Microsoft.AnalysisServices.AmoException>|Classe base|O aplicativo recebe esta exceção quando um objeto pai exigido está ausente ou quando um item solicitado não é localizado em uma coleção.|  
|<xref:Microsoft.AnalysisServices.OutOfSyncException>|Derivada de AMOException|O aplicativo recebe esta exceção quando o AMO não está sincronizado com o mecanismo e o mecanismo retorna uma referência de objeto que o AMO não conhece.|  
|<xref:Microsoft.AnalysisServices.OperationException>|Derivada de AMOException|Esta é uma exceção importante recebida por aplicativos com frequência. Esta exceção contém os detalhes de um erro vindo do servidor, provavelmente por causa de uma operação malsucedida do AMO, como Update ou Process ou Drop.|  
|<xref:Microsoft.AnalysisServices.ResponseFormatException>|Derivada de AMOException|Esta exceção ocorre quando o mecanismo retorna uma mensagem em um formato que o AMO não compreende.|  
|<xref:Microsoft.AnalysisServices.ConnectionException>|Derivada de AMOException|Esta exceção ocorre quando uma conexão não pode ser estabelecida (com Server.Connect) ou quando a conexão é perdida durante a comunicação do AMO com o mecanismo (por exemplo, durante um Update ou Process ou Drop).|  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.AnalysisServices>   
 [Introdução às Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
