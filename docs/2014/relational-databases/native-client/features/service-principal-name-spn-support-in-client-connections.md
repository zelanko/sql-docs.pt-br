---
title: Suporte a SPN (Nome da Entidade de Serviço) em conexões de cliente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, SPNs
- ODBC, SPNs
- OLE DB, SPNs
- SPNs [SQL Server]
ms.assetid: 96598c69-ce9a-4090-aacb-d546591e8af7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42b25dfe8f0a39c577e38c6d1ef21c7f3315a89d
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "75231782"
---
# <a name="service-principal-name-spn-support-in-client-connections"></a>Suporte a SPN (Nome da entidade de serviço) em conexões com o cliente
  Do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] em diante, o suporte para SPNs (nomes das entidades de serviço) foi estendido para habilitar a autenticação mútua em todos os protocolos. Em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], apenas havia suporte para SPNs no Kerberos via TCP quando o SPN padrão da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] era registrado no Active Directory.  
  
 Os SPNs são usados pelo protocolo de autenticação para determinar a conta na qual uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é executada. Se a conta da instância for conhecida, autenticação Kerberos poderá ser usada para fornecer autenticação mútua pelo cliente e servidor. Se a conta de instância não for conhecida, a autenticação NTLM, que só fornece autenticação do cliente pelo servidor, será usada. Atualmente, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client executa a pesquisa de autenticação, derivando o SPN das propriedades de nome da instância e conexão de rede. As instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tentarão registrar os SPNs na inicialização, ou eles podem ser registrados manualmente. Porém, o registro falhará se houver direitos de acesso insuficientes para a conta que tenta registrar os SPNs.  
  
 As contas de domínio e computador são registradas automaticamente no Active Directory. Elas podem ser usadas como SPNs ou os administradores podem definir seus próprios SPNs. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] torna a autenticação segura mais gerenciável e confiável, permitindo que os clientes especifiquem diretamente o SPN a ser usado.  
  
> [!NOTE]  
>  Um SPN especificado por um aplicativo cliente é usado somente quando uma conexão é feita com a segurança integrada pelo Windows.  
  
