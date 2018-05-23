---
title: MSSQLSERVER_605 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 605 (Database Engine error)
ms.assetid: d8d3a22e-1ff8-48a4-891f-4c8619437e24
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0e6fe4b98cd7db3aceac8f8b455ced2c072673f1
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver605"></a>MSSQLSERVER_605
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|605|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|WRONGPAGE|  
|Texto da mensagem|Falha na tentativa de buscar a página lógica %S_PGID no banco de dados %d. Ela pertence à unidade de alocação %I64d não a %I64d.|  
  
## <a name="explanation"></a>Explicação  
Esse erro geralmente indica um dano na página ou na alocação do banco de dados especificado. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta danos quando lê páginas que pertencem a uma tabela, seguindo os vínculos de página ou usando a página IAM. Todas as páginas alocadas para uma tabela devem pertencer a uma das unidades de alocação associadas à tabela. Se a ID da unidade de alocação contida no cabeçalho da página não corresponder a uma ID de unidade de alocação associada à tabela, essa exceção será gerada. A primeira ID de unidade de alocação listada na mensagem de erro é a ID presente no cabeçalho da página, e o segundo valor da unidade de alocação é a ID associada com a tabela.  
  
**Erros de dados corrompidos**  
  
Um nível de gravidade 21 indica a possibilidade de os dados estarem corrompidos. As possíveis causas são uma cadeia de páginas danificada, uma página IAM corrompida ou uma entrada inválida na exibição de catálogo [sys.objects](~/relational-databases/system-catalog-views/sys-objects-transact-sql.md) do objeto em questão. Esses erros geralmente são causados por falha de hardware ou do driver de dispositivo do disco.  
  
**Erros transitórios**  
  
Um nível de gravidade 12 indica um possível erro transitório; ou seja, ele ocorre no cache e não indica dano nos dados armazenados em disco. Os erros transitórios 605 podem ser causados pelas seguintes condições:  
  
-   O sistema operacional prematuramente notifica o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de que uma operação de E/S foi concluída; a mensagem de erro é exibida mesmo que os dados não estejam corrompidos.  
  
Executar uma consulta com a dica de otimização NOLOCK ou definir o nível de isolamento da transação como READ UNCOMMITTED. Quando uma consulta que não usa NOLOCK ou READ UNCOMMITTED tenta ler dados que estão sendo movidos ou alterados por outro usuário, ocorre um erro 605. Para verificar se é um erro 605 transitório, reexecute a consulta posteriormente. Para obter mais informações, consulte o artigo [235880](http://support.microsoft.com/kb/235880/en-us) da Base de Dados de Conhecimento: “Você recebe uma mensagem de erro "Erro 605" quando executa uma consulta com a dica de otimização NOLOCK ou define o nível de isolamento da transação como READ UNCOMMITTED no SQL Server”.  
  
Em geral, se o erro ocorreu durante o acesso aos dados, mas as operações DBCC CHECKDB subsequentes foram concluídas com êxito, provavelmente o erro 605 era transitório.  
  
## <a name="user-action"></a>Ação do usuário  
Se o erro 605 não é transitório, o problema é grave e deve ser corrigido por meio das seguintes tarefas:  
  
1.  Identifique as tabelas associadas com as unidades de alocação especificadas na mensagem executando a consulta a seguir. Substitua `allocation_unit_id` pelas unidades de alocação especificadas na mensagem de erro.  
  
    USE`database_name`;  
  
    GO  
  
    SELECT au.allocation_unit_id, OBJECT_NAME(p.object_id) AS table_name, fg.name AS filegroup_name,  
  
    au.type_desc AS allocation_type, au.data_pages, partition_number  
  
    FROM sys.allocation_units AS au  
  
    JOIN sys.partitions AS p ON au.container_id = p.partition_id  
  
    JOIN sys.filegroups AS fg ON fg.data_space_id = au.data_space_id  
  
    WHERE au.allocation_unit_id = `allocation_unit_id` OR au.allocation_unit_id = `allocation_unit_id`  
  
    ORDER BY au.allocation_unit_id;  
  
    GO  
  
2.  Execute DBCC CHECKTABLE sem uma cláusula REPAIR na tabela associada com a segunda ID de unidade de alocação especificada na mensagem de erro.  
  
3.  Execute DBCC CHECKDB sem uma cláusula REPAIR o mais rápido possível para determinar toda a extensão do dano causado no banco de dados inteiro.  
  
4.  Verifique no log de erros se existem outros erros que costumam acompanhar um erro 605 e examine o Log de Eventos do Windows para identificar problemas de sistema ou relacionados ao hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se o problema não estiver relacionado ao hardware, execute uma das seguintes tarefas:  
  
1.  Restaure o banco de dados de um backup limpo conhecido. Use o recurso de backup de restauração de página para restaurar somente as páginas danificadas.  
  
2.  Execute DBCC CHECKDB com a cláusula REPAIR recomendada pela operação DBCC CHECKDB executada na etapa 3 para reparar o dano. Se a execução de DBCC CHECKDB com uma das cláusulas REPAIR não corrigir o problema, contate seu provedor de suporte. Revise a saída gerada por DBCC CHECKDB.  
  
    > [!CAUTION]  
    > Se você não tiver certeza do efeito de DBCC CHECKDB com uma cláusula REPAIR sobre seus dados, contate o provedor de suporte antes de executar essa instrução.  
  
## <a name="see-also"></a>Consulte Também  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
  
