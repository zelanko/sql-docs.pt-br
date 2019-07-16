---
title: sys. sysaltfiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysaltfiles_TSQL
- sys.sysaltfiles
- sysaltfiles_TSQL
- sysaltfiles
dev_langs:
- TSQL
helpviewer_keywords:
- sysaltfiles system table
- sys.sysaltfiles compatibility view
ms.assetid: 698dec23-5336-4108-87a5-f8e407f8da09
author: rothja
ms.author: jroth
ms.openlocfilehash: 891e88761cac47be83fb69debbbc5e4cb6c401c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006964"
---
# <a name="syssysaltfiles-transact-sql"></a>sys.sysaltfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Em circunstâncias especiais, contém linhas que correspondem aos arquivos em um banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|Número de identificação do arquivo. Esse número é exclusivo para cada banco de dados.|  
|**groupid**|**smallint**|Número de identificação do grupo de arquivos.|  
|**size**|**int**|Tamanho do arquivo, em páginas de 8 kilobytes (KB).|  
|**maxsize**|**int**|Tamanho de arquivo máximo, em páginas de 8 KB.<br /><br /> 0 = Sem crescimento.<br /><br /> -1 = Arquivo crescerá até que o disco esteja completo.<br /><br /> 268435456 = Arquivo de log crescerá a um tamanho máximo de 2 TB.<br /><br /> Observação: Bancos de dados que são atualizados com um tamanho de arquivo de log ilimitado informarão -1 para o tamanho máximo do arquivo de log.|  
|**growth**|**int**|Tamanho de crescimento do banco de dados.<br /><br /> 0 = Sem crescimento. Pode ser o número de páginas ou a porcentagem do tamanho de arquivo, dependendo do valor de status. Se **status** for 0x100000, **crescimento** é a porcentagem do arquivo tamanho; caso contrário, ele é o número de páginas.|  
|**status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**perf**|**int**|Reservado.|  
|**dbid**|**smallint**|Número de identificação do banco de dados ao qual este arquivo pertence.|  
|**name**|**sysname**|Nome lógico do arquivo.|  
|**filename**|**nvarchar(260)**|Nome do dispositivo físico. Isso inclui o caminho completo do arquivo.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
