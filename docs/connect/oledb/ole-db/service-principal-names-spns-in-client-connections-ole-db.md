---
title: SPNs (Nomes da Entidade de Serviço) em conexões de cliente (OLE DB) | Microsoft Docs
description: SPNs (Nomes da Entidade de Serviço) em conexões de cliente (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c758a55b39eeecde4a3a713bc13462f01aa77a32
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015183"
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>SPNs (Nomes da Entidade de Serviço) em conexões de cliente (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]


  Este tópico descreve as propriedades OLE DB e as funções de membro que dão suporte a SPNs (nomes da entidade de serviço) em aplicativos clientes. Para obter mais informações sobre SPNs em aplicativos cliente, confira [Nome da entidade de serviço &#40;SPN&#41; Suporte em conexões de cliente](../../oledb/features/service-principal-name-spn-support-in-client-connections.md). Para ver um exemplo, confira [Autenticação Kerberos integrada &#40;OLE DB&#41;](../../oledb/ole-db-how-to/integrated-kerberos-authentication-ole-db.md).  
  
## <a name="provider-initialization-string-keywords"></a>Palavras-chave da cadeia de caracteres de inicialização do provedor  
 As palavras-chave da cadeia de caracteres de inicialização de provedor a seguir dão suporte a SPNs em aplicativos OLE DB. Na tabela a seguir, os valores na coluna de palavra-chave são usados para a cadeia de caracteres do provedor de IDBInitialize::Initialize. Os valores na coluna de descrição são usados em cadeias de inicialização na conexão usando o ADO ou IDataInitialize::GetDataSource.  
  
|Palavra-chave|DESCRIÇÃO|Valor|  
|-------------|-----------------|-----------|  
|ServerSPN|SPN do servidor|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia, o que faz com que o Driver do OLE DB para SQL Server use o SPN padrão gerado pelo provedor.|  
|FailoverPartnerSPN|SPN do parceiro de failover:|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia, o que faz com que o Driver do OLE DB para SQL Server use o SPN padrão gerado pelo provedor.|  
  
## <a name="data-source-initialization-properties"></a>Propriedades de inicialização da fonte de dados  
 As propriedades a seguir do conjunto de propriedades **DBPROPSET_SQLSERVERDBINIT** permitem que os aplicativos especifiquem SPNs.  
  
|Nome|Type|Uso|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR, leitura/gravação|Especifica o SPN do servidor. O valor padrão é uma cadeia de caracteres vazia, o que faz com que o Driver do OLE DB para SQL Server use o SPN padrão gerado pelo provedor.|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR, leitura/gravação|Especifica o SPN para o parceiro de failover. O valor padrão é uma cadeia de caracteres vazia, o que faz com que o Driver do OLE DB para SQL Server use o SPN padrão gerado pelo provedor.|  
  
## <a name="data-source-properties"></a>Propriedades de fonte de dados  
 As propriedades a seguir do conjunto de propriedades **DBPROPSET_SQLSERVERDATASOURCEINFO** permitem que os aplicativos descubram o método de autenticação.  
  
|Nome|Type|Uso|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR, somente leitura|Retorna o método de autenticação usado para a conexão. O valor retornado ao aplicativo é o valor que o Windows retorna ao Driver do OLE DB para SQL Server. O valores possíveis são os seguintes: <br />"NTLM", que é retornado quando uma conexão é aberta usando a autenticação NTLM.<br />"Kerberos", que é retornado quando uma conexão é aberta usando a autenticação Kerberos.<br /><br /> Se uma conexão foi aberta e não for possível determinar o método de autenticação, VT_EMPTY será retornado.<br /><br /> Essa propriedade só pode ser lida quando uma fonte de dados tiver sido inicializada. Se você tentar ler a propriedade antes da inicialização da fonte de dados, IDBProperties::GetProperies retornará DB_S_ERRORSOCCURRED ou DB_E_ERRORSOCCURRED, conforme apropriado, e DBPROPSTATUS_NOTSUPPORTED será definido em DBPROPSET_PROPERTIESINERROR para essa propriedade. Esse comportamento está de acordo com a especificação principal do OLE DB.|  
|SSPROP_MUTUALLYAUTHENICATED|VT_BOOL, somente leitura|Retorna VARIANT_TRUE se os servidores da conexão forem autenticados mutuamente. Caso contrário, retorna VARIANT_FALSE.<br /><br /> Essa propriedade só pode ser lida quando uma fonte de dados tiver sido inicializada. Se houver uma tentativa de ler a propriedade antes da inicialização da fonte de dados, IDBProperties::GetProperies retornará DB_S_ERRORSOCCURRED ou DB_E_ERRORSOCCURRED, conforme apropriado, e DBPROPSTATUS_NOTSUPPORTED será definido em DBPROPSET_PROPERTIESINERROR para essa propriedade. Esse comportamento está de acordo com a especificação principal do OLE DB<br /><br /> Se esse atributo for consultado para uma conexão que não usou a Autenticação do Windows, será retornado VARIANT_FALSE.|  
  
## <a name="ole-db-api-support-for-spns"></a>Suporte de API do OLE DB para SPNs  
 A tabela a seguir descreve o as funções do membro OLE DB que dá suporte a SPNs em conexões do cliente:  
  
|Função de membro|DESCRIÇÃO|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString* pode conter as novas palavras-chave **ServerSPN** e **FailoverPartnerSPN**.|  
|IDataInitialize::GetInitializationString|Se SSPROP_INIT_SERVERSPN e SSPROP_INIT_FAILOVERPARTNERSPN tiverem valores não padrão, eles serão incluídos na cadeia de caracteres de inicialização por meio dos valores de palavra-chave *ppwszInitString* para **ServerSPN** e **FailoverPartnerSPN**. Caso contrário, essas palavras-chave não serão incluídas na cadeia de inicialização.|  
|IDBInitialize::Initialize|Se o aviso for habilitado pela definição de DBPROP_INIT_PROMPT nas propriedades de inicialização da fonte de dados, a caixa de diálogo Logon no OLE DB será exibida. Isto permite que os SPNs sejam inseridos no servidor principal e no seu parceiro de failover.<br /><br /> Se a cadeia de caracteres do provedor em DPPROP_INIT_PROVIDERSTRING estiver definida, ela reconhecerá as novas palavras-chave **ServerSPN** e **FailoverPartnerSPN** e usará seus valores, caso estejam presentes, para inicializar SSPROP_INIT_SERVER_SPN e SSPROP_INIT_FAILOVER_PARTNER_SPN.<br /><br /> IDBProperties::SetProperties pode ser chamada para definir as propriedades SSPROP_INIT_SERVER_SPN e SSPROP_INIT_FAILOVER_PARTNER_SPN antes de IDBInitialize::Initialize ser chamado. Essa é uma alternativa ao uso de uma cadeia de caracteres de provedor.<br /><br /> Se uma propriedade for definida em mais de um local, um valor definido programaticamente terá precedência sobre um conjunto de valor na cadeia de caracteres de provedor. Um valor definido na cadeia de inicialização tem precedência sobre um valor definido em uma caixa de diálogo de login.<br /><br /> Se a mesma palavra-chave aparecer mais de uma vez na cadeia de caracteres de provedor, o valor da primeira ocorrência terá precedência.|  
|IDBProperties::GetProperties|IDBProperties::GetProperties pode ser chamado para obter os valores das novas propriedades de inicialização da fonte de dados SSPROP_INIT_SERVERSPN e SSPROP_INIT_FAILOVERPARTNERSPN, e das novas propriedades da fonte de dados SSPROP_AUTHENTICATIONMETHOD e SSPROP_MUTUALLYAUTHENTICATED.|  
|IDBProperties::GetPropertyInfo|IdbProperties::GetPropertyInfo incluirá as novas propriedades de inicialização da fonte de dados SSPROP_INIT_SERVERSPN e SSPROP_INIT_FAILOVERPARTNERSPN, ou as novas propriedades da fonte de dados SSPROP_AUTHENTICATION_METHOD e SSPROP_MUTUALLYAUTHENTICATED.|  
|IDBProperties::SetProperties|IDBProperties::SetProperties pode ser chamado para definir os valores das novas propriedades de inicialização da fonte de dados SSPROP_INITSERVERSPN e SSPROP_INIT_FAILOVERPARTNERSPN.<br /><br /> Essas propriedades podem ser definidas a qualquer momento, mas se a fonte de dados já estiver aberta, o erro a seguir será retornado:DB_E_ERRORSOCCURRED, "Operação de várias etapas do OLE DB gerou erros. Verifique todos os valores de status do OLE DB, se disponíveis. Não foram executados trabalhos."|  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
