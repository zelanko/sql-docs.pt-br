---
title: sysssispackages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackages90_TSQL
- sysdtspackages90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackages system table
ms.assetid: 66155dcd-dcdb-4e33-a242-1625828ad8d2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e400905801f3186f2eb54956bad612c17d686d14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757747"
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada pacote que é salvo em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa tabela é armazenada no banco de dados **msdb** .  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O identificador exclusivo do pacote.|  
|**id**|**uniqueidentifier**|O GUID do pacote.|  
|**ndescrição**|**nvarchar**|A descrição opcional do pacote.|  
|**CreateDate**|**datetime**|A data em que o pacote foi criado.|  
|**FolderId**|**uniqueidentifier**|O GUID da pasta lógica na qual o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] lista o pacote.|  
|**ownersid**|**varbinary**|O identificador de segurança exclusivo do usuário que criou o pacote.|  
|**packagedata**|**imagem**|O pacote.|  
|**packageformat**|**int**|O formato em que o pacote foi salvo:<br /><br /> Um valor de 2 indica que o pacote foi salvo no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] formato.<br /><br /> Um valor de 3 indica que o pacote é salvo no formato do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou posterior.|  
|**PackageType**|**int**|O cliente que criou o pacote. Os valores possíveis são os seguintes:<br /><br /> 0 (valor padrão)<br /><br /> 1 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de importação e exportação)<br /><br /> 3 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] replicação)<br /><br /> 5 ( [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer)<br /><br /> 6 (Assistente ou Designer do Plano de Manutenção).<br /><br /> <br /><br /> Observe que os valores nesta coluna correspondem à <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType> enumeração.|  
|**vermajor**|**int**|A versão principal mais recente do pacote.|  
|**verminor**|**int**|A versão secundária mais recente do pacote.|  
|**verbuild**|**int**|O versão mais recente do pacote.|  
|**vercomments**|**nvarchar**|Comentários sobre a versão do pacote.|  
|**verid**|**uniqueidentifier**|O GUID da versão do pacote.|  
|**IsEncrypted**|**bit**|Um booliano que indica se o pacote é criptografado.|  
|**readrolesid**|**varbinary**|A função [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pode carregar pacotes.|  
|**writerolesid**|**varbinary**|A função [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pode salvar pacotes.|  
  
## <a name="see-also"></a>Consulte Também  
 [Pacotes do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)  
  
  
