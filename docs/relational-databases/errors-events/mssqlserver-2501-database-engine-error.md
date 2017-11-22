---
title: MSSQLSERVER_2501 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7583ceb06b4120b3f2d806c51ecba4998e8d54f5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2501"></a>MSSQLSERVER_2501
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2501|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_NO_SUCH_TABLE_NAME|  
|Texto da mensagem|Não foi possível encontrar uma tabela ou um objeto com o nome 'NAME'. Verifique o catálogo do sistema.|  
  
## <a name="explanation"></a>Explicação  
O objeto especificado não foi encontrado.  
  
### <a name="possible-causes"></a>Causas possíveis  
Esse erro pode ser causado por um dos seguintes problemas:  
  
-   O objeto não foi especificado corretamente.  
  
-   O objeto não existe ou foi descartado antes que uma instrução tentasse utilizá-lo.  
  
-   Talvez o objeto exista, mas não foi possível expô-lo para o usuário. Por exemplo, talvez o usuário não tenha permissões no objeto ou o objeto é uma tabela interna que não pôde ser vista pelo usuário.  
  
## <a name="user-action"></a>Ação do usuário  
  
-   Verifique se o contexto do banco de dados atual está correto. Para obter mais informações, veja [USE &#40;Transact-SQL&#41;](~/t-sql/language-elements/use-transact-sql.md).  
  
-   Verifique se o nome da tabela ou do objeto foi digitado corretamente.  
  
-   Verifique o nome do esquema que contém o objeto. Se o objeto pertencer a um esquema diferente do esquema padrão (**dbo**), você deverá especificar o nome da tabela ou do objeto usando o formato de duas partes *schema_name.object_name*.  
  
-   Verifique se o objeto existe nas tabelas do sistema. Para verificar se uma tabela ou outro objeto no escopo do esquema existe, consulte a exibição do catálogo [sys.objects](~/relational-databases/system-catalog-views/sys-objects-transact-sql.md). Se o objeto não estiver nas tabelas do sistema, isso indica que ele foi excluído ou que o usuário não tem permissão para exibir metadados do objeto. Para obter mais informações sobre como exibir metadados de objeto, consulte [Configuração de visibilidade de metadados](~/relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
[Exibições de catálogo &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
