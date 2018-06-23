---
title: SQLGetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5c6f1220685b2e9f72df52ddea9c1f676453b856
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120352"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLGetStmtAttr para expor atributos de instrução específicos de driver estende o driver ODBC Native Client.  
  
 [SQLSetStmtAttr](sqlsetstmtattr.md) lista os atributos de instrução que sejam de leitura e gravação. Este tópico lista os atributos de instrução somente leitura.  
  
## <a name="sqlsoptsscurrentcommand"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 O atributo SQL_SOPT_SS_CURRENT_COMMAND expõe o comando atual de um lote de comando. O retorno é um inteiro que especifica o local do comando no lote. O valor *ValuePtr* é do tipo SQLLEN.  
  
## <a name="sqlsoptssnocountstatus"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 O atributo SQL_SOPT_SS_NOCOUNT_STATUS indica a configuração atual de NOCOUNT opção, que controla se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relata o número de linhas afetadas por uma instrução quando [SQLRowCount](sqlrowcount.md) é chamado. O valor *ValuePtr* é do tipo SQLLEN.  
  
|Valor|Description|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT é OFF. SQLRowCount retorna o número de linhas afetadas.|  
|SQL_NC_ON|NOCOUNT é ON. O número de linhas afetadas não é retornado por SQLRowCount e o valor retornado será 0.|  
  
 Se SQLRowCount retornará 0, o aplicativo deverá testar SQL_SOPT_SS_NOCOUNT_STATUS. Se SQL_NC_ON for retornado, o valor 0 de SQLRowCount apenas indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não retornou uma contagem de linhas. Se SQL_NC_OFF for retornado, isso significa que NOCOUNT está desativado e o valor de 0 de SQLRowCount indica que a instrução não afetou nenhuma linha.  
  
 Aplicativos não deverão exibir o valor de SQLRowCount quando SQL_SOPT_SS_NOCOUNT_STATUS for SQL_NC_OFF. Lotes grandes ou procedimentos armazenados podem conter várias instruções SET NOCOUNT, portanto não é possível supor que SQL_SOPT_SS_NOCOUNT_STATUS permaneça constante. Essa opção deve ser testada sempre que SQLRowCount retornará 0.  
  
## <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 O atributo SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT retorna o texto de mensagem para a solicitação de notificação de consulta.  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr e Parâmetros com valor de tabela  
 SQLGetStmtAttr pode ser chamado para obter o valor de SQL_SOPT_SS_PARAM_FOCUS no (APD) do descritor de parâmetro de aplicativo ao trabalhar com parâmetros com valor de tabela. Para obter mais informações sobre SQL_SOPT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLSetStmtAttr](http://go.microsoft.com/fwlink/?LinkId=59370)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  