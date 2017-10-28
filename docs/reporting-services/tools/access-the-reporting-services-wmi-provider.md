---
title: "Provedor WMI de serviços de acesso a relatórios | Microsoft Docs"
ms.custom: 
ms.date: 11/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- Reporting Services WMI Provider
apilocation:
- reportingservices.mof
helpviewer_keywords:
- WMI provider [Reporting Services]
- programming [Reporting Services]
ms.assetid: 22cfbeb8-4ea3-4182-8f54-3341c771e87b
caps.latest.revision: 57
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2aa02df2ee2953c1a3f4b02236cd5203ff08cdc3
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="access-the-reporting-services-wmi-provider"></a>Acessar o provedor WMI do Reporting Services
  O provedor WMI do Reporting Services expõe duas classes WMI para administração de instâncias de servidor de relatório do modo nativo através de scripts:  
  
> [!IMPORTANT]  
>  A partir da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , o provedor WMI tem suporte apenas para servidores de relatórios no modo nativo. Servidores de relatórios no modo do SharePoint podem ser gerenciados com páginas Administração Central do SharePoint e scripts do PowerShell.  
  
|Classe|Namespace|Description|  
|-----------|---------------|-----------------|  
|MSReportServer_Instance|root\Microsoft\SqlServer\ReportServer\RS_*\<EncodedInstanceName >*\v13|Fornece as informações básicas exigidas para um cliente se conectar a um servidor de relatório instalado.|  
|MSReportServer_ConfigurationSetting|root\Microsoft\SqlServer\ReportServer\RS_*\<EncodedInstanceName >*\v13\Admin|Representa os parâmetros de instalação e de tempo de execução de uma instância do servidor de relatório. Esses parâmetros são armazenados no arquivo de configuração para o servidor de relatório.<br /><br /> **\*\* Importante \*\*** Esta classe é acessível apenas com privilégios administrativos.|  
  
 Uma instância de cada uma das classes anteriores é criada para cada instância de servidor de relatório. Você pode usar qualquer ferramenta Microsoft ou de terceiros para acessar os objetos WMI expostos pelo servidor de relatório, inclusive interfaces de programação de WMI expostas pelo próprio .NET Framework. Este tópico descreve como acessar e usar as instâncias de classe WMI com o comando do PowerShell [Get-WmiObject](http://technet.microsoft.com/library/dd315295.aspx).  
  
## <a name="determine-the-instance-name-in-the-namespace-string"></a>Determine o nome de instância na cadeia de caracteres de namespace  
 O nome de instância no caminho de namespace para as classes WMI do Reporting Services é uma codificação dos nomes de instância que você especifica ao instalar as instâncias nomeadas do Reporting Services. Isto é, caracteres especiais são codificados nos nomes de instância. Por exemplo, um sublinhado (_) é codificado como "_5f"; assim, um nome de instância de "My_Instance" é codificado como "My_5fInstance" no caminho de namespace do WMI.  
  
 Para listar os nomes de instância codificados de suas instâncias de servidor de relatório no caminho de namespace do WMI, use o seguinte comando do PowerShell:  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace root\Microsoft\SqlServer\ReportServer  –class __Namespace –ComputerName hostname | select Name  
```  
  
## <a name="access-the-wmi-classes-using-powershell"></a>Acesse as classes WMI usando o PowerShell  
 Para acessar as classes WMI, execute o seguinte comando:  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace <namespacename> –class <classname> –ComputerName <hostname>  
```  
  
 Por exemplo, para acessar a classe MSReportServer_ConfigurationSetting na instância de servidor de relatório padrão do myrshost de host, execute o comando a seguir. A instância de servidor de relatório padrão deve ser instalada no myrshost para este comando ter êxito.  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERER\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost  
```  
  
 Esta sintaxe de comando gera todos os nomes e valores de propriedade de classe. Observe que todas as instâncias da classe MSReportServer_ConfigurationSetting são retornadas, embora você esteja acessando a classe no namespace da instância de servidor de relatório padrão (RS_MSSQLSERVER). Por exemplo, se myrshost for instalado com a instância de servidor de relatório padrão e uma instância de servidor de relatório nomeada chamada SHAREPOINT, este comando retornará dois objetos WMI e gerará os nomes e valores de propriedade para ambas as instâncias de servidor de relatório.  
  
 Para retornar uma instância de classe específica quando várias instâncias são retornadas, use o parâmetro –Filter para filtrar os resultados com base em propriedades com valores exclusivos como InstanceName. Por exemplo, para retornar apenas o objeto WMI para a instância de servidor de relatório padrão, use o seguinte comando:  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='MSSQLSERVER'"  
```  
  
## <a name="query-the-available-methods-and-properties"></a>Consultar os métodos e as propriedades disponíveis  
 Para consultar que métodos e propriedades estão disponíveis em uma das classes WMI do Reporting Services, canalize os resultados de Get-WmiObject para o comando Get-Member. Por exemplo:  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost | Get-Member  
```  
  
## <a name="use-a-wmi-method-or-property"></a>Usar um método ou propriedade WMI  
 Quando você tiver os objetos WMI para as classes do Reporting Services e conhecer os métodos e as propriedades disponíveis, poderá usar esses métodos e propriedades. Por exemplo, se você tiver uma instância de servidor de relatório nomeada no modo Integrado do SharePoint chamado SHAREPOINT, use a seguinte sequência de comandos para recuperar a URL para o site de Administração Central do SharePoint:  
  
```  
PS C:\windows\system32> $rsconfig = Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='SHAREPOINT'"  
PS C:\windows\system32> $rsconfig.GetAdminSiteUrl()  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Biblioteca do provedor WMI do Reporting Services &#40;SSRS&#41;](../../reporting-services/wmi-provider-library-reference/reporting-services-wmi-provider-library-reference-ssrs.md)   
 [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  

