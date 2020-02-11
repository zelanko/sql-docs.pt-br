---
title: sys. resource_usage (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_usage_TSQL
- resource_usage
- sys.resource_usage
- resource_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- resource_usage
- sys.resource_usage
ms.assetid: b90147a3-fd8e-408e-961d-5c7000e068ad
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 3be4ff07923759af53b929852d4dbaa4088a77f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67904428"
---
# <a name="sysresource_usage-azure-sql-database"></a>sys.resource_usage (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]
>  Esse recurso está em um estado de visualização. Não usa uma dependência na implementação específica desse recurso porque o recurso pode ser alterado ou removido em uma versão futura.  
> 
>  Quando está em um estado de visualização, a equipe de operações do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] pode ativar ou desativar a coleta de dados para esse DMV:  
> 
>  -   Quando ativado, o DMV retorna dados atuais à medida que são agregados.  
> -   Quando desativado, o DMV retorna os dados históricos, que podem estar obsoletos.  
  
 Fornece um resumo de hora em hora de dados de uso de recurso para bancos de dados de usuário no servidor atual. Os dados históricos são mantidos por 90 dias.  
  
 Para cada banco de dados de usuário, há uma linha para cada hora na forma contínua. Mesmo se o banco de dados estiver ocioso durante aquela hora, há uma linha, e o valor de usage_in_seconds para esse banco de dados será 0. O uso de armazenamento e as informações de SKU são acumuladas para a hora adequadamente.  
  
|Colunas|Tipo de Dados|DESCRIÇÃO|  
|-------------|---------------|-----------------|  
|time|**datetime**|A hora (UTC) em incrementos de hora.|  
|database_name|**nvarchar**|Nome do banco de dados de usuário.|  
|sku|**nvarchar**|O nome da SKU. O valores possíveis são os seguintes:<br /><br /> Web<br /><br /> Negócios<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|Soma do tempo de CPU usado na hora.<br /><br /> Observação: esta coluna foi preterida para v11 e não se aplica ao V12. **O valor é sempre definido como 0.**|  
|storage_in_megabytes|**decimal**|Tamanho máximo de armazenamento para a hora, inclusive dados do banco de dados, índices, procedimentos armazenados e metadados.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao banco de dados **mestre** virtual.  
  
  
