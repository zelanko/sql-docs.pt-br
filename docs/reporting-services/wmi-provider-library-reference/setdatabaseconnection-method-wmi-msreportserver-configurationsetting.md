---
title: "M&#233;todo SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "Método SetDatabaseConnection"
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
caps.latest.revision: 19
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting)
  Define a conexão do banco de dados do servidor de relatório para um banco de dados do servidor de relatório específico.  
  
## Sintaxe  
  
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
  
## Parâmetros  
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
  
## Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## Comentários  
 Quando o parâmetro *CredentialsType* for definido como 0 (Windows), os parâmetros *UserName* e *Password* devem ser definidos. O parâmetro *UserName* deve estar no formulário "domain\username" e o valor deve representar um logon de Windows válido.  
  
 Quando o parâmetro *CredentialsType* for definido como 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), o valor transmitido no parâmetro *UserName* deverá estar em conformidade com os requisitos de um nome de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando o parâmetro *CredentialsType* é definido como 2 (serviço Windows), o servidor de relatório usa a segurança integrada para se conectar ao banco de dados do servidor de relatório, e os parâmetros *UserName* e *Password* são ignorados. O serviço Web do servidor de relatório usará a conta [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ou uma conta do pool de aplicativos e a conta do serviço do Windows para acessar o banco de dados do servidor de relatório.  
  
 Quando chamado, o método SetDatabaseConnection criptografa e armazena as credenciais e informações do banco de dados no arquivo de configuração para o servidor de relatório especificado.  
  
 O método SetDatabaseConnection não verifica se o servidor de relatório pode se conectar ao banco de dados do servidor de relatório usando os dados especificados.  
  
 Quando configurada pela primeira vez, a propriedade ConnectionPoolSize é definida com base nos seguintes processadores: ConnectionPoolSize = #Processadores * 75.  
  
 O método SetDatabaseConnection não concede permissões para as contas especificadas. Você deve chamar o método [GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/generatedatabaserightsscript-method-wmi-msreportserver-configurationsetting.md) para cada conta que requer acesso ao banco de dados do servidor de relatório e executar o script resultante.  
  
## Requisitos  
 **Namespace: ** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  