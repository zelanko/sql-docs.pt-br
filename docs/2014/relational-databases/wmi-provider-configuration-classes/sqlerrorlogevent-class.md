---
title: Classe SqlErrorLogEvent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 558e60a5638ab3af75c5450e3f6fc22c6f9d9601
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721071"
---
# <a name="sqlerrorlogevent-class"></a>Classe SqlErrorLogEvent
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
|FileName|Tipo de dados: `string`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> O nome do arquivo do log de erros.|  
|InstanceName|Tipo de dados: `string`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> Qualificadores: Chave<br /><br /> O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o arquivo de log reside.|  
|LogDate|Tipo de dados: `datetime`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> Qualificadores: Chave<br /><br /> <br /><br /> A data e a hora em que o evento foi gravado no arquivo de log.|  
|Mensagem|Tipo de dados: `string`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> A mensagem do evento.|  
|ProcessInfo|Tipo de dados: `string`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> Informações sobre a SPID (ID do processo do servidor de origem) do evento.|  
  
## <a name="remarks"></a>Comentários  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Namespace|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como recuperar valores para todos os eventos registrados em um arquivo de log especificado. Para executar o exemplo, substitua \< *Instance_Name*> pelo nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como ' instance1 ' e substitua ' file_name ' pelo nome do arquivo de log de erros, como ' cafiler. 1 '.  
  
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
 Quando *InstanceName* ou *filename* não forem fornecidos na instrução WQL, a consulta retornará informações para a instância padrão e o arquivo de log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. Por exemplo, a instrução WQL a seguir retornará todos os eventos de log do arquivo de log atual (ERRORLOG) na instância padrão (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>Segurança  
 Para se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um arquivo de log por meio do WMI, você deve ter as seguintes permissões nos computadores locais e remotos:  
  
-   Acesso de leitura ao namespace WMI do **Root\Microsoft\SqlServer\ComputerManagement10** . Por padrão, todos usuários têm acesso de leitura por meio da permissão Habilitar Conta.  
  
-   Permissão de leitura para a pasta que contém os logs de erros. Por padrão, os logs de erros estão localizados no caminho a seguir \<(em que a *unidade>* representa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unidade \<em que você instalou e *InstanceName*> é o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nome da instância do):  
  
     **Unidade>: \Program Files\Microsoft SQL Server\MSSQL12. \<** **\< InstanceName> \MSSQL\Log**  
  
 Se você se conectar através de um firewall, verifique se uma exceção está definida no firewall para WMI em computadores de destino remotos. Para obter mais informações, consulte [conectando-se ao WMI remotamente a partir do Windows Vista](https://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Consulte Também  
 [Classe sqllogsfile](sqlerrorlogfile-class.md)   
 [Exibir arquivos de log offline](../logs/view-offline-log-files.md)  
  
  
