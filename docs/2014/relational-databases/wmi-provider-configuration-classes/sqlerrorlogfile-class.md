---
title: Classe SqlErrorLogFile | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5e23c4512f04370fa24b3eb4ff3b74a072f6a2e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117395"
---
# <a name="sqlerrorlogfile-class"></a>Classe SqlErrorLogFile
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
 A classe SQLErrorLogFile define as propriedades a seguir.  
  
|||  
|-|-|  
|ArchiveNumber|Tipo de dados: `uint32`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> O número do arquivo morto do arquivo de log.|  
|InstanceName|Tipo de dados: `string`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> Qualificadores: Chave<br /><br /> <br /><br /> O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o arquivo de log reside.|  
|LastModified|Tipo de dados: `datetime`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> A data da última modificação do arquivo de log.|  
|LogFileSize|Tipo de dados: `uint32`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> <br /><br /> O tamanho do arquivo de log, em bytes.|  
|Nome|Tipo de dados: `string`<br /><br /> Tipo de acesso: Somente leitura<br /><br /> Qualificadores: Chave<br /><br /> <br /><br /> O nome do arquivo de log.|  
  
## <a name="remarks"></a>Remarks  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Namespace|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir recupera informações sobre todos os arquivos de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para executar o exemplo, substitua \< *Instance_Name*> com o nome da instância, por exemplo, 'instância1'.  
  
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
 Quando *InstanceName* não é fornecido na instrução WQL, a consulta retornará informações para a instância padrão. Por exemplo, a instrução WQL a seguir retornará informações sobre todos os arquivos de log da instância padrão (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>Segurança  
 Para se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo de log por meio do WMI, você deve ter as seguintes permissões em ambos os computadores locais e remotos:  
  
-   Acesso de leitura para o **Root\Microsoft\SqlServer\ComputerManagement10** namespace WMI. Por padrão, todos usuários têm acesso de leitura por meio da permissão Habilitar Conta.  
  
    > [!NOTE]  
    >  Para obter informações sobre como verificar permissões de WMI, consulte a seção de segurança do tópico [arquivos de Log Offline exibição](../logs/view-offline-log-files.md).  
  
-   Permissão de leitura para a pasta que contém os logs de erros. Por padrão, o erro logs estão localizados no caminho a seguir (onde \< *Drive >* representa a unidade onde você instalou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e \< *InstanceName*> é o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<Unidade >: Server \ mssql11 SQL de \Program Files\Microsoft** **.\< InstanceName > \mssql\log.**  
  
 Se você se conectar através de um firewall, verifique se uma exceção está definida no firewall para WMI em computadores de destino remotos. Para obter mais informações, consulte [se conectar ao WMI remotamente começando com o Windows Vista](http://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Consulte também  
 [Classe SqlErrorLogEvent](sqlerrorlogevent-class.md)   
 [Exibir arquivos de log offline](../logs/view-offline-log-files.md)  
  
  