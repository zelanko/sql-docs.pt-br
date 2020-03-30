---
title: MSSQLSERVER_208 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 208 (Database Engine error)
ms.assetid: 4b1895f5-3197-4da1-af86-954c93507956
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a1b39638bf7ac09cac4a37d948ba13753ffb6d04
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68056812"
---
# <a name="mssqlserver_208"></a>MSSQLSERVER_208
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|208|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQ_BADOBJECT|  
|Texto da mensagem|Nome de objeto '%.*ls' inválido.|  
  
## <a name="explanation"></a>Explicação  
O objeto especificado não foi encontrado.  
  
### <a name="possible-causes"></a>Possíveis causas  
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
  
-   A diferenciação de maiúsculas e minúsculas da ordenação de banco de dados.  
  
    Quando um banco de dados usa uma ordenação com diferenciação de maiúsculas e minúsculas, o nome do objeto deve corresponder ao uso de maiúsculas e minúsculas do objeto no banco de dados. Por exemplo, quando um objeto for especificado como **MyTable** em um banco de dados com uma ordenação com diferenciação de maiúsculas e minúsculas, as consultas que fizerem referência ao objeto como **mytable** ou **Mytable** retornarão o erro 208, pois os nomes dos objetos não são correspondentes.  
  
    Você pode verificar a ordenação de banco de dados executando a instrução a seguir.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    A abreviação CS no nome da ordenação indica que ela diferencia maiúsculas de minúsculas. Por exemplo, Latin1_General_CS_AS é uma ordenação que tem diferenciação de maiúsculas e minúsculas e também de acentos. CI indica uma ordenação sem diferenciação de maiúsculas e minúsculas.  
  
-   O usuário tem permissão para acessar o objeto. Para verificar as permissões do usuário no objeto, use a função de sistema **Has_Perms_By_Name**.  
  
## <a name="see-also"></a>Consulte Também  
[USE &#40;Transact-SQL&#41;](~/t-sql/language-elements/use-transact-sql.md)  
[Configuração de visibilidade de metadados](~/relational-databases/security/metadata-visibility-configuration.md)  
[HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](~/t-sql/functions/has-perms-by-name-transact-sql.md)  
  
