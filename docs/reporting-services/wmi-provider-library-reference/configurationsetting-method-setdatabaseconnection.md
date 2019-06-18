---
title: Método SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: af40d79d876edb8f0448bd5abaef5c173a6edce9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65572594"
---
# <a name="configurationsetting-method---setdatabaseconnection"></a>Método de ConfigurationSetting – SetDatabaseConnection
  Define a conexão do banco de dados do servidor de relatório para um banco de dados do servidor de relatório específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Servidor*  
 O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para hospedar o banco de dados do servidor de relatório.  
  
 *DatabaseName*  
 O nome do banco de dados do servidor de relatório.  
  
 *CredentialsType*  
 O tipo de credenciais a ser usada para a conexão. Os valores podem ser:  
  
-   0 - Windows  
  
-   1 – [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 - Serviço do Windows  
  
 *UserName*  
 O nome de conta usada para se conectar ao banco de dados do servidor de relatório.  
  
 *Senha*  
 A senha usada para se conectar ao banco de dados do servidor de relatório.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Remarks  
 Quando o parâmetro *CredentialsType* for definido como 0 (Windows), os parâmetros *UserName* e *Password* devem ser definidos. O parâmetro *UserName* deve estar no formulário "domain\username" e o valor deve representar um logon de Windows válido.  
  
 Quando o parâmetro *CredentialsType* é definido como 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), o valor passado no parâmetro *UserName* precisa estar em conformidade com os requisitos de um nome de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando o parâmetro *CredentialsType* é definido como 2 (serviço Windows), o servidor de relatório usa a segurança integrada para se conectar ao banco de dados do servidor de relatório, e os parâmetros *UserName* e *Password* são ignorados. O serviço Web Servidor de Relatórios usará a conta [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ou uma conta do pool de aplicativos e a conta de serviço Windows para acessar o banco de dados do servidor de relatório.  
  
 Quando chamado, o método SetDatabaseConnection criptografa e armazena as credenciais e informações do banco de dados no arquivo de configuração para o servidor de relatório especificado.  
  
 O método SetDatabaseConnection não verifica se o servidor de relatório pode se conectar ao banco de dados do servidor de relatório usando os dados especificados.  
  
 Quando configurada pela primeira vez, a propriedade ConnectionPoolSize é definida com base nos seguintes processadores: ConnectionPoolSize = #Processadores * 75.  
  
 O método SetDatabaseConnection não concede permissões para as contas especificadas. Você deve chamar o método [GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md) para cada conta que requer acesso ao banco de dados do servidor de relatório e executar o script resultante.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
