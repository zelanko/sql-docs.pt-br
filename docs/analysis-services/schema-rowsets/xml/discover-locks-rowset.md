---
title: Conjunto de linhas DISCOVER_LOCKS | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_LOCKS rowset
ms.assetid: dea48167-212c-40b7-a416-434042a1b697
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d50a6cb0bdc6bfdb27fdbfff4c79b25c43e27e58
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverlocks-rowset"></a>Conjunto de linhas DISCOVER_LOCKS
  Oferece informações sobre os bloqueios atuais no servidor.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_LOCKS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LOCK_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||A hora do servidor UTC no momento em que o bloqueio foi solicitado.|  
|**LOCK_GRANT_TIME**|**DBTYPE_DBTIMESTAMP**||A hora do servidor UTC no momento em que o bloqueio foi concedido no recurso.|  
|**LOCK_ID**|**DBTYPE_GUID**||O identificador exclusivo do bloqueio, como um GUID.|  
|**LOCK_OBJECT_ID**|**DBTYPE_WSTR**||O identificador exclusivo do objeto bloqueado.|  
|**LOCK_STATUS**|**DBTYPE_I4**||O estado de bloqueio.<br /><br /> 0 significa "Aguardando para bloquear o objeto".<br /><br /> 1 significa "Bloqueio Concedido".|  
|**LOCK_TRANSACTION_ID**|**DBTYPE_GUID**||O identificador exclusivo da transação, como um GUID.|  
|**LOCK_TYPE**|**DBTYPE_I4**||Uma máscara de bits de Tipos de Bloqueio; para obter mais informações, consulte a seção Comentários deste tópico.|  
|**SPID**|**DBTYPE_I4**||A ID da sessão.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_LOCKS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|Opcional.|  
|LOCK_TRANSACTION_ID|DBTYPE_GUID|Opcional.|  
|LOCK_OBJECT_ID|DBTYPE_WSTR|Opcional.|  
|LOCK_STATUS|DBTYPE_I4|Opcional.|  
|LOCK_TYPE|DBTYPE_I4|Opcional.|  
|LOCK_MIN_TOTAL_MS|DBTYPE_I8|Opcional.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="lock-types"></a>Tipos de bloqueio  
  
|Nome do bloqueio|Valor|Descrição|  
|---------------|-----------|-----------------|  
|LOCK_NONE|0x0000000|Nenhum bloqueio.|  
|LOCK_SESSION_LOCK|0x0000001|Sessão inativa; não interfere em outros bloqueios.|  
|LOCK_READ|0x0000002|Bloqueio de leitura durante processamento.|  
|LOCK_WRITE|0x0000004|Bloqueio de gravação durante processamento.|  
|LOCK_COMMIT_READ|0x0000008|Bloqueio de confirmação, compartilhado.|  
|LOCK_COMMIT_WRITE|0x0000010|Bloqueio de confirmação, exclusivo.|  
|LOCK_COMMIT_ABORTABLE|0x0000020|Anular no andamento de confirmação.|  
|LOCK_COMMIT_INPROGRESS|0x0000040|Confirmação em andamento.|  
|LOCK_INVALID|0x0000080|Bloqueio inválido.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

