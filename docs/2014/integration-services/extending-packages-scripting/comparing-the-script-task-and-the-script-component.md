---
title: Comparar a tarefa Script e o componente Script | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], comparing to Script component
- Script component [Integration Services], comparing to Script task
ms.assetid: 4b73753a-4239-491b-b7a6-abc63ba83d2d
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b38d47585c1fc5b35384b882cdf6920c10dbc07
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302286"
---
# <a name="comparing-the-script-task-and-the-script-component"></a>Comparando a tarefa Script e o componente Script
  A tarefa Script, disponível na janela Fluxo de Controle do designer do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o componente Script, disponível na janela Fluxo de Dados, têm finalidades bem distintas em um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A tarefa é uma ferramenta de fluxo de controle de uso general, enquanto o componente serve como uma origem, transformação ou destino no fluxo de dados. Apesar das diferentes finalidades, a tarefa Script e o componente Script possuem algumas semelhanças nas ferramentas de codificação que eles usam e nos objetos do pacote que são disponibilizados para o desenvolvedor. A compreensão dessas semelhanças e diferenças pode ajudá-lo a usar a tarefa e o componente de forma mais eficaz.  
  
## <a name="similarities-between-the-script-task-and-the-script-component"></a>Semelhanças entre a tarefa Script e o componente Script  
 A tarefa Script e o componente Script compartilham os recursos em comum a seguir.  
  
