---
title: "Usando criptografia sem validação | Microsoft Docs"
ms.custom: 
ms.date: 12/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d19f47d30ddb7c4849f31611e0bc59170404a52c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="using-encryption-without-validation"></a>Usando criptografia sem validação
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre criptografa pacotes de rede associados a logon. Se nenhum certificado tiver sido provisionado no servidor quando ele foi inicializado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerará um certificado autoassinado usado para criptografar pacotes de login.  

Os certificados autoassinados não garante a segurança. O handshake criptografado é baseado do NT LAN Manager (NTLM). É altamente recomendável que você forneça um certificado verificável no SQL Server para a conectividade segura. Camada de segurança de transporte (TLS) podem ser feitas segura somente com a validação do certificado.

Os aplicativos também podem solicitar a criptografia de todo o tráfego de rede usando palavras-chave de cadeia de conexão ou propriedades de conexão. As palavras-chave são "Encrypt" para ODBC e OLE DB ao usar uma cadeia de caracteres do provedor com **IDBInitialize:: Initialize**, ou "Use Encryption for Data", para ADO e OLE DB ao usar uma cadeia de caracteres de inicialização com **IDataInitialize** . Isso também pode ser configurado com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Configuration Manager usando o **Forçar criptografia de protocolo** opção e pela configuração do cliente para solicitar conexões criptografadas. Por padrão, a criptografia de todo o tráfego de rede para uma conexão requer que um certificado seja aprovisionado no servidor. Definindo seu cliente para confiar no certificado do servidor, você pode ficar vulnerável a ataques man-in-the-middle. Se você implantar um certificado verificável no servidor, certifique-se de que você altere as configurações do cliente sobre o certificado de confiança para FALSE.

Para obter informações sobre palavras-chave de cadeia de caracteres de conexão, consulte [usando Conexão String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para habilitar a criptografia a ser usado quando um certificado não tiver sido provisionado no servidor, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Configuration Manager pode ser usado para definir ambos os **Forçar criptografia de protocolo** e o **confiar em certificado do servidor**  opções. Neste caso, a criptografia usará um certificado do servidor autoassinado sem validação, se nenhum certificado verificável tiver sido provisionado no servidor.  
  
 Os aplicativos também podem usar a palavra-chave "TrustServerCertificate" ou seu atributo de conexão associado para garantir a criptografia. As configurações do aplicativo nunca reduzem o nível de segurança definido pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Gerenciador de Configurações de Cliente, mas podem fortalecê-la. Por exemplo, se **Forçar criptografia de protocolo** não está definido para o cliente, um aplicativo pode solicitar criptografia por conta própria. Para garantir a criptografia até mesmo quando um certificado do servidor não foi provisionado, um aplicativo pode solicitar a criptografia e "TrustServerCertificate". Porém, se "TrustServerCertificate" não for habilitado na configuração do cliente, um certificado do servidor provisionado ainda será necessário. A tabela a seguir descreve todos os casos:  
  
|Configuração do cliente Forçar Criptografia de Protocolo|Configuração do cliente Confiar em Certificado do Servidor|Atributo de conexão/cadeia de conexão Criptografar/Usar criptografia de dados|Atributo de conexão/cadeia de conexão Confiar em Certificado do Servidor|Resultado|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|não|N/A|Não (padrão)|Ignored|Não ocorre criptografia.|  
|não|N/A|Sim|Não (padrão)|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|não|N/A|Sim|Sim|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  
|Sim|não|Ignored|Ignored|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Sim|Sim|Não (padrão)|Ignored|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  
|Sim|Sim|Sim|Não (padrão)|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Sim|Sim|Sim|Sim|A criptografia sempre ocorre, mas pode usar um certificado de servidor autoassinado.|  
||||||

> [!CAUTION]
> A tabela anterior só fornece um guia sobre o comportamento do sistema em configurações diferentes. Para a conectividade segura, certifique-se de que o cliente e o servidor exigem criptografia. Além disso, verifique se o servidor tem um certificado verificável e que o **TrustServerCertificate** configuração no cliente é definida como FALSE.

## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client oferece suporte à criptografia sem validação por meio da adição da propriedade de inicialização de SSPROP_INIT_TRUST_SERVER_CERTIFICATE dados fonte, que é implementada na propriedade DBPROPSET_SQLSERVERDBINIT conjunto. Além disso, uma conexão nova palavra-chave string, "TrustServerCertificate", foi adicionada. Ele aceita valores Sim ou não. não é o padrão. Ao usar componentes de serviço, aceita os valores true ou false; false é o padrão.  
  
 Para obter mais informações sobre aprimoramentos feitos ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [propriedades de inicialização e autorização](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte à criptografia sem validação por meio da adição de [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) funções. SQL_COPT_SS_TRUST_SERVER_CERTIFICATE foi adicionado para aceitar SQL_TRUST_SERVER_CERTIFICATE_YES ou SQL_TRUST_SERVER_CERTIFICATE_NO, com SQL_TRUST_SERVER_CERTIFICATE_NO sendo padrão. Além disso, uma nova palavra-chave de cadeia de conexão, “TrustServerCertificate”, foi adicionada. Ele aceita valores Sim ou não. "não" é o padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
