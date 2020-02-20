---
title: Usando criptografia sem validação | Microsoft Docs
description: Usando criptografia sem validação
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ef21cdb2a223aaa50b690f5b2b3c30696dd9e196
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67988854"
---
# <a name="using-encryption-without-validation"></a>Usando criptografia sem validação
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre criptografa pacotes de rede associados a logon. Se nenhum certificado tiver sido provisionado no servidor quando ele foi inicializado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerará um certificado autoassinado usado para criptografar pacotes de login.  

Os certificados autoassinados não garantem a segurança. O handshake criptografado é baseado no NTLM (NT LAN Manager). É altamente recomendável que você provisione um certificado verificável no SQL Server a fim de ter uma conectividade segura. O protocolo TLS pode se tornar seguro somente com a validação de certificado.

Os aplicativos também podem solicitar a criptografia de todo o tráfego de rede usando palavras-chave de cadeia de conexão ou propriedades de conexão. As palavras-chave são "Encrypt" para o OLE DB ao usar uma cadeia de caracteres do provedor com **IDbInitialize::Initialize** ou "Use Encryption for Data" para o ADO e o OLE DB ao usar uma cadeia de caracteres de inicialização com **IDataInitialize**. Isso também pode ser configurado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager usando a opção **Forçar Protocolo de Criptografia** e configurando o cliente para solicitar conexões criptografadas. Por padrão, a criptografia de todo o tráfego de rede para uma conexão requer que um certificado seja aprovisionado no servidor. Ao configurar o cliente para confiar no certificado no servidor, você pode se tornar vulnerável a ataques man-in-the-middle. Se você implantar um certificado verificável no servidor, será necessário alterar as configurações do cliente sobre confiar no certificado para FALSE.

Para obter informações sobre palavras-chave da cadeia de conexão, confira [Usando palavras-chave da cadeia de conexão com o OLE DB Driver for SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md ).  
  
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
> A tabela anterior fornece apenas um guia sobre o comportamento do sistema em diferentes configurações. Para conectividade segura, verifique se tanto o cliente quanto o servidor exigem criptografia. Verifique também se o servidor tem um certificado verificável e se a configuração **TrustServerCertificate** no cliente está definida como FALSE.

## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 
 O OLE DB Driver for SQL Server dá suporte à criptografia sem validação por meio da adição da propriedade de inicialização de fonte de dados SSPROP_INIT_TRUST_SERVER_CERTIFICATE, que é implementada no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT. Além disso, uma nova palavra-chave de cadeia de conexão, "TrustServerCertificate", foi adicionada. Ela aceita os valores sim ou não; não é o padrão. Ao usar componentes de serviço, aceita os valores true ou false; false é o padrão.  
  
 Para obter mais informações sobre aprimoramentos realizados no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, confira [Propriedades de inicialização e autorização](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
