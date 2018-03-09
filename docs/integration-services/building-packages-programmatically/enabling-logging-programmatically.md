---
title: Habilitar o registro em log programaticamente | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- Integration Services packages, logs
- SSIS logging
- log providers [Integration Services]
- logs [Integration Services], enabling
- LoggingMode property
- LogProvider object
- packages [Integration Services], logs
ms.assetid: 3222a1ed-83eb-421c-b299-a53b67bba740
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9a3eafea038aa10da1bd21e1ab89c6c3f6fcdbb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="enabling-logging-programmatically"></a>Habilitando o registro em log programaticamente
  O mecanismo de tempo de execução fornece uma coleção de objetos <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> que permitem que informações específicas a eventos sejam capturadas durante a validação e a execução de pacotes. Os objetos <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> estão disponíveis para objetos <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer>, inclusive os objetos <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, <xref:Microsoft.SqlServer.Dts.Runtime.Package>, <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop> e <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>. O registro em log é habilitado em contêineres individuais ou no pacote inteiro.  
  
 Há vários tipos de provedores de log disponíveis para uso por um contêiner. Isso fornece a flexibilidade para criar e armazenar informações de log em diversos formatos. A inscrição de um objeto contêiner no registro em log é um processo de duas etapas: primeiro o registro é habilitado e depois um provedor de log é selecionado. As propriedades <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> do contêiner são usadas para especificar os eventos registrados e selecionar o provedor de log.  
  
## <a name="enabling-logging"></a>Habilitando o registro em log  
 A propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A>, localizada em cada contêiner que pode executar o registro em log, determina se as informações de evento do contêiner são registradas no log de eventos. É atribuído um valor a essa propriedade a partir da estrutura <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode> e ele é herdado por padrão do pai do contêiner. Se o contêiner for um pacote e não tiver pai, a propriedade usará o <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting>, que assume o valor **Disabled** por padrão.  
  
### <a name="selecting-a-log-provider"></a>Selecionando um provedor de log  
 Depois que a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> é definida como **Enabled**, um provedor de logs é adicionado à coleção <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> do contêiner para concluir o processo. A coleção <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> está disponível no objeto <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions> e contém os provedores de log selecionados para o contêiner. O método <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A> é chamado para criar um provedor e adicioná-lo à coleção. O método retorna o provedor de log que foi adicionado à coleção. Cada provedor tem parâmetros de configuração que são exclusivos desse provedor e essas propriedades são definidas através da propriedade <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A>.  
  
 A tabela a seguir lista os provedores de log disponíveis, sua descrição e as informações sobre <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A>.  
  
|Provedor|Description|Propriedade ConfigString|  
|--------------|-----------------|---------------------------|  
|SQL Server Profiler|Gera rastreamentos do SQL que podem ser capturados e exibidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler. A extensão de nome de arquivo padrão deste provedor é .trc.|Nenhuma configuração é necessária.|  
|SQL Server|Escreve entradas de log de evento na tabela **sysssislog** em qualquer banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|O provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exige a especificação da conexão ao banco de dados e também o nome do banco de dados de destino.|  
|Arquivo de texto|Grava entradas do log de eventos em arquivos de texto ASCII em formato CSV (valores separados por vírgula). A extensão de nome de arquivo padrão deste provedor é .log.|O nome do gerenciador de conexões de um arquivo.|  
|Log de eventos do Windows|Conecta-se ao log de eventos padrão do Windows no computador local no log do Aplicativo.|Nenhuma configuração é necessária.|  
|Arquivo XML|Grava entradas do log de eventos no arquivo em formato XML. A extensão padrão do nome de arquivo desse provedor é .xml.|O nome do gerenciador de conexões de um arquivo.|  
  
 Os eventos são incluídos no log de eventos ou excluídos dele configurando as propriedades **EventFilterKind** e **EventFilter** do contêiner. A estrutura **EventFilterKind** contém dois valores, **ExclusionFilter** e **InclusionFilter**, que indicam se os eventos que são adicionados ao **EventFilter** estão incluídos no log de eventos. A propriedade **EventFilter** recebe uma matriz de cadeia de caracteres que contém os nomes dos eventos que são o assunto da filtragem.  
  
 O código a seguir habilita o registro em um pacote, adiciona o provedor de log dos arquivos de Texto à coleção <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> e especifica uma lista de eventos para incluir na saída de log.  
  
## <a name="sample"></a>Amostra  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      ConnectionManager loggingConnection = p.Connections.Add("FILE");  
      loggingConnection.ConnectionString = @"C:\SSISPackageLog.txt";  
  
      LogProvider provider = p.LogProviders.Add("DTS.LogProviderTextFile.2");  
      provider.ConfigString = loggingConnection.Name;  
      p.LoggingOptions.SelectedLogProviders.Add(provider);  
      p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion;  
      p.LoggingOptions.EventFilter = new String[] { "OnPreExecute",   
         "OnPostExecute", "OnError", "OnWarning", "OnInformation" };  
      p.LoggingMode = DTSLoggingMode.Enabled;  
  
      // Add tasks and other objects to the package.  
  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
  
    Dim loggingConnection As ConnectionManager = p.Connections.Add("FILE")  
    loggingConnection.ConnectionString = "C:\SSISPackageLog.txt"  
  
    Dim provider As LogProvider = p.LogProviders.Add("DTS.LogProviderTextFile.2")  
    provider.ConfigString = loggingConnection.Name  
    p.LoggingOptions.SelectedLogProviders.Add(provider)  
    p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion  
    p.LoggingOptions.EventFilter = New String() {"OnPreExecute", _  
       "OnPostExecute", "OnError", "OnWarning", "OnInformation"}  
    p.LoggingMode = DTSLoggingMode.Enabled  
  
    ' Add tasks and other objects to the package.  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Registro em Log do Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
