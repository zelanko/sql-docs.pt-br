---
title: Usando criptografia sem validação | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7805a5bc9d18ab183ba1d741dc4962dd6e6fb196
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787992"
---
# <a name="using-encryption-without-validation"></a>Usando criptografia sem validação
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre criptografa pacotes de rede associados a logon. Se nenhum certificado tiver sido provisionado no servidor quando ele foi inicializado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerará um certificado autoassinado usado para criptografar pacotes de login.  

Os certificados autoassinados não garantem a segurança. O handshake criptografado é baseado no NTLM (NT LAN Manager). É altamente recomendável que você provisione um certificado verificável em SQL Server para conectividade segura. A camada de segurança de transporte (TLS) pode se tornar segura somente com a validação de certificado.

Os aplicativos também podem solicitar a criptografia de todo o tráfego de rede usando palavras-chave de cadeia de conexão ou propriedades de conexão. As palavras-chave são "Encrypt" para ODBC e OLE DB ao usar uma cadeia de caracteres de provedor com **IDBInitialize:: Initialize**ou "usar criptografia para dados" para ADO e OLE DB ao usar uma cadeia de inicialização com **IDataInitialize**. Isso também pode ser configurado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager usando a opção **forçar criptografia de protocolo** e Configurando o cliente para solicitar conexões criptografadas. Por padrão, a criptografia de todo o tráfego de rede para uma conexão requer que um certificado seja aprovisionado no servidor. Ao definir o cliente para confiar no certificado no servidor, você pode se tornar vulnerável a ataques man-in-the-Middle. Se você implantar um certificado verificável no servidor, certifique-se de alterar as configurações do cliente sobre confiar no certificado como falso.

Para obter informações sobre palavras-chave da cadeia de conexão, consulte [usando palavras-chave da cadeia de conexão com SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para permitir o uso da criptografia quando um certificado não for provisionado no servidor, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager poderá ser usado para definir as opções **Forçar Criptografia de Protocolo** e **Confiar em Certificado do Servidor**. Neste caso, a criptografia usará um certificado do servidor autoassinado sem validação, se nenhum certificado verificável tiver sido provisionado no servidor.  
  
 Os aplicativos também podem usar a palavra-chave "TrustServerCertificate" ou seu atributo de conexão associado para garantir a criptografia. As configurações do aplicativo nunca reduzem o nível de segurança definido pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Gerenciador de Configurações de Cliente, mas podem fortalecê-la. Por exemplo, se a opção **Forçar Criptografia de Protocolo** não for definida para o cliente, um aplicativo poderá solicitar a criptografia por conta própria. Para garantir a criptografia até mesmo quando um certificado do servidor não foi provisionado, um aplicativo pode solicitar a criptografia e "TrustServerCertificate". Porém, se "TrustServerCertificate" não for habilitado na configuração do cliente, um certificado do servidor provisionado ainda será necessário. A tabela a seguir descreve todos os casos:  
  
|Configuração do cliente Forçar Criptografia de Protocolo|Configuração do cliente Confiar em Certificado do Servidor|Atributo de conexão/cadeia de conexão Criptografar/Usar criptografia de dados|Atributo de conexão/cadeia de conexão Confiar em Certificado do Servidor|Result|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|Não|N/D|Não (padrão)|Ignored|Não ocorre criptografia.|  
|Não|N/D|Sim|Não (padrão)|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Não|N/D|Sim|Sim|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  
|Sim|Não|Ignored|Ignored|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Sim|Sim|Não (padrão)|Ignored|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  
|Sim|Sim|Sim|Não (padrão)|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Sim|Sim|Sim|Sim|A criptografia sempre ocorre, mas pode usar um certificado de servidor autoassinado.|  
||||||

> [!CAUTION]
> A tabela anterior fornece apenas um guia sobre o comportamento do sistema em diferentes configurações. Para conectividade segura, verifique se o cliente e o servidor exigem Criptografia. Verifique também se o servidor tem um certificado verificável e se a configuração **TrustServerCertificate** no cliente está definida como false.

## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte à criptografia sem validação por meio da adição da propriedade de inicialização da fonte de dados SSPROP_INIT_TRUST_SERVER_CERTIFICATE, que é implementada no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT. Além disso, uma nova palavra-chave de cadeia de conexão, "TrustServerCertificate", foi adicionada. Ela aceita os valores sim ou não; não é o padrão. Ao usar componentes de serviço, aceita os valores true ou false; false é o padrão.  
  
 Para obter mais informações sobre os aprimoramentos feitos no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [Propriedades de inicialização e autorização](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte à criptografia sem validação por meio de adições às funções [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) . SQL_COPT_SS_TRUST_SERVER_CERTIFICATE foi adicionado para aceitar SQL_TRUST_SERVER_CERTIFICATE_YES ou SQL_TRUST_SERVER_CERTIFICATE_NO, com SQL_TRUST_SERVER_CERTIFICATE_NO sendo padrão. Além disso, uma nova palavra-chave de cadeia de conexão, “TrustServerCertificate”, foi adicionada. Ele aceita sim ou nenhum valor; "não" é o padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
