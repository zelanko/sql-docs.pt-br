---
title: MSSQLSERVER_208 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 208 (Database Engine error)
ms.assetid: 4b1895f5-3197-4da1-af86-954c93507956
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d28505b8f83d619171c83bf452a817a56efbd612
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver208"></a>MSSQLSERVER_208
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|208|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQ_BADOBJECT|  
|Texto da mensagem|Nome de objeto '%.*ls' inválido.|  
  
## <a name="explanation"></a>Explicação  
O objeto especificado não foi encontrado.  
  
### <a name="possible-causes"></a>Causas possíveis  
Esse erro pode ser causado por um dos seguintes problemas:  
  
-   O objeto não foi especificado corretamente.  
  
-   O objeto não existe no banco de dados atual ou no banco de dados especificado.  
  
-   O objeto existe, mas não pôde ser exposto ao usuário. Por exemplo, o usuário pode não ter as permissões no objeto ou talvez o objeto foi criado em uma instrução EXECUTE, mas acessado fora dela.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique as informações a seguir e corrija a instrução conforme apropriado.  
  
-   O nome do objeto foi digitado corretamente.  
  
-   O contexto do banco de dados atual está correto. Se um nome de banco de dados não for especificado para o objeto, este deverá existir no banco de dados atual. Para obter mais informações sobre como definir o contexto do banco de dados, consulte [USE &#40;Transact-SQL&#41;](~/t-sql/language-elements/use-transact-sql.md).  
  
-   O objeto existe nas tabelas do sistema. Para verificar se uma tabela ou outro objeto no escopo do esquema existe, consulte a exibição do catálogo **sys.objects**. Se o objeto não estiver nas tabelas do sistema, isso indica que ele foi excluído ou que o usuário não tem permissão para exibir metadados do objeto. Para obter mais informações sobre as permissões para exibir metadados de objeto, consulte [Configuração de visibilidade de metadados](~/relational-databases/security/metadata-visibility-configuration.md).  
  
-   O objeto está contido no esquema padrão do usuário. Se ele não estiver, o objeto deverá ser especificado no formato de duas partes *schema_name.object_name*. Observe que as funções com valor escalar sempre devem ser chamadas usando-se pelo menos um nome de duas partes.  
  
-   A diferenciação de maiúsculas e minúsculas do agrupamento de banco de dados.  
  
    Quando um banco de dados usa um agrupamento com diferenciação de maiúsculas e minúsculas, o nome do objeto deve corresponder ao uso de maiúsculas e minúsculas do objeto no banco de dados. Por exemplo, quando um objeto for especificado como **MyTable** em um banco de dados com um agrupamento com diferenciação de maiúsculas e minúsculas, as consultas que fizerem referência ao objeto como **mytable** ou **Mytable** retornarão o erro 208, pois os nomes dos objetos não são correspondentes.  
  
    Você pode verificar o agrupamento de banco de dados executando a instrução a seguir.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    A abreviação CS no nome do agrupamento indica que ele diferencia maiúsculas de minúsculas. Por exemplo, Latin1_General_CS_AS é um agrupamento que tem diferenciação de maiúsculas e minúsculas e também de acentos. CI indica um agrupamento sem diferenciação de maiúsculas e minúsculas.  
  
-   O usuário tem permissão para acessar o objeto. Para verificar as permissões do usuário no objeto, use a função de sistema **Has_Perms_By_Name**.  
  
## <a name="see-also"></a>Consulte Também  
[USE &#40;Transact-SQL&#41;](~/t-sql/language-elements/use-transact-sql.md)  
[Configuração de visibilidade de metadados](~/relational-databases/security/metadata-visibility-configuration.md)  
[HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](~/t-sql/functions/has-perms-by-name-transact-sql.md)  
  
