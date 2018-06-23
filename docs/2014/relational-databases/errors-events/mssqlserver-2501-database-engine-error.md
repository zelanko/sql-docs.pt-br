---
title: MSSQLSERVER_2501 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1d6e9f16e00684f0a55682b69e4c2d89d0dd552e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116602"
---
# <a name="mssqlserver2501"></a>MSSQLSERVER_2501
    
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
  
-   Verifique se o contexto do banco de dados atual está correto. Para obter mais informações, veja [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
-   Verifique se o nome da tabela ou do objeto foi digitado corretamente.  
  
-   Verifique o nome do esquema que contém o objeto. Se o objeto pertencer a um esquema diferente do esquema padrão (**dbo**), você deverá especificar o nome da tabela ou do objeto usando o formato de duas partes *schema_name.object_name*.  
  
-   Verifique se o objeto existe nas tabelas do sistema. Para verificar se uma tabela ou outro objeto no escopo do esquema existe, consulte a exibição do catálogo [sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql). Se o objeto não estiver nas tabelas do sistema, isso indica que ele foi excluído ou que o usuário não tem permissão para exibir metadados do objeto. Para obter mais informações sobre como exibir metadados de objeto, consulte [Configuração de visibilidade de metadados](../security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)  
  
  
