---
title: "Funções determinísticas e não determinísticas | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- built-in functions [SQL Server]
- nondeterministic functions
- extended stored procedures [SQL Server], functions that call
- deterministic functions
- user-defined functions [SQL Server], deterministic
ms.assetid: 2f3ce5f5-c81c-4470-8141-8144d4f218dd
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 2a25a75485ecfb5bae812b01f142a9650ce2933c
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="deterministic-and-nondeterministic-functions"></a>Funções determinísticas e não determinísticas
  As funções determinísticas sempre retornam o mesmo resultado quando são chamadas com o uso de um conjunto específico de valores de entrada e quando recebem o mesmo estado do banco de dados. As funções não determinísticas podem retornar resultados diferentes cada vez que são chamadas com um conjunto específico de valores de entrada, mesmo que o estado do banco de dados que elas acessam permaneça o mesmo. Por exemplo, a função AVG sempre retorna o mesmo resultado, dadas as qualificações declaradas acima, mas a função GETDATE, que retorna o valor datetime atual, sempre retorna um resultado diferente.  
  
 Há várias propriedades de funções definidas pelo usuário que determinam a capacidade do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] de indexar os resultados da função, tanto por meio de índices em colunas computadas que chamam a função como por meio de exibições indexadas que referenciam a função. O determinismo de uma função é uma dessas propriedades. Por exemplo, um índice clusterizado não poderá ser criado em uma exibição se ela referenciar qualquer função não determinística. Para obter mais informações sobre propriedades de funções, inclusive determinismo, consulte [Funções definidas pelo usuário](../../relational-databases/user-defined-functions/user-defined-functions.md).  
  
 Este tópico identifica o determinismo de funções de sistema internas e o efeito da propriedade determinística de funções definidas pelo usuário quando ela contém uma chamada para procedimentos armazenados estendidos.  
  
## <a name="built-in-function-determinism"></a>Determinismo de função interna  
 Você não pode influenciar o determinismo de nenhuma função interna. Cada função interna é determinística ou não determinística com base no modo como a função é implementada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, a especificação de uma cláusula ORDER BY em uma consulta não altera o determinismo de uma função usada nessa consulta.  
  
 Todas as funções internas de cadeia de caracteres são determinísticas. Para obter uma lista dessas funções, consulte [Funções de sequência de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md).  
  
 As seguintes funções internas pertencentes a categorias de funções internas que não sejam de cadeia de caracteres sempre são determinísticas.  
  
||||  
|-|-|-|  
|ABS|DATEDIFF|POWER|  
|ACOS|DAY|RADIANS|  
|ASIN|DEGREES|ROUND|  
|ATAN|EXP|SIGN|  
|ATN2|FLOOR|SIN|  
|CEILING|ISNULL|SQUARE|  
|COALESCE|ISNUMERIC|SQRT|  
|COS|LOG|TAN|  
|COT|LOG10|YEAR|  
|DATALENGTH|MONTH||  
|DATEADD|NULLIF||  
  
 As funções a seguir nem sempre são determinísticas, mas podem ser usadas em exibições indexadas ou índices em colunas computadas quando são especificadas de uma maneira determinística.  
  
|Função|Comentários|  
|--------------|--------------|  
|todas as funções de agregação|Todas as funções de agregação são determinísticas, a menos que sejam especificadas com as cláusulas OVER e ORDER BY. Para obter uma lista dessas funções, consulte [Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md).|  
|CAST|Determinística a menos que usado com **datetime**, **smalldatetime**ou **sql_variant**.|  
|CONVERT|Determinística, a menos que um destas condições exista:<br /><br /> <br /><br /> O tipo é **sql_variant**.<br /><br /> O tipo de destino é **sql_variant** e seu tipo de origem é não determinístico.<br /><br /> O tipo de origem ou de destino é **datetime** ou **smalldatetime**, o outro tipo de origem ou destino é uma cadeia de caracteres, e um estilo não determinístico é especificado. Para ser determinístico, o parâmetro de estilo deve ser uma constante. Além disso, estilos menores ou iguais a 100 são não determinísticos, com exceção dos estilos 20 e 21. Estilos maiores que 100 são determinísticos, com exceção dos estilos 106, 107, 109 e 113.|  
|CHECKSUM|Determinístico, com a exceção de CHECKSUM(*).|  
|ISDATE|Determinístico somente se usado com a função CONVERT, o parâmetro de estilo CONVERT é especificado e o estilo não é igual a 0, 100, 9 ou 109.|  
|RAND|RAND só é determinística quando um parâmetro *seed* é especificado.|  
  
 Todas as funções estatísticas de configuração, cursor, metadados, segurança e sistema são não determinísticas. Para obter uma lista dessas funções, consulte [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md), [Funções de cursor &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md), [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md), [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md) e [Funções estatísticas de sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md).  
  
 As funções internas a seguir de outras categorias nunca são determinísticas.  
  
|||  
|-|-|  
|@@CONNECTIONS |GETDATE|  
|@@CPU_BUSY |GETUTCDATE|  
|@@DBTS |GET_TRANSMISSION_STATUS|  
|@@IDLE |LAG|  
|@@IO_BUSY |LAST_VALUE|  
|@@MAX_CONNECTIONS |LEAD|  
|@@PACK_RECEIVED |MIN_ACTIVE_ROWVERSION|  
|@@PACK_SENT |NEWID|  
|@@PACKET_ERRORS |NEWSEQUENTIALID|  
|@@TIMETICKS |NEXT VALUE FOR|  
|@@TOTAL_ERRORS |NTILE|  
|@@TOTAL_READ |PARSENAME|  
|@@TOTAL_WRITE |PERCENTILE_CONT|  
|AT TIME ZONE|PERCENTILE_DISC|
|CUME_DIST|PERCENT_RANK|  
|CURRENT_TIMESTAMP|RAND|  
|DENSE_RANK|RANK|  
|FIRST_VALUE|ROW_NUMBER|   
|FORMAT|TEXTPTR|  
  
## <a name="calling-extended-stored-procedures-from-functions"></a>Chamando procedimentos armazenados estendidos de funções  
 Funções que chamam procedimentos armazenados estendidos são não determinísticas, pois esses procedimentos podem causar efeitos colaterais no banco de dados. Efeitos colaterais são alterações em um estado global do banco de dados, como a atualização de uma tabela ou de um recurso externo, como um arquivo ou a rede; por exemplo, a modificação de um arquivo ou o envio de uma mensagem de email. Não confie no retorno de um conjunto de resultados consistente ao executar um procedimento armazenado estendido de uma função definida pelo usuário. Funções definidas pelo usuário que criam efeitos colaterais no banco de dados não são recomendadas.  
  
 Quando chamado de dentro de uma função, o procedimento armazenado estendido não pode retornar conjuntos de resultados para o cliente. Todas as APIs Open Data Services que retornam conjuntos de resultados para o cliente têm um código de retorno FAIL.  
  
 O procedimento armazenado estendido pode voltar a se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, o procedimento não pode unir a mesma transação como a função original que invocou o procedimento armazenado estendido.  
  
 Semelhante a invocações de um procedimento armazenado ou em lotes, o procedimento armazenado estendido é executado no contexto da conta de segurança do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sob a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado. O proprietário do procedimento armazenado estendido deve considerar as permissões do contexto de segurança, ao conceder permissões a outros usuários para executar o procedimento.  
  
  

