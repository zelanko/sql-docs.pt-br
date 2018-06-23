---
title: Esquema de FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8515d78ddab2dd39e223087a44b0e021a5aca439
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130789"
---
# <a name="filetable-schema"></a>Esquema da FileTable
  Descreve o esquema predefinido e fixo de uma FileTable.  
  
|Nome do atributo do arquivo|Tipo|Tamanho|Padrão|Description|Acessibilidade do sistema de arquivos|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|`hierarchyid`|variável|Um `hierarchyid` que identifica a posição desse item.|A posição deste nó no FileNamespace hierárquico.<br /><br /> Chave primária da tabela.|Pode ser criada e modificada por meio da definição de valores de caminho do Windows.|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||Um valor retornado pelo `NEWID()` função.|Uma ID exclusiva para os dados FILESTREAM.|Não aplicável.|  
|**file_stream**|`varbinary(max)`<br /><br /> `filestream`|variável|NULL|Contém os dados de FILESTREAM.|Não aplicável.|  
|**file_type**|`nvarchar(255)`|variável|NULL.<br /><br /> Uma operação de criação e renomeação no sistema de arquivos popula o valor da extensão do arquivo a partir do nome.|Representa o tipo do arquivo.<br /><br /> Essa coluna pode ser usada como `TYPE COLUMN` para criar um índice de texto completo.<br /><br /> **file_type** é uma coluna computada persistente.|Calculado automaticamente. Não pode ser definido.|  
|**Nome**|`nvarchar(255)`|variável|Valor do GUID.|O nome do arquivo ou do diretório.|Pode ser criado ou modificado por meio de APIs do Windows.|  
|**parent_path_locator**|`hierarchyid`|variável|Um `hierarchyid` que identifica o diretório que contém esse item.|O `hierarchyid` do diretório que contém.<br /><br /> **parent_path_locator** é uma coluna computada persistente.|Calculado automaticamente. Não pode ser definido.|  
|**cached_file_size**|`bigint`|||O tamanho em bytes dos dados FILESTREAM.<br /><br /> **cached_file_size** é uma coluna computada persistente.|Embora o tamanho de arquivo armazenado em cache seja mantido atualizado automaticamente, ele pode ficar fora de sincronia em circunstâncias incomuns. Para calcular o tamanho exato, use o `DATALENGTH()` função.|  
|**creation_time**|`datetime2(4)`<br /><br /> `not null`|8 bytes|Hora atual.|A data e a hora em que o arquivo foi criado.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**last_write_time**|`datetime2(4)`<br /><br /> `not null`|8 bytes|Hora atual.|Data e hora em que o arquivo foi atualizado pela última vez.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**last_access_time**|`datetime2(4)`<br /><br /> `not null`|8 bytes|Hora atual.|Data e hora em que o arquivo foi acessado pela última vez.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_directory**|`bit`<br /><br /> `not null`|1 byte|FALSE|Indica se a linha representa um diretório. Esse valor é calculado automaticamente e não pode ser definido.|Calculado automaticamente. Não pode ser definido.|  
|**is_offline**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de arquivo offline.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_hidden**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de arquivo oculto.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_readonly**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de arquivo somente leitura.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_archive**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de arquivo morto.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_system**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de arquivo do sistema.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_temporary**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de arquivo temporário.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar, alterar e remover FileTables](create-alter-and-drop-filetables.md)  
  
  