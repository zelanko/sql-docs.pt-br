---
title: MSSQLSERVER_2501 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f80ee71b0a85dc41b006d5ba6dc003a362d078bc
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553341"
---
# <a name="mssqlserver_2501"></a>MSSQLSERVER_2501
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|2501|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_NO_SUCH_TABLE_NAME|  
|Texto da mensagem|Não foi possível encontrar uma tabela ou um objeto com o nome 'NAME'. Verifique o catálogo do sistema.|  
  
## <a name="explanation"></a>Explicação  
 O objeto especificado não foi encontrado.  
  
### <a name="possible-causes"></a>Possíveis causas  
 Esse erro pode ser causado por um dos seguintes problemas:  
  
-   O objeto não foi especificado corretamente.  
  
-   O objeto não existe ou foi descartado antes que uma instrução tentasse utilizá-lo.  
  
-   Talvez o objeto exista, mas não foi possível expô-lo para o usuário. Por exemplo, talvez o usuário não tenha permissões no objeto ou o objeto é uma tabela interna que não pôde ser vista pelo usuário.  
  
## <a name="user-action"></a>Ação do usuário  
  
-   Verifique se o contexto do banco de dados atual está correto. Para obter mais informações, veja [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
-   Verifique se o nome da tabela ou do objeto foi digitado corretamente.  
  
-   Verifique o nome do esquema que contém o objeto. Se o objeto pertencer a um esquema diferente do esquema padrão (**dbo**), você deverá especificar o nome da tabela ou do objeto usando o formato de duas partes *schema_name.object_name*.  
  
-   Verifique se o objeto existe nas tabelas do sistema. Para verificar se uma tabela ou outro objeto no escopo do esquema existe, consulte a exibição do catálogo [sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql). Se o objeto não estiver nas tabelas do sistema, isso indica que ele foi excluído ou que o usuário não tem permissão para exibir metadados do objeto. Para obter mais informações sobre como exibir metadados de objeto, consulte [Configuração de visibilidade de metadados](../security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)  
  
  
