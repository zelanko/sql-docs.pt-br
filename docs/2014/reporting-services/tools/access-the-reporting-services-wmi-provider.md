---
title: Acessar o provedor WMI do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- Reporting Services WMI Provider
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services]
- programming [Reporting Services]
ms.assetid: 22cfbeb8-4ea3-4182-8f54-3341c771e87b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: efbe03a4aab65f792b352eeb5b6c5130c4c32335
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783213"
---
# <a name="access-the-reporting-services-wmi-provider"></a>Acessar o provedor WMI do Reporting Services
  O provedor WMI do Reporting Services expõe duas classes WMI para administração de instâncias de servidor de relatório do modo nativo através de scripts:  
  
> [!IMPORTANT]  
>  A partir da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , o provedor WMI tem suporte apenas para servidores de relatórios no modo nativo. Servidores de relatórios no modo do SharePoint podem ser gerenciados com páginas Administração Central do SharePoint e scripts do PowerShell.  
  
|Classe|Namespace|Description|  
|-----------|---------------|-----------------|  
|MSReportServer_Instance|root\Microsoft\SqlServer\ReportServer\RS_ *\<EncodedInstanceName >* \v11|Fornece as informações básicas exigidas para um cliente se conectar a um servidor de relatório instalado.|  
|MSReportServer_ConfigurationSetting|root\Microsoft\SqlServer\ReportServer\RS_ *\<EncodedInstanceName >* \v11\Admin|Representa os parâmetros de instalação e de tempo de execução de uma instância do servidor de relatório. Esses parâmetros são armazenados no arquivo de configuração para o servidor de relatório.<br /><br /> **\*\* Importante \*\*** Esta classe é acessível apenas com privilégios administrativos.|  
  
 Uma instância de cada uma das classes anteriores é criada para cada instância de servidor de relatório. Você pode usar qualquer ferramenta Microsoft ou de terceiros para acessar os objetos WMI expostos pelo servidor de relatório, inclusive interfaces de programação de WMI expostas pelo próprio .NET Framework. Este tópico descreve como acessar e usar as instâncias de classe WMI com o comando do PowerShell [Get-WmiObject](https://technet.microsoft.com/library/dd315295.aspx).  
  
## <a name="determine-the-instance-name-in-the-namespace-string"></a>Determine o nome de instância na cadeia de caracteres de namespace  
 O nome de instância no caminho de namespace para as classes WMI do Reporting Services é uma codificação dos nomes de instância que você especifica ao instalar as instâncias nomeadas do Reporting Services. Isto é, caracteres especiais são codificados nos nomes de instância. Por exemplo, um sublinhado (_) é codificado como "_5f"; assim, um nome de instância de "My_Instance" é codificado como "My_5fInstance" no caminho de namespace do WMI.  
  
 Para listar os nomes de instância codificados de suas instâncias de servidor de relatório no caminho de namespace do WMI, use o seguinte comando do PowerShell:  
  
```powershell
Get-WmiObject -Namespace root\Microsoft\SqlServer\ReportServer -Class __Namespace -ComputerName hostname | Select Name  
```  
  
## <a name="access-the-wmi-classes-using-powershell"></a>Acesse as classes WMI usando o PowerShell  
 Para acessar as classes WMI, execute o seguinte comando:  
  
```powershell
Get-WmiObject -Namespace <namespacename> -Class <classname> -ComputerName <hostname>  
```  
  
 Por exemplo, para acessar a classe MSReportServer_ConfigurationSetting na instância de servidor de relatório padrão do myrshost de host, execute o comando a seguir. A instância de servidor de relatório padrão deve ser instalada no myrshost para este comando ter êxito.  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERER\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost  
```  
  
 Esta sintaxe de comando gera todos os nomes e valores de propriedade de classe. Observe que todas as instâncias da classe MSReportServer_ConfigurationSetting são retornadas, embora você esteja acessando a classe no namespace da instância de servidor de relatório padrão (RS_MSSQLSERVER). Por exemplo, se myrshost for instalado com a instância de servidor de relatório padrão e uma instância de servidor de relatório nomeada chamada SHAREPOINT, este comando retornará dois objetos WMI e gerará os nomes e valores de propriedade para ambas as instâncias de servidor de relatório.  
  
 Para retornar uma instância de classe específica quando várias instâncias são retornadas, use o parâmetro -Filter para filtrar os resultados com base em propriedades com valores exclusivos como InstanceName. Por exemplo, para retornar apenas o objeto WMI para a instância de servidor de relatório padrão, use o seguinte comando:  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost -Filter "InstanceName='MSSQLSERVER'"  
```  
  
## <a name="query-the-available-methods-and-properties"></a>Consultar os métodos e as propriedades disponíveis  
 Para consultar que métodos e propriedades estão disponíveis em uma das classes WMI do Reporting Services, canalize os resultados de Get-WmiObject para o comando Get-Member. Por exemplo:  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost | Get-Member  
```  
  
 Para obter a documentação sobre as propriedades e métodos do Reporting Services classes WMI, consulte....  
  
## <a name="use-a-wmi-method-or-property"></a>Usar um método ou propriedade WMI  
 Quando você tiver os objetos WMI para as classes do Reporting Services e conhecer os métodos e as propriedades disponíveis, poderá usar esses métodos e propriedades. Por exemplo, se você tiver uma instância de servidor de relatório nomeada no modo Integrado do SharePoint chamado SHAREPOINT, use a seguinte sequência de comandos para recuperar a URL para o site de Administração Central do SharePoint:  
  
```powershell
$rsconfig = Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost -Filter "InstanceName='SHAREPOINT'"  
$rsconfig.GetAdminSiteUrl()  
```  
  
## <a name="see-also"></a>Consulte Também
 [Referência da Biblioteca do provedor WMI do Reporting Services &#40;SSRS&#41;](../wmi-provider-library-reference/reporting-services-wmi-provider-library-reference-ssrs.md)   
 [Arquivo de configuração RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
