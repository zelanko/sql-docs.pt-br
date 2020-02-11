---
title: Classe SqlErrorLogFile
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0dd923f17fe0267edf40d07da982d0856ec4ba06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73659050"
---
# <a name="sqlerrorlogfile-class"></a>Classe SqlErrorLogFile
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Fornece propriedades para exibição de informações sobre um arquivo de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
class SQLErrorLogFile  
{  
   uint32ArchiveNumber;  
   stringInstanceName;  
   datetimeLastModified;  
   uint32LogFileSize;  
   stringName;  
  
};  
```  
  
## <a name="properties"></a>Propriedades  
 A classe sqllogsfile define as propriedades a seguir.  
  
|||  
|-|-|  
|ArchiveNumber|Tipo de dados: **UInt32**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> O número do arquivo morto do arquivo de log.|  
|InstanceName|Tipo de dados: **cadeia de caracteres**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> Qualificadores: Chave<br /><br /> <br /><br /> O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o arquivo de log reside.|  
|LastModified|Tipo de dados: **DateTime**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> A data da última modificação do arquivo de log.|  
|LogFileSize|Tipo de dados: **UInt32**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> O tamanho do arquivo de log, em bytes.|  
|Nome|Tipo de dados: **cadeia de caracteres**<br /><br /> Tipo de acesso: Somente leitura<br /><br /> Qualificadores: Chave<br /><br /> <br /><br /> O nome do arquivo de log.|  
  
## <a name="remarks"></a>Comentários  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Namespace|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir recupera informações sobre todos os arquivos de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para executar o exemplo, substitua \< *Instance_Name*> pelo nome da instância, por exemplo, ' instance1 '.  
  
```  
on error resume next  
set strComputer = "."  
set objWMIService = GetObject("winmgmts:\\.\root\Microsoft\SqlServer\ComputerManagement10")  
set LogFiles = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogFile WHERE InstanceName = '<Instance_Name>'")  
  
For Each logFile in LogFiles  
  
WScript.Echo "Instance Name:  " & logFile.InstanceName & vbNewLine _  
    & "Log File Name:  " & logFile.Name & vbNewLine _  
    & "Archive Number: " & logFile.ArchiveNumber & vbNewLine _  
    & "Log File Size:  " & logFile.LogFileSize & " bytes" & vbNewLine _  
    & "Last Modified:  " & logFile.LastModified & vbNewLine _  
  
Next   
```  
  
## <a name="comments"></a>Comentários  
 Quando *InstanceName* não for fornecido na instrução WQL, a consulta retornará informações para a instância padrão. Por exemplo, a instrução WQL a seguir retornará informações sobre todos os arquivos de log da instância padrão (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>Segurança  
 Para se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um arquivo de log por meio do WMI, você deve ter as seguintes permissões nos computadores locais e remotos:  
  
-   Acesso de leitura ao namespace WMI do **Root\Microsoft\SqlServer\ComputerManagement10** . Por padrão, todos usuários têm acesso de leitura por meio da permissão Habilitar Conta.  
  
    > [!NOTE]  
    >  Para obter informações sobre como verificar as permissões de WMI, consulte a seção segurança do tópico [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
-   Permissão de leitura para a pasta que contém os logs de erros. Por padrão, os logs de erros estão localizados no caminho a seguir \<(em que a *unidade>* representa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unidade \<em que você instalou e *InstanceName*> é o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nome da instância do):  
  
     **Unidade>: \Program Files\Microsoft SQL Server\MSSQL11. \<** **\< InstanceName> \MSSQL\Log**  
  
 Se você se conectar através de um firewall, verifique se uma exceção está definida no firewall para WMI em computadores de destino remotos. Para obter mais informações, consulte [conectando-se ao WMI remotamente a partir do Windows Vista](https://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Consulte Também  
 [Classe SqlErrorLogEvent](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md)   
 [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md)  
  
  