> [!TIP]  
>  **Kerberos Configuration [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Manager for é uma ferramenta de diagnóstico que ajuda a solucionar problemas de conectividade relacionados ao Kerberos com . [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Para obter mais informações, consulte [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
> [!TIP]  
>  **Kerberos Configuration [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Manager for é uma ferramenta de diagnóstico que ajuda a solucionar problemas de conectividade relacionados ao Kerberos com . [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Para obter mais informações, consulte [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
 Para obter mais informações sobre Kerberos, consulte os artigos a seguir:  
  
-   [Suplemento técnico do Kerberos para Windows](https://go.microsoft.com/fwlink/?LinkId=101449)  
  
-   [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)  
  
## <a name="usage"></a>Uso  
 A tabela a seguir descreve os cenários mais comuns nos quais os aplicativos cliente podem habilitar a autenticação segura.  
  
|Cenário|Descrição|  
|--------------|-----------------|  
|Um aplicativo herdado não especifica um SPN.|Este cenário de compatibilidade garante que não haverá nenhuma alteração de comportamento para aplicativos desenvolvidos para versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se nenhum SPN for especificado, o aplicativo confiará nos SPNs gerados e não terá nenhum conhecimento de qual método de autenticação será usado.|  
|Um aplicativo cliente que usa a versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client especifica um SPN na cadeia de conexão como um usuário do domínio ou uma conta de computador, como um SPN específico da instância ou uma cadeia definida pelo usuário.|A palavra-chave `ServerSPN` pode ser usada em um provedor, uma inicialização ou uma cadeia de conexão para fazer o seguinte:<br /><br /> - Especifique [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a conta usada pela instância para uma conexão. Isto simplifica o acesso à autenticação Kerberos. Se um KDC (Centro de Distribuição de Chaves) Kerberos estiver presente e a conta correta for especificada, a autenticação Kerberos provavelmente será mais usada que NTLM. O KDC normalmente reside no mesmo computador que o controlador de domínio.<br />- Especifique um SPN para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] procurar a conta de serviço para a ocorrência. Para cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], são gerados dois SPNs padrão que podem ser usados para essa finalidade. Não há garantia de que estas chaves estejam presentes no Active Directory. Entretanto, nesta situação, a autenticação Kerberos não é garantida.<br />- Especifique um SPN que será usado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para procurar a conta de serviço para a ocorrência. Esta poderá ser qualquer cadeia de caracteres definida pelo usuário que mapeia para a conta de serviço. Neste caso, a chave deve ser registrada manualmente no KDC e deve satisfazer as regras para um SPN definido pelo usuário.<br /><br /> A palavra-chave `FailoverPartnerSPN` pode ser usada para especificar o SPN para o servidor de parceiro de failover. O intervalo de conta e valores de chave do Active Directory é igual aos valores que você pode especificar para o servidor principal.|  
|Um aplicativo ODBC especifica um SPN como um atributo de conexão para o servidor principal ou servidor de parceiro de failover.|O atributo de conexão `SQL_COPT_SS_SERVER_SPN` pode ser usado para especificar o SPN para uma conexão com o servidor principal.<br /><br /> O atributo de conexão `SQL_COPT_SS_FAILOVER_PARTNER_SPN` pode ser usado para especificar o SPN para o servidor de parceiro de failover.|  
|Um aplicativo OLE DB especifica um SPN como uma propriedade de inicialização de fonte de dados para o servidor principal ou para um servidor de parceiro de failover.|A propriedade de conexão `SSPROP_INIT_SERVER_SPN` no conjunto de propriedades `DBPROPSET_SQLSERVERDBINIT` pode ser usada para especificar o SPN para uma conexão.<br /><br /> A propriedade de conexão `SSPROP_INIT_FAILOVER_PARTNER_SPN` na `DBPROPSET_SQLSERVERDBINIT` pode ser usada para especificar o SPN para o servidor de parceiro de failover.|  
|Um usuário especifica um SPN para um servidor ou servidor de parceiro de failover em um DSN (nome de fonte de dados) ODBC.|O SPN pode ser especificado em um DSN ODBC pelas caixas de diálogo de configuração do DSN.|  
|O usuário especifica um SPN para um servidor ou servidor de parceiro de failover em uma caixa de diálogo **Vínculo de Dados** ou **Logon** no OLE DB.|O SPN pode ser especificado em uma caixa de diálogo **Vínculo de Dados** ou **Logon** . A caixa de diálogo **Logon** pode ser usada com ODBC ou OLE DB.|  
|Um aplicativo ODBC determina o método de autenticação usado para estabelecer uma conexão.|Quando uma conexão foi aberta com êxito, um aplicativo pode consultar o atributo de conexão `SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD` para determinar qual método de autenticação foi usado. Os valores incluirão (mas não estarão limitados a) `NTLM` e `Kerberos`.|  
|Um aplicativo OLE DB determina o método de autenticação usado para estabelecer uma conexão.|Quando uma conexão foi aberta com êxito, um aplicativo pode consultar a propriedade de conexão `SSPROP_AUTHENTICATION_METHOD` no conjunto de propriedades `DBPROPSET_SQLSERVERDATASOURCEINFO` para determinar qual método de autenticação foi usado. Os valores incluirão (mas não estarão limitados a) `NTLM` e `Kerberos`.|  
  
## <a name="failover"></a>Failover  
 Os SPNs não são armazenados no cache de failover e, portanto, não podem ser transmitidos entre conexões. Os SPNs serão usados em todas as tentativas de conexão com a entidade e o parceiro quando especificados na cadeia de conexão ou nos atributos de conexão.  
  
## <a name="connection-pooling"></a>Pool de conexões  
 Os aplicativos devem estar atentos que especificar SPNs em algumas, mas não em todas as cadeias de conexão, podem contribuir para o agrupamento da fragmentação.  
  
 Os aplicativos podem especificar SPNs programaticamente como atributos de conexão, em vez de especificar palavras-chave da cadeia de conexão. Isto pode ajudar no gerenciamento da fragmentação do pool de conexões.  
  
 Os aplicativos deverão saber que os SPNs nas cadeias de conexão possam ser substituídos definindo os atributos de conexão correspondentes, mas as cadeias de conexão usadas pelo pool de conexões usarão os valores da cadeia de conexão para fins de pool.  
  
## <a name="down-level-server-behavior"></a>Comportamento de servidor de versão anterior  
 O novo comportamento de conexão é implementado pelo cliente; portanto, ele não é específico para uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="linked-servers-and-delegation"></a>Servidores vinculados e delegação  
 Quando servidores vinculados são criados, o parâmetro `@provstr` de [sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) pode ser usado para especificar os SPNs do servidor e do parceiro de failover. Os benefícios disso é o mesmo que especificar SPNs em cadeias de conexão de cliente. É mais simples e confiável estabelecer conexões que usam autenticação Kerberos.  
  
 A delegação com servidores vinculados exige a autenticação Kerberos.  
  
## <a name="management-aspects-of-spns-specified-by-applications"></a>Aspectos de gerenciamento de SPNs especificados por aplicativos  
 Ao escolher se deseja especificar SPNs em um aplicativo (por meio de cadeias de conexão) ou, programaticamente, por meio de propriedades de conexão (em vez de confiar no provedor padrão gerado por SPNs), considere os seguintes fatores:  
  
-   Segurança: o SPN especificado divulga informações que estão protegidas?  
  
-   Confiabilidade: para permitir o uso de SPNs padrão, a conta de serviço na qual a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é executada precisa ter privilégios suficientes para atualizar o Active Directory no KDC.  
  
-   Conveniência e transparência de local: como os SPNs de um aplicativo serão afetados se seu banco de dados for movido para uma instância diferente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ? Isto se aplicará ao servidor principal e seu parceiro de failover se você usar espelhamento de banco de dados. Se uma alteração de servidor significar que os SPNs devem ser alterados, como isto afetará os aplicativos? Qualquer alteração será gerenciada?  
  
## <a name="specifying-the-spn"></a>Especificando o SPN  
 Você pode especificar um SPN em caixas de diálogo e em código. Esta seção discute como você pode especificar um SPN.  
  
 O tamanho máximo de um SPN é 260 caracteres.  
  
 A sintaxe que os SPNs usam em cadeia de conexão ou atributos de conexão é a seguinte:  
  
|Sintaxe|Descrição|  
|------------|-----------------|  
|MSSQLSvc/*fqdn*|O SPN padrão gerado pelo provedor para uma instância padrão quando um protocolo diferente de TCP é usado.<br /><br /> *fqdn* é um nome de domínio totalmente qualificado.|  
|MSSQLSvc/*fqdn:**porta*|O SPN padrão gerado pelo provedor quando o protocolo TCP é usado.<br /><br /> *port* é um número de porta TCP.|  
|MSSQLSvc/*fqdn*:*InstanceName*|O SPN padrão gerado pelo provedor para uma instância nomeada quando um protocolo diferente de TCP é usado.<br /><br /> *InstanceName* é um nome de instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|HOST/*fqdn*<br /><br /> HOST/*MachineName*|O SPN que mapeia para contas internas do computador que são automaticamente registradas pelo Windows.|  
|*Username*@*Domínio* de nome de usuário|Especificação direta de uma conta de domínio.<br /><br /> *Username* é um nome de conta de usuário do Windows.<br /><br /> *Domain* é um nome de domínio ou nome de domínio totalmente qualificado do Windows.|  
|*MachineName*$@*Domínio* machinename|Especificação direta de uma conta de computador.<br /><br /> (Se o servidor ao que você está se conectando estiver sendo executado `ServerSPN` em contas LOCAL SYSTEM ou NETWORK SERVICE, para obter a autenticação do Kerberos, pode estar no formato *MachineName*$@*Domain.)*|  
|*KDCKey*/*MachineName*|Um SPN especificado pelo usuário.<br /><br /> *KDCKey* é uma cadeia de caracteres alfanumérica que está em conformidade com as regras para uma chave do KDC.|  
  
## <a name="odbc-and-ole-db-syntax-supporting-spns"></a>Sintaxe do ODBC e OLE DB que dão suporte a SPNs  
 Para informações específicas de sintaxe, consulte os seguintes tópicos:  
  
-   [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;ODBC&#41;](../odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;OLE DB&#41;](../ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, consulte [Exemplos de programabilidade de dados do SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
