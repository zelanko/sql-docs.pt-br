---
title: Trabalhando com isolamento de instantâneo | Microsoft Docs
description: Trabalhar com isolamento de instantâneo no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], snapshot isolation
- MSOLEDBSQL, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, snapshot isolation
- SQLGetInfo function
- concurrency [OLE DB Driver for SQL Server]
- SQLSetConnectAttr function
author: pmasl
ms.author: pelopes
ms.openlocfilehash: acbb39726ede983d3c0909235d1fb2ddb588d65b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85986434"
---
# <a name="working-with-snapshot-isolation"></a>Trabalhando com isolamento de instantâneo
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu um novo nível de isolamento de "instantâneo" cujo objeto é aumentar a simultaneidade para aplicativos OLTP (online transaction processing). Nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a simultaneidade baseava-se apenas no bloqueio, o que pode causar problemas de bloqueio e de deadlock em alguns aplicativos. O isolamento de instantâneo depende de aprimoramentos no controle de versão de linha e seu objetivo é melhorar o desempenho evitando cenários de bloqueio de leitor/gravador.  
  
 As transações que iniciam com o isolamento de instantâneo leem um instantâneo de banco de dados a partir da hora em que a transação inicia. Os cursores de servidor de conjunto de chaves, dinâmicos e estáticos, abertos em um contexto de transação de instantâneo, comportam-se como os cursores estáticos que foram abertos em transações serializáveis. Porém, quando os cursores são abertos com o nível de isolamento de instantâneo os bloqueios não são considerados. Esse fato pode reduzir o bloqueio no servidor.  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server  
 O Driver do OLE DB para SQL Server tem aprimoramentos que aproveitam o isolamento de instantâneo introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Esses aprimoramentos incluem alterações aos conjuntos de propriedades DBPROPSET_DATASOURCEINFO e DBPROPSET_SESSION.  
  
### <a name="dbpropset_datasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 O conjunto de propriedades DBPROPSET_DATASOURCEINFO tem sido alterado para indicar que o nível de isolamento de instantâneo é suportado pela adição do valor DBPROPVAL_TI_SNAPSHOT usado na propriedade DBPROP_SUPPORTEDTXNISOLEVELS. Esse novo valor indica que haverá suporte para o nível de isolamento do instantâneo se o controle de versão tiver sido ou não habilitado no banco de dados. A seguinte tabela lista os valores de DBPROP_SUPPORTEDTXNISOLEVELS:  
  
|ID da propriedade|DESCRIÇÃO|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Tipo: VT_I4<br /><br /> R/W: somente leitura<br /><br /> Descrição: Um bitmask que especifica os níveis de isolamento da transação com suporte. Uma combinação de zeros ou mais do seguinte:<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropset_session"></a>DBPROPSET_SESSION  
 O conjunto de propriedades DBPROPSET_SESSION tem sido alterado para indicar que o nível de isolamento de instantâneo é suportado pela adição do valor DBPROPVAL_TI_SNAPSHOT usado na propriedade DBPROP_SESS_AUTOCOMMITISOLEVELS. Esse novo valor indica que haverá suporte para o nível de isolamento do instantâneo se o controle de versão tiver sido ou não habilitado no banco de dados. A seguinte tabela lista os valores de DBPROP_SESS_AUTOCOMMITISOLEVELS:
  
|ID da propriedade|DESCRIÇÃO|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Tipo: VT_I4<br /><br /> R/W: somente leitura<br /><br /> Descrição: Especifica um bitmask que indica o nível de isolamento da transação enquanto estiver no modo de confirmação automática. Os valores que podem ser definidos nesse bitmask são os mesmos valores que podem ser definidos para DBPROP_SUPPORTEDTXNISOLEVELS.|  
  
> [!NOTE]  
>  Os erros DB_S_ERRORSOCCURRED ou DB_E_ERRORSOCCURRED ocorrerão se DBPROPVAL_TI_SNAPSHOT for definido durante o uso de versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obter informações sobre o suporte ao isolamento de instantâneo em transações, confira [Suporte a transações locais](../../oledb/ole-db-transactions/supporting-local-transactions.md).  

  
## <a name="see-also"></a>Consulte Também  
 [Recursos do OLE DB Driver for SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [Propriedades e comportamentos do conjunto de linhas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
