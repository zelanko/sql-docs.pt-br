---
title: Usando criptografia sem validação | Microsoft Docs
description: Usando criptografia sem validação
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1c2b736c3bdb5c4e5154bfe1f56ff4a4ce18a656
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-encryption-without-validation"></a>Usando criptografia sem validação
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre criptografa pacotes de rede associados a logon. Se nenhum certificado tiver sido provisionado no servidor quando ele foi inicializado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerará um certificado autoassinado usado para criptografar pacotes de login.  

Os certificados autoassinados não garante a segurança. O handshake criptografado é baseado do NT LAN Manager (NTLM). É altamente recomendável que você forneça um certificado verificável no SQL Server para a conectividade segura. Camada de segurança de transporte (TLS) podem ser feitas segura somente com a validação do certificado.

Os aplicativos também podem solicitar a criptografia de todo o tráfego de rede usando palavras-chave de cadeia de conexão ou propriedades de conexão. As palavras-chave são "Encrypt" para OLE DB ao usar uma cadeia de caracteres do provedor com **IDBInitialize:: Initialize**, ou "Use Encryption for Data", para ADO e OLE DB ao usar uma cadeia de caracteres de inicialização com **IDataInitialize**. Isso também pode ser configurado com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Configuration Manager usando o **Forçar criptografia de protocolo** opção e pela configuração do cliente para solicitar conexões criptografadas. Por padrão, a criptografia de todo o tráfego de rede para uma conexão requer que um certificado seja aprovisionado no servidor. Definindo seu cliente para confiar no certificado do servidor, você pode ficar vulnerável a ataques man-in-the-middle. Se você implantar um certificado verificável no servidor, certifique-se de que você altere as configurações do cliente sobre o certificado de confiança para FALSE.

Para obter informações sobre palavras-chave de cadeia de caracteres de conexão, consulte [usando Conexão String Keywords com OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md ).  
  
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

## <a name="ole-db-driver-for-sql-server"></a>Driver do OLE DB para SQL Server 
 O Driver OLE DB para SQL Server dá suporte a criptografia sem validação por meio da adição da propriedade de inicialização de SSPROP_INIT_TRUST_SERVER_CERTIFICATE dados fonte, que é implementada no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT. Além disso, uma conexão nova palavra-chave string, "TrustServerCertificate", foi adicionada. Ele aceita valores Sim ou não. não é o padrão. Ao usar componentes de serviço, aceita os valores true ou false; false é o padrão.  
  
 Para obter mais informações sobre aprimoramentos feitos ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [propriedades de inicialização e autorização](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Consulte também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
