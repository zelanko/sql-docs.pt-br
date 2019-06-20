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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d652bc4ff516a03dfe2a0ff66b0b9f9590fea3c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62928738"
---
# <a name="using-encryption-without-validation"></a>Usando criptografia sem validação
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre criptografa pacotes de rede associados a logon. Se nenhum certificado tiver sido provisionado no servidor quando ele foi inicializado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerará um certificado autoassinado usado para criptografar pacotes de login.  

Os certificados autoassinados não garante a segurança. O handshake criptografado é baseado no Gerenciador de NTLM (NT LAN). É altamente recomendável que você forneça um certificado verificável no SQL Server para uma conectividade segura. Camada de segurança de transporte (TLS) podem ser feitas segura somente com a validação do certificado.

Os aplicativos também podem solicitar a criptografia de todo o tráfego de rede usando palavras-chave de cadeia de conexão ou propriedades de conexão. As palavras-chave são "Encrypt" para ODBC e OLE DB ao usar uma cadeia de caracteres de provedor **IDBInitialize:: Initialize**, ou "Use Encryption for Data", para ADO e OLE DB ao usar uma cadeia de caracteres de inicialização com **IDataInitialize** . Isso também pode ser configurado com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager usando o **Forçar criptografia de protocolo** opção e, configurando o cliente para solicitar conexões criptografadas. Por padrão, a criptografia de todo o tráfego de rede para uma conexão requer que um certificado seja aprovisionado no servidor. Definindo o seu cliente para confiar no certificado no servidor, você pode se tornar vulnerável a ataques man-in-the-middle. Se você implantar um certificado verificável no servidor, certifique-se de que você altere as configurações do cliente sobre o certificado de confiança para FALSE.

Para obter informações sobre palavras-chave de cadeia de caracteres de conexão, consulte [usando Conexão String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para permitir o uso da criptografia quando um certificado não for provisionado no servidor, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager poderá ser usado para definir as opções **Forçar Criptografia de Protocolo** e **Confiar em Certificado do Servidor**. Neste caso, a criptografia usará um certificado do servidor autoassinado sem validação, se nenhum certificado verificável tiver sido provisionado no servidor.  
  
 Os aplicativos também podem usar a palavra-chave "TrustServerCertificate" ou seu atributo de conexão associado para garantir a criptografia. As configurações do aplicativo nunca reduzem o nível de segurança definido pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Gerenciador de Configurações de Cliente, mas podem fortalecê-la. Por exemplo, se a opção **Forçar Criptografia de Protocolo** não for definida para o cliente, um aplicativo poderá solicitar a criptografia por conta própria. Para garantir a criptografia até mesmo quando um certificado do servidor não foi provisionado, um aplicativo pode solicitar a criptografia e "TrustServerCertificate". Porém, se "TrustServerCertificate" não for habilitado na configuração do cliente, um certificado do servidor provisionado ainda será necessário. A tabela a seguir descreve todos os casos:  
  
|Configuração do cliente Forçar Criptografia de Protocolo|Configuração do cliente Confiar em Certificado do Servidor|Atributo de conexão/cadeia de conexão Criptografar/Usar criptografia de dados|Atributo de conexão/cadeia de conexão Confiar em Certificado do Servidor|Resultado|  
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
> A tabela anterior apenas fornece um guia sobre o comportamento do sistema em configurações diferentes. Para a conectividade segura, certifique-se de que o cliente e o servidor exigem criptografia. Também verifique se o servidor tem um certificado verificável e que o **TrustServerCertificate** configuração no cliente é definida como FALSE.

## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte à criptografia sem validação por meio da adição da propriedade de inicialização de SSPROP_INIT_TRUST_SERVER_CERTIFICATE dados fonte, que é implementada na propriedade DBPROPSET_SQLSERVERDBINIT Defina. Além disso, uma nova palavra-chave de cadeia de conexão, "TrustServerCertificate", foi adicionada. Ela aceita os valores sim ou não; não é o padrão. Ao usar componentes de serviço, aceita os valores true ou false; false é o padrão.  
  
 Para obter mais informações sobre os aprimoramentos feitos no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [propriedades de inicialização e autorização](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client dá suporte à criptografia sem validação por meio de adições para o [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) funções. SQL_COPT_SS_TRUST_SERVER_CERTIFICATE foi adicionado para aceitar SQL_TRUST_SERVER_CERTIFICATE_YES ou SQL_TRUST_SERVER_CERTIFICATE_NO, com SQL_TRUST_SERVER_CERTIFICATE_NO sendo padrão. Além disso, uma nova palavra-chave de cadeia de conexão, “TrustServerCertificate”, foi adicionada. Ele aceita valores Sim ou não; "não" é o padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
