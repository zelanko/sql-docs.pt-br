---
title: Trabalhando com isolamento de instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], snapshot isolation
- SQLNCLI, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, snapshot isolation
- SQL Server Native Client ODBC driver, snapshot isolation
- SQL Server Native Client, snapshot isolation
- SQLGetInfo function
- concurrency [SQL Server Native Client]
- SQLSetConnectAttr function
ms.assetid: 39e87eb1-677e-45dd-bc61-83a4025a7756
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 502c36c0d4793a28cb3f9db631d9544ab8467bcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761270"
---
# <a name="working-with-snapshot-isolation"></a>Trabalhando com isolamento de instantâneo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu um novo nível de isolamento de "instantâneo" cujo objeto é aumentar a simultaneidade para aplicativos OLTP (online transaction processing). Nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a simultaneidade baseava-se apenas no bloqueio, o que pode causar problemas de bloqueio e de deadlock em alguns aplicativos. O isolamento de instantâneo depende de aprimoramentos no controle de versão de linha e seu objetivo é melhorar o desempenho evitando cenários de bloqueio de leitor/gravador.  
  
 As transações que iniciam com o isolamento de instantâneo leem um instantâneo de banco de dados a partir da hora em que a transação inicia. Um dos resultados é que os cursores de servidor de conjunto de chaves, dinâmicos e estáticos, quando abertos em um contexto de transação de instantâneo, comportam-se de modo semelhante aos cursores estáticos abertos em transações serializáveis. Porém, quando os cursores são abertos com o nível de isolamento de instantâneo os bloqueios não são considerados, o que pode reduzir o bloqueio no servidor.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo tem aprimoramentos que aproveitam o isolamento de instantâneo [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]introduzido no. Esses aprimoramentos incluem alterações aos conjuntos de propriedades DBPROPSET_DATASOURCEINFO e DBPROPSET_SESSION.  
  
### <a name="dbpropset_datasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 O conjunto de propriedades DBPROPSET_DATASOURCEINFO tem sido alterado para indicar que o nível de isolamento de instantâneo é suportado pela adição do valor DBPROPVAL_TI_SNAPSHOT usado na propriedade DBPROP_SUPPORTEDTXNISOLEVELS. Esse novo valor indica que haverá suporte para o nível de isolamento do instantâneo se o controle de versão tiver sido ou não habilitado no banco de dados. Esta é uma lista dos valores DBPROP_SUPPORTEDTXNISOLEVELS:  
  
|ID da propriedade|DESCRIÇÃO|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Tipo: VT_I4<br /><br /> R/W: somente leitura<br /><br /> Descrição: Um bitmask que especifica os níveis de isolamento da transação com suporte. Uma combinação de zeros ou mais do seguinte:<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropset_session"></a>DBPROPSET_SESSION  
 O conjunto de propriedades DBPROPSET_SESSION tem sido alterado para indicar que o nível de isolamento de instantâneo é suportado pela adição do valor DBPROPVAL_TI_SNAPSHOT usado na propriedade DBPROP_SESS_AUTOCOMMITISOLEVELS. Esse novo valor indica que haverá suporte para o nível de isolamento do instantâneo se o controle de versão tiver sido ou não habilitado no banco de dados. Esta é uma lista dos valores DBPROP_SESS_AUTOCOMMITISOLEVELS:  
  
|ID da propriedade|DESCRIÇÃO|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Tipo: VT_I4<br /><br /> R/W: somente leitura<br /><br /> Descrição: Especifica um bitmask que indica o nível de isolamento da transação enquanto estiver no modo de confirmação automática. Os valores que podem ser definidos nesse bitmask são os mesmos que podem ser definidos para DBPROP_SUPPORTEDTXNISOLEVELS.|  
  
> [!NOTE]  
>  Os erros DB_S_ERRORSOCCURRED ou DB_E_ERRORSOCCURRED ocorrerão se DBPROPVAL_TI_SNAPSHOT for definido durante o uso de versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obter informações sobre como o isolamento de instantâneo tem suporte em transações, consulte [dando suporte a transações locais](../../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client fornece suporte para isolamento de instantâneos, por meio de aprimoramentos feitos nas funções [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) .  
  
### <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 A função **SQLSetConnectAttr** agora dá suporte ao uso do atributo SQL_COPT_SS_TXN_ISOLATION. Configurar SQL_COPT_SS_TXN_ISOLATION como SQL_TXN_SS_SNAPSHOT indica que a transação ocorrerá no nível de isolamento do instantâneo.  
  
### <a name="sqlgetinfo"></a>SQLGetInfo  
 A função [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) agora dá suporte ao valor SQL_TXN_SS_SNAPSHOT que foi adicionado ao tipo de informações SQL_TXN_ISOLATION_OPTION.  
  
 Para obter informações sobre como o isolamento de instantâneo tem suporte em transações, consulte [cursor TRANSACTION ISOLATION LEVEL](../../../relational-databases/native-client-odbc-cursors/properties/cursor-transaction-isolation-level.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Propriedades e comportamentos do conjunto de linhas](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
