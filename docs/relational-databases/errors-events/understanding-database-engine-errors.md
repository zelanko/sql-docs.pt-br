---
title: Compreendendo os erros do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], about errors
- errors [SQL Server], Database Engine
- errors [SQL Server]
- Database Engine [SQL Server], errors
ms.assetid: ddaca9d3-956f-46a5-8cd3-a7a15ec75878
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5ed21ec6de1f739eec94d3b47bc31eb9de2b9ebb
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34328897"
---
# <a name="understanding-database-engine-errors"></a>Compreendendo os erros do Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Os erros gerados pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] têm os atributos descritos na tabela abaixo.  
  
|attribute|Descrição|  
|---------------|-----------------|  
|Número do erro|Cada mensagem de erro tem um número de erro exclusivo.|  
|Error message string|A mensagem de erro contém informações de diagnóstico sobre a causa do erro. Muitas mensagens de erro têm variáveis de substituição nas quais são inseridas informações, como o nome do objeto que gera o erro.|  
|Severity|A severidade indica a gravidade do erro. Erros com uma severidade baixa , como 1 ou 2, são mensagens de informações ou advertências de nível baixo. Erros com uma severidade alta indicam problemas que devem ser tratados o mais rápido possível. Para obter mais informações sobre severidades, consulte [Severidade de erro do mecanismo de banco de dados](../../relational-databases/errors-events/database-engine-error-severities.md).|  
|Estado|Algumas mensagens de erro podem ser geradas em vários pontos no código para o [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, um erro 1105 pode ser gerado para várias condições diferentes. Cada condição específica que gera um erro atribui um código de estado exclusivo.<br /><br /> Quando você estiver exibindo bancos de dados que contêm informações sobre assuntos conhecidos, como A Base de Dados de Conhecimento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] , você pode usar o número do estado para determinar se o assunto registrado é igual ao erro que você encontrou. Por exemplo, se um Artigo da Base de Dados de Conhecimento descreve um erro 1105 com um estado 2 e a mensagem de erro 1105 que você recebeu tinha um estado 3, o erro provavelmente tem uma causa diferente daquela informada no artigo.<br /><br /> Um engenheiro de suporte [!INCLUDE[msCoName](../../includes/msconame-md.md)] também pode usar o código de estado de um erro para encontrar o local no código de origem onde está sendo gerado aquele código de erro. Essas informações podem fornecer ideias adicionais sobre como diagnosticar o problema.|  
|Nome do procedimento|É o nome do procedimento armazenado ou disparador no qual ocorreu o erro.|  
|Line number|Indica qual instrução em um lote, procedimento armazenado, disparador ou função gerou o erro.|  
  
 Todas as mensagens de erro do sistema e definidas pelo usuário em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estão na exibição de catálogo **sys.messages** . Você pode usar a instrução RAISERROR para retornar erros definidos pelo usuário a um aplicativo.  
  
 Todos os APIs de banco de dados, como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **SQLClient** namespace, ActiveX Data Objects (ADO), OLE DB e Open Database Connectivity (ODBC), informam os atributos básicos de erro. Essa informação inclui o número de erro e cadeia de caracteres de mensagem. Porém, nem todos os APIs informam todos os outros atributos de erro.  
  
 Informações sobre um erro que acontece no escopo do bloco TRY de uma construção TRY.CATCH podem ser obtidas em código [!INCLUDE[tsql](../../includes/tsql-md.md)] usando-se funções como ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY e ERROR_STATE no escopo do bloco CATCH associado. Para obter mais informações, consulte [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir consulta a exibição de catálogo `sys.messages` para retornar uma lista de todas as mensagens de erro do sistema e definidas pelo usuário no [!INCLUDE[ssDE](../../includes/ssde-md.md)] que tenham texto em inglês (`1033`).  
  
```  
SELECT  
    message_id,  
    language_id,  
    severity,  
    is_event_logged,  
    text  
  FROM sys.messages  
  WHERE language_id = 1033;  
```  
  
 Para obter mais informações, consulte [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)  
  
  
