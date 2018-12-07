---
title: Método GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- GenerateDatabaseRightsScript method
ms.assetid: f2e6dcc9-978f-4c2c-bafe-36c330247fd0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d08234fcf8e50851d40a86859244e6bc2840fd1f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526401"
---
# <a name="configurationsetting-method---generatedatabaserightsscript"></a>Método de ConfigurationSetting – GenerateDatabaseRightsScript
  Gera um Script SQL que pode ser usado para conceder direitos de usuário ao banco de dados do servidor de relatório e a outros bancos de dados necessários para a execução de um servidor de relatório. O chamador deve se conectar ao servidor de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executar o script.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub GenerateDatabaseRightsScript(ByVal UserName As String, _  
    ByVal DatabaseName As String, ByVal IsRemote As Boolean, _  
    ByVal IsWindowsUser As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseRightsScript(string UserName, string DatabaseName, bool IsRemote, bool IsWindowsUser, out string Script,   
out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *UserName*  
 O nome de usuário ou o identificador de segurança (SID) do Windows do usuário ao qual o script concederá direitos.  
  
 *DatabaseName*  
 O nome do banco de dados para o qual o script concederá acesso ao usuário.  
  
 *IsRemote*  
 Um valor Booleano que indica se o banco de dados é remoto em relação ao servidor de relatório.  
  
 *IsWindowsUser*  
 Um valor Booleano que indica se o nome de usuário especificado é de um usuário do Windows ou de um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 *Script*  
 [out] Uma cadeia de caracteres que contém o script [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerado.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Remarks  
 Se *DatabaseName* ficar vazio, *IsRemote* será ignorado e o valor do arquivo de configuração do servidor de relatório será usado como o nome do banco de dados.  
  
 Se *IsWindowsUser* for definido como **true**, *UserName* deverá estar no formato \<domain>\\<username\>.  
  
 Quando *IsWindowsUser* é definido como **true**, o script gerado concede direitos de logon ao usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], configurando o banco de dados do servidor de relatório como o banco de dados padrão, e concede a função **RSExec** no banco de dados do servidor de relatório, no banco de dados temporário do servidor de relatório, no banco de dados mestre e no banco de dados do sistema MSDB.  
  
 Quando *IsWindowsUser* é definido como **true**, o método aceita os SIDs do Windows padrão como entrada. Quando um SID do Windows padrão ou nome de conta de serviço é fornecido, ele é convertido em uma cadeia de caracteres de nome de usuário. Se o banco de dados for local, a conta será convertida para a representação localizada correta da conta. Se o banco de dados for remoto, a conta será representada como a conta do computador.  
  
 A tabela a seguir mostra as contas que são convertidas e sua representação remota.  
  
|Conta/SID que está convertido|Nome comum|Nome remoto|  
|---------------------------------------|-----------------|-----------------|  
|(S-1-5-18)|Sistema Local|\<Domain>\\<ComputerName\>$|  
|.\LocalSystem|Sistema Local|\<Domain>\\<ComputerName\>$|  
|Nome do computador\sistema local|Sistema Local|\<Domain>\\<ComputerName\>$|  
|LocalSystem|Sistema Local|\<Domain>\\<ComputerName\>$|  
|(S-1-5-20)|Serviço de Rede|\<Domain>\\<ComputerName\>$|  
|NT AUTHORITY\NetworkService|Serviço de Rede|\<Domain>\\<ComputerName\>$|  
|(S-1-5-19)|Serviço Local|Erro – veja abaixo.|  
|NT AUTHORITY\LocalService|Serviço Local|Erro – veja abaixo.|  
  
 No [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)], se você estiver usando uma conta interna e o banco de dados do servidor de relatório for remoto, será retornado um erro.  
  
 Se a conta interna **LocalService** for especificada e o banco de dados do servidor de relatório for remoto, um erro será retornado.  
  
 Quando *IsWindowsUser* for true e o valor fornecido no *UserName* precisar ser convertido, o provedor WMI determinará se o banco de dados do servidor de relatório está localizado no mesmo computador ou em um computador remoto. Para determinar se a instalação é local, o provedor de WMI avaliará a propriedade DatabaseServerName da lista de valores a seguir. Se uma correspondência for localizada, o banco de dados é local. Caso contrário, é remoto. A comparação não diferencia maiúsculas e minúsculas.  
  
|Valor do DatabaseServerName|Exemplo|  
|---------------------------------|-------------|  
|"."||  
|"(local)"||  
|"LOCAL"||  
|localhost||  
|\<Machinename>|testlab14|  
|\<MachineFQDN>|example.redmond.microsoft.com|  
|\<IPAddress>|180.012.345,678|  
  
 Quando *IsWindowsUser* é definido como **true**, o provedor WMI chama LookupAccountName para obter o SID para a conta e, em seguida, chama LookupAccountSID para obter o nome para colocar no script [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso assegura que o nome da conta usado transmitirá a validação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Quando *IsWindowsUser* é definido como **false**, o script gerado concede a função **RSExec** no banco de dados do servidor de relatório, no banco de dados temporário do servidor de relatório e no banco de dados MSDB.  
  
 Quando *IsWindowsUser* é definido como **false**, o usuário do SQL Server já deve existir no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que o script seja executado corretamente.  
  
 Se o servidor de relatório não tiver um banco de dados do servidor de relatório especificado, a ação de chamar GrantRightsToDatabaseUser retornará um erro.  
  
 O script gerado dá suporte ao [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 e ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
