---
title: sys. sysfiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a3554e254be0623e36719fe76b2d811908a939d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053471"
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada arquivo em um banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**FileID**|**smallint**|Número de identificação do arquivo exclusivo para cada banco de dados.|  
|**GroupId**|**smallint**|Número de identificação do grupo de arquivos.|  
|**tamanho**|**int**|Tamanho do arquivo, em páginas de 8 KB.|  
|**MaxSize**|**int**|Tamanho de arquivo máximo, em páginas de 8 KB.<br /><br /> 0 = Sem crescimento.<br /><br /> -1 = Arquivo crescerá até que o disco esteja completo.<br /><br /> 268435456 = Arquivo de log crescerá a um tamanho máximo de 2 TB.<br /><br /> Observação: os bancos de dados que são atualizados com um tamanho de arquivo de log ilimitado relatarão-1 para o tamanho máximo do arquivo de log.|  
|**growth**|**int**|Tamanho de crescimento do banco de dados. Pode ser o número de páginas ou a porcentagem do tamanho do arquivo, dependendo do valor do **status**.<br /><br /> 0 = Sem crescimento.|  
|**Estado**|**int**|Bits de status para o valor de **crescimento** em megabytes (MB) ou quilobytes (KB).<br /><br /> 0x2 = Arquivo de disco.<br /><br /> 0x40 = Arquivo de log<br /><br /> 0x100000 = Crescimento. Este valor é uma porcentagem e não o número de páginas.|  
|**perf**|**int**|Reservado.|  
|**name**|**sysname**|Nome lógico do arquivo.|  
|**nome do arquivo**|**nvarchar(260)**|Nome do dispositivo físico. Isso inclui o caminho completo do arquivo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;&#41;Transact-SQL](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
