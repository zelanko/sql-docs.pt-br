---
title: Classe SqlErrorLogEvent
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d2a07c87dea5be1a3d66c5e24996a120323d09ce
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738460"
---
# <a name="sqlerrorlogevent-class"></a>Classe SqlErrorLogEvent
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]
  Fornece propriedades para exibir eventos em um arquivo de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
class SQLErrorLogEvent   
{  
   stringFileName;  
   stringInstanceName;  
   datetimeLogDate;  
   stringMessage;  
   stringProcessInfo;  
};  
```  
  
## <a name="properties"></a>Propriedades  
 A classe SQLErrorLogEvent define as propriedades a seguir.  
  
|||  
|-|-|  
|FileName|Tipo de dados: **cadeia de caracteres**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> O nome do arquivo do log de erros.|  
|InstanceName|Tipo de dados: **cadeia de caracteres**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> Qualificadores: Chave<br /><br /> O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o arquivo de log reside.|  
|LogDate|Tipo de dados: **DateTime**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> Qualificadores: Chave<br /><br /> <br /><br /> A data e a hora em que o evento foi gravado no arquivo de log.|  
|Mensagem|Tipo de dados: **cadeia de caracteres**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> A mensagem do evento.|  
|ProcessInfo|Tipo de dados: **cadeia de caracteres**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> Informações sobre a SPID (ID do processo do servidor de origem) do evento.|  
  
## <a name="remarks"></a>Comentários  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Namespace|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como recuperar valores para todos os eventos registrados em um arquivo de log especificado. Para executar o exemplo, substitua \<*Instance_Name*> pelo nome da instância do, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ' instance1 ', e substitua ' file_name ' pelo nome do arquivo de log de erros, como ' cafiler. 1 '.  
  
```  
on error resume next  
strComputer = "."  
Set objWMIService = GetObject("winmgmts:" _  
    & "{impersonationLevel=impersonate}!\\" _  
    & strComputer & "\root\MICROSOFT\SqlServer\ComputerManagement10")  
set logEvents = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogEvent WHERE InstanceName = '<Instance_Name>' AND FileName = 'File_Name'")  
  
For Each logEvent in logEvents  
WScript.Echo "Instance Name: " & logEvent.InstanceName & vbNewLine _  
    & "Log Date: " & logEvent.LogDate & vbNewLine _  
    & "Log File Name: " & logEvent.FileName & vbNewLine _  
    & "Process Info: " & logEvent.ProcessInfo & vbNewLine _  
    & "Message: " & logEvent.Message & vbNewLine _  
  
Next  
```  
  
## <a name="comments"></a>Comentários  
 Quando *InstanceName* ou *filename* não forem fornecidos na instrução WQL, a consulta retornará informações para a instância padrão e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo de log atual. Por exemplo, a instrução WQL a seguir retornará todos os eventos de log do arquivo de log atual (ERRORLOG) na instância padrão (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>Segurança  
 Para se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo de log por meio do WMI, você deve ter as seguintes permissões nos computadores locais e remotos:  
  
-   Acesso de leitura ao namespace WMI do **Root\Microsoft\SqlServer\ComputerManagement10** . Por padrão, todos usuários têm acesso de leitura por meio da permissão Habilitar Conta.  
  
-   Permissão de leitura para a pasta que contém os logs de erros. Por padrão, os logs de erros estão localizados no caminho a seguir (em que \<*Drive> * representa a unidade em que você instalou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e \<*InstanceName*> é o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ):  
  
     ** \<Drive> : \Arquivos de Programas\microsoft SQL Server\MSSQL13** **. \<InstanceName> \MSSQL\Log**  
  
 Se você se conectar através de um firewall, verifique se uma exceção está definida no firewall para WMI em computadores de destino remotos. Para obter mais informações, consulte [conectando-se ao WMI remotamente a partir do Windows Vista](https://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Consulte Também  
 [Classe sqllogsfile](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md)  
  
  
