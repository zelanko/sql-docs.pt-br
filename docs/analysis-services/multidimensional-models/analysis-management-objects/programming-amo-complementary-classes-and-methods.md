---
title: "As Classes AMO complementares e métodos de programação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- restores [AMO]
- assemblies [AMO]
- AMO, backup and restore
- capture logs [AMO]
- programming [AMO]
- Analysis Management Objects, backup and restore
- traces [AMO]
- backups [AMO]
ms.assetid: 14aed554-d2e2-49e5-9c72-26660759bce2
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b851de387d82c563e1e63e119c3a42904eacef8b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="programming-amo-complementary-classes-and-methods"></a>Programando classes e métodos AMO complementares
  Este tópico contém as seguintes seções:  
  
-   [Classe de assembly](#Assembly)  
  
-   [Backup e restauração](#BU)  
  
-   [Classe Trace](#TRC)  
  
-   [Classe CaptureLog e atributo CaptureXML](#CL)  
  
##  <a name="Assembly"></a>Classe de assembly  
 Assemblies permitem que os usuários estender a funcionalidade de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] adicionando novos procedimentos armazenados ou funções MDX (Multidimensional Expressions). Para obter mais informações, consulte [métodos e as outras Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md).  
  
 A adição e o descarte de assemblies são simples e podem ser executados de forma online. É preciso ser administrador de banco de dados para adicionar um assembly ao banco de dados ou um administrador de servidor para adicionar o assembly ao objeto de servidor.  
  
 O exemplo a seguir adiciona um assembly ao banco de dados fornecido e atribui a conta de serviço para a execução do assembly. Se o assembly existir no banco de dados, será descartado antes da tentativa de adição.  
  
```  
static public void CreateStoredProcedures(Database db)  
{  
    ClrAssembly clrAssembly;  
  
    // Verify That assembly exist in database and drop it  
    if (db.Assemblies.ContainsName("StoredProcedures"))  
    {  
        clrAssembly = db.Assemblies.FindByName("StoredProcedures");  
        clrAssembly.Drop();  
    }  
  
    // Create the CLR assembly  
    clrAssembly = db.Assemblies.Add("StoredProcedures");  
    clrAssembly.ImpersonationInfo = new ImpersonationInfo(  
        ImpersonationMode.ImpersonateServiceAccount);  
    clrAssembly.PermissionSet = PermissionSet.Unrestricted;  
  
    // Load the assembly files  
    clrAssembly.LoadFiles(Environment.CurrentDirectory  
        + @"\StoredProcedures2.dll", false);  
  
    clrAssembly.Update();  
}  
  
```  
  
##  <a name="BU"></a>Métodos de backup e restauração  
 Os métodos Backup e Restore permitem que os administradores façam backup de bancos de dados e os restaurem.  
  
 O exemplo a seguir cria backups para todos os bancos de dados do servidor especificado. Se um arquivo de backup já existir, será substituído. Os arquivos de backup são salvos na pasta BackUp da pasta Data do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
```  
static public void BackUpAllDatabases(Server svr)  
{  
    string fileName;  
    if ((svr != null) && ( svr.Connected))  
        foreach (Database db in svr.Databases)  
        {  
            fileName = db.Name + "_" + ((Int64)(DateTime.Today.Year * 10000 + DateTime.Today.Month * 100 + DateTime.Today.Day)).ToString()+ ".abf";  
            db.Backup(fileName, true);  
        }  
}  
```  
  
 O exemplo a seguir restaura o backup "Adventure Works" do exemplo anterior. Se o banco de dados "My Adventure WorksDW" já existir, será substituído.  
  
```  
static public void RestoreAdventureWorks(Server svr)  
{  
    svr.Restore("Adventure Works DW_20051025.abf", "My Adventure WorksDW", true);  
}  
```  
  
##  <a name="TRC"></a>Classe Trace  
 O monitoramento da atividade de servidor exige o uso de dois tipos de rastreamentos: Rastreamentos de Sessão e Rastreamentos de Servidor. Rastrear o servidor pode dizer a você como está a execução da sua tarefa atual no servidor (Rastreamentos de Sessão) ou os rastreamentos poderão dizer como está a atividade geral no servidor sem que você tenha de se conectar ao servidor (Rastreamentos de Servidor).  
  
 Durante o rastreamento da atividade atual (Rastreamentos de Sessão), o servidor envia notificações ao aplicativo atual sobre os eventos que estão ocorrendo no servidor e que foram causados pelo aplicativo. Os eventos são capturados por meio de manipuladores de eventos do aplicativo atual. Primeiro você atribui as rotinas de manipulação de eventos ao objeto <xref:Microsoft.AnalysisServices.SessionTrace> e então inicia o Rastreamento de Sessão.  
  
 O exemplo a seguir mostra como configurar um Rastreamento de Sessão para rastrear as atividades atuais. As rotinas do manipulador de eventos estão localizadas no final do exemplo e produzirão todas as informações de rastreamento para o objeto System.Console. Para gerar eventos de rastreamento, o cubo de exemplo "Adventure Works" será completamente processado depois do início do rastreamento.  
  
```  
static public void TestSessionTraces(Server svr)  
{  
    // Start the default trace  
  
    svr.SessionTrace.OnEvent  
        += new TraceEventHandler(DefaultTrace_OnEvent);  
    svr.SessionTrace.Stopped  
        += new TraceStoppedEventHandler(DefaultTrace_Stopped);  
    svr.SessionTrace.Start();  
  
    // Process the databases  
    // The trace handlers will output all progress notifications   
    // to the console  
    Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    cube.Process(ProcessType.ProcessFull);  
  
    // Stop the default trace  
    svr.SessionTrace.Stop();  
  
}  
static public void DefaultTrace_OnEvent(object sender, TraceEventArgs e)  
{  
    Console.WriteLine("{0}", e.TextData);  
}  
  
static public void DefaultTrace_Stopped(ITrace sender, TraceStoppedEventArgs e)  
{  
    switch (e.StopCause)  
    {  
        case TraceStopCause.StoppedByUser:  
        case TraceStopCause.Finished:  
            Console.WriteLine("Processing completed successfully");  
            break;  
  
        case TraceStopCause.StoppedByException:  
            Console.WriteLine("Processing failed: {0}",  
                e.Exception.Message);  
            break;  
    }  
}  
```  
  
 Os rastreamentos de servidor podem ser configurados para registrar tudo em um arquivo de rastreamento e podem ser reiniciados automaticamente quando o serviço reiniciar.  
  
 Para definir um rastreamento de servidor, primeiro é necessário definir que eventos do servidor serão monitorados e que dados do evento serão salvos no arquivo de rastreamento. Para cada evento, você deve definir as colunas de dados a serem salvadas no arquivo de rastreamento.  
  
 A criação de um rastreamento de servidor exige quatro etapas:  
  
1.  Crie o objeto de rastreamento de servidor e preencha os atributos comuns básicos.  
  
     LogFileSize define o tamanho máximo do arquivo de rastreamento e é definido em MegaBytes; LogFileRollOver permite que o arquivo de log comece em um arquivo diferente caso o limite de LogFileSize seja atingido; quando habilitado, o nome do arquivo será anexado a um número de sequência; AutoRestart permite que o rastreamento comece novamente se o Serviço for reiniciado.  
  
2.  Crie os eventos e as colunas de dados correspondentes.  
  
3.  Inicie e pare o rastreamento quando necessário.  
  
     Mesmo depois que o rastreamento foi interrompido, o rastreamento existe no servidor e deve ser iniciado novamente se o rastreamento foi definido como AutoRestart =**true**.  
  
4.  Descarte o rastreamento quando já não for necessário.  
  
 No exemplo seguinte, se o rastreamento já existir, será descartado e então recriado. Os arquivos de rastreamento são salvos na pasta Log das pastas de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
```  
static public void TestServerTraces(Server svr)  
{  
    Trace trc;  
    TraceEvent te;  
  
        trc = svr.Traces.FindByName("TestServerTraces");  
        if (trc != null)  
            trc.Drop();  
        trc = svr.Traces.Add("TestServerTraces", "TestServerTraces");  
        trc.LogFileName = ("TestServerTraces_" +((Int64)(DateTime.Now.Year * 10000 + DateTime.Now.Month * 100 + DateTime.Now.Day)).ToString() + "_" +  
                ((Int64)(DateTime.Now.Hour * 10000 + DateTime.Now.Minute * 100 + DateTime.Now.Second)).ToString() + ".trc");  
        trc.LogFileSize = 100;  
        trc.LogFileRollover = true;  
        trc.AutoRestart = false;  
  
        #region Define Events to trace & data columns per event  
        te = trc.Events.Add(TraceEventClass.ProgressReportBegin);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportCurrent);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportEnd);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.EndTime);  
        te.Columns.Add(TraceColumn.Success);  
        te.Columns.Add(TraceColumn.Error);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
        #endregion  
  
        trc.Update();  
        trc.Start();  
  
        #region Process the Adventure Works Cube  
        // The trace settings will output all progress notifications   
        // to the trace file  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        Cube cube = db.Cubes.FindByName("Adventure Works");  
        cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        trc.Stop();  
        trc.Drop();  
  
}  
```  
  
##  <a name="CL"></a>Atributos CaptureLog e CaptureXml  
 O atributo CaptureLog permite que você crie arquivos em lotes XMLA a partir das suas operações AMO. CaptureLog permite que você gere scripts de objetos de servidor como bancos de dados, cubos, dimensões, estruturas de mineração e outros.  
  
 A criação de um CaptureLog exige as seguintes etapas:  
  
1.  Iniciar a captura do log XMLA definindo o servidor de atributo CaptureXml como **true**.  
  
     Essa opção começará a salvar todas as operações AMO em a uma coleção de cadeias de caracteres em vez de enviá-las ao servidor.  
  
2.  Inicie a atividade AMO como sempre, mas lembre-se de que nenhuma ação será enviada ao servidor. Atividade pode ser qualquer operação, como processamento, criação, exclusão, atualização ou qualquer outra ação executada em um objeto.  
  
3.  Parar a captura do log XMLA redefinido CaptureXml como **false**.  
  
4.  Revise o XMLA capturado, revisando cada uma das cadeias de caracteres na coleção de cadeias de caracteres CaptureLog ou gerando uma cadeia de caracteres completa com o método ConcatenateCaptureLog. ConcatenateCaptureLog permite que você gere o lote XMLA como uma única transação e adicione a opção de processo paralelo ao lote.  
  
 O exemplo a seguir retorna uma cadeia de caracteres com os comandos em lote para a execução de um processo Completo em todas as dimensões e em todos os cubos do banco de dados [Adventure Works DW Multidimensional 2012].  
  
```  
static public string TestCaptureLog(Server svr)  
{  
    String capturedXmla = "";  
    if ((svr != null) && (svr.Connected))  
    {  
        svr.CaptureXml = true;  
  
        #region Actions to be captured to an XMLA file  
        //No action is executed during CaptureXml = true  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        foreach (Dimension dim in db.Dimensions)  
            dim.Process(ProcessType.ProcessFull);  
        foreach (Cube cube in db.Cubes)  
            cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        svr.CaptureXml = false;  
  
        capturedXmla = svr.ConcatenateCaptureLog(true, true);  
  
    }  
  
    return capturedXmla;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Introdução às Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO outras Classes e métodos](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Processar um modelo multidimensional &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