|Recurso|Description|  
|-------------|-----------------|  
|Dois modos de design-tempo|Na tarefa e no componente, você começa especificando propriedades no editor e, depois, alterna para o ambiente de desenvolvimento para escrever código.|  
|VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications)|A tarefa e o componente usam o mesmo VSTA IDE e dão suporte ao código escrito em [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.|  
|Scripts pré-compilados|A partir do [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], todos os scripts são pré-compilados. Em versões anteriores, você podia especificar se os scripts foram pré-compilados.<br /><br /> O script é pré-compilado em código binário, permitindo maior rapidez na execução, mas isso resulta no aumento do tamanho do pacote.|  
|Depuração|A tarefa e o componente dão suporte a pontos de interrupção e passa pelo código durante a depuração no ambiente de design. Para obter mais informações, consulte [codificando e depurando a tarefa Script](../control-flow/script-task.md) e [codificando e depurando o componente Script] (... / extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.|  
  
## <a name="differences-between-the-script-task-and-the-script-component"></a>Diferenças entre a tarefa Script e o componente Script  
 Convém destacar as diferenças a seguir entre a tarefa Script e o componente Script.  
  
|Recurso|Tarefa Script|Componente Script|  
|-------------|-----------------|----------------------|  
|Fluxo de controle / Fluxo de dados|A tarefa Script é configurada na guia Fluxo de Controle do designer e é executada fora do fluxo de dados do pacote.|O componente Script é configurado na página Fluxo de Dados do designer e representa uma origem, transformação ou destino na tarefa Fluxo de Dados.|  
|Finalidade|Uma tarefa Script pode realizar praticamente qualquer tarefa para fins gerais.|Especifique se você deseja criar uma origem, transformação ou destino com o componente Script.|  
|Execução|Uma tarefa Script executa código personalizado em algum ponto no fluxo de trabalho do pacote. A menos que você coloque isso em um contêiner de loop ou em um manipulador de eventos, ele só será executado uma vez.|Um componente Script também é executado uma vez, mas costuma executar sua rotina de processamento principal uma vez para cada linha de dados do fluxo de dados.|  
|Editor|O **Editor da Tarefa Script** contém três páginas: **Geral**, **Script** e **Expressões**. Somente o `ReadOnlyVariables` e `ReadWriteVariables`, e **ScriptLanguage** propriedades afetam diretamente o código que você pode escrever.|O **Editor de Transformação Scripts** contém no máximo quatro páginas: **Colunas de Entrada**, **Entradas e Saídas**, **Script** e **Gerenciadores de Conexões**. Os metadados e propriedades que você configura em cada uma dessas páginas determinam os membros das classes base que são gerenciadas automaticamente para seu uso na codificação.|  
|Interação com o pacote|No código escrito para uma tarefa Script, você usa a propriedade `Dts` para acessar outros recursos do pacote. A propriedade `Dts` é um membro da classe `ScriptMain`.|No código do componente Script, você usa propriedades de acessador tipado para acessar determinados recursos do pacote, tais como variáveis e gerenciadores de conexões.<br /><br /> O método `PreExecute` só pode acessar variáveis somente leitura. O método `PostExecute` pode acessar variáveis somente leitura e de leitura/gravação.<br /><br /> Para obter mais informações sobre esses métodos, consulte [codificando e depurando o componente Script] (... / extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.|  
|Usando variáveis|A tarefa Script usa a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> do objeto `Dts` para acessar variáveis que estão disponíveis através das propriedades <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> da tarefa. Por exemplo:<br /><br /> **[VB]**<br /><br /> `Dim myVar as String myVar = Dts.Variables(“MyStringVariable”).Value.ToString`<br /><br /> <br /><br /> **[C#]**<br /><br /> `string myVar; myVar = Dts.Variables["MyStringVariable"].Value.ToString();`|O componente Script usa propriedades do acessador tipado da classe base gerada automaticamente, criada a partir das propriedades <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> do componente. Por exemplo:<br /><br /> **[VB]**<br /><br /> `Dim myVar as String myVar = Me.Variables.MyStringVariable`<br /><br /> <br /><br /> **[C#]**<br /><br /> `string myVar; myVar = this.Variables.MyStringVariable;`|  
|Usando conexões|A tarefa Script usa a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> do objeto `Dts` para acessar gerenciadores de conexões definidos no pacote. Por exemplo:<br /><br /> **[VB]**<br /><br /> `Dim myFlatFileConnection As String myFlatFileConnection = _     DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _     String)`<br /><br /> <br /><br /> **[C#]**<br /><br /> `string myFlatFileConnection; myFlatFileConnection = (Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);`|O componente Script usa propriedades do acessador tipado da classe base gerada automaticamente, criada a partir da lista de gerenciadores de conexões digitada pelo usuário na página Gerenciadores de Conexões do editor. Por exemplo:<br /><br /> **[VB]**<br /><br /> `Dim connMgr As IDTSConnectionManager100 connMgr = Me.Connections.MyADONETConnection`<br /><br /> <br /><br /> **[C#]**<br /><br /> `IDTSConnectionManager100 connMgr; connMgr = this.Connections.MyADONETConnection;`|  
|Gerando eventos|A tarefa Script usa a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> do objeto `Dts` para gerar eventos. Por exemplo:<br /><br /> **[VB]**<br /><br /> `Dts.Events.FireError(0, "Event Snippet", _     ex.Message & ControlChars.CrLf & ex.StackTrace, _     "", 0)`<br /><br /> <br /><br /> **[C#]**<br /><br /> `Dts.Events.FireError(0, "Event Snippet", ex.Message + "\r" + ex.StackTrace, "", 0);`|O componente Script gera erros, avisos e mensagens informativas através dos métodos da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> retornados pela propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>. Por exemplo:<br /><br /> **[VB]**<br /><br /> `Dim myMetadata as IDTSComponentMetaData100 myMetaData = Me.ComponentMetaData myMetaData.FireError(...)`|  
|Log|A tarefa Script usa o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> método da `Dts` habilitado de objeto para registrar informações para provedores de log. Por exemplo:<br /><br /> **[VB]**<br /><br /> `Dim bt(0) As Byte Dts.Log("Test Log Event", _     0, _     bt)`<br /><br /> <br /><br /> **[C#]**<br /><br /> `byte[] bt = new byte[0]; Dts.Log("Test Log Event", 0, bt);`|O componente Script usa o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> da classe base gerada automaticamente para registrar informações para provedores de log habilitados. Por exemplo:<br /><br /> **[VB]**<br /><br /> `Dim bt(0) As Byte`<br /><br /> `Me.Log("Test Log Event", _`<br /><br /> `0, _`<br /><br /> `bt)`<br /><br /> <br /><br /> **[C#]**<br /><br /> `byte[] bt = new byte[0]; this.Log("Test Log Event", 0, bt);`|  
|Retornando resultados|A tarefa Script usa o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> propriedade e opcional <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> propriedade do `Dts` objeto notificar o tempo de execução de seus resultados.|O componente Script é executado como parte da tarefa Fluxo de Dados e não relata resultados através de uma dessas propriedades.|  
  
## <a name="see-also"></a>Consulte também  
 [Estender o pacote com a tarefa Script](task/extending-the-package-with-the-script-task.md)   
 [Estender o fluxo de dados com o componente Script](data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
 [Consumir serviços Web no SSIS usando Scripts (resposta da curadoria)](http://go.microsoft.com/fwlink/?LinkId=321996)  
  
  
