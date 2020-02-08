---
title: BEGIN DISTRIBUTED TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DISTRIBUTED
- BEGIN_DISTRIBUTED_TRANSACTION_TSQL
- DISTRIBUTED_TSQL
- BEGIN DISTRIBUTED TRANSACTION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN DISTRIBUTED TRANSACTION statement
- distributed transactions [SQL Server], starting
- MS DTC, transaction management
- distributed transactions [SQL Server], BEGIN DISTRIBUTED TRANSACTION statement
- servers [SQL Server], distributed transactions
- starting distributed transactions
- remote servers [SQL Server], distributed transactions
- starting transactions
ms.assetid: c3bc2716-39d3-4061-8c6a-8734899231ac
author: rothja
ms.author: jroth
ms.openlocfilehash: 0faddc5b763a2728dc507d2aad17b26501846452
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68125320"
---
# <a name="begin-distributed-transaction-transact-sql"></a>BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Especifica o início de uma transação distribuída [!INCLUDE[tsql](../../includes/tsql-md.md)] gerenciada pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC).  
    
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BEGIN DISTRIBUTED { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *transaction_name*  
 É o nome de uma transação definida pelo usuário usada para rastrear transação distribuída em utilitários MS DTC. *transaction_name* precisa estar em conformidade com as regras para identificadores e ter \< igual a 32 caracteres.  
  
 @*tran_name_variable*  
 É o nome de uma variável definida pelo usuário que contém um nome de transação usado para rastrear transação distribuída em utilitários MS DTC. A variável precisa ser declarada com o tipo de dados **char**, **varchar**, **nchar** ou **nvarchar**.  
  
## <a name="remarks"></a>Comentários  
 A instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que executa a instrução BEGIN DISTRIBUTED TRANSACTION é a originadora da transação e controla a conclusão da transação. Quando as instruções subsequentes COMMIT TRANSACTION ou ROLLBACK TRANSACTION são emitidas para a sessão, a instância controladora solicita que o MS DTC gerencie a conclusão da transação distribuída em todas as instâncias envolvidas.  
  
 O isolamento de instantâneo em nível de transação não oferece suporte a transações distribuídas.  
  
 A principal forma pela qual as instâncias remotas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] são inscritas em uma transação distribuída é quando uma sessão já inscrita na transação distribuída executa uma consulta distribuída que faz referência a um servidor vinculado.  
  
 Por exemplo, se BEGIN DISTRIBUTED TRANSACTION for emitido no ServidorA, a sessão chamará um procedimento armazenado no ServidorB e outro procedimento armazenado no ServidorC. O procedimento armazenado no ServidorC executará uma consulta distribuída no ServidorD e todos os quatro computadores serão envolvidos na transação distribuída. A instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no ServidorA é a instância controladora de origem para a transação.  
  
 As sessões envolvidas em transações distribuídas de [!INCLUDE[tsql](../../includes/tsql-md.md)] não obtêm um objeto de transação que elas possam passar para outra sessão, de modo que ele possa ser inscrito explicitamente na transação distribuída. O único modo para um servidor remoto se inscrever na transação é sendo o destino de uma consulta distribuída ou de uma chamada de procedimento armazenado remoto.  
  
 Quando uma consulta distribuída for executada em uma transação local, a transação será promovida automaticamente a uma transação distribuída se a fonte de dados OLE DB de destino for compatível com ITransactionLocal. Se a fonte de dados OLE DB de destino não for compatível com ITransactionLocal, apenas operações somente leitura serão permitidas na consulta distribuída.  
  
 Uma sessão já inscrita na transação distribuída executa uma chamada de procedimento armazenado remoto fazendo referência a um servidor remoto.  
  
 A opção **sp_configure remote proc trans** controla se as chamadas para procedimentos armazenados remotos em uma transação local fazem com que a transação local seja automaticamente promovida a uma transação distribuída gerenciada pelo MS DTC. A opção SET no nível da conexão REMOTE_PROC_TRANSACTIONS pode ser usada para substituir o padrão da instância estabelecido por **sp_configure remote proc trans**. Com essa opção definida, uma chamada de procedimento armazenado remoto faz com que uma transação local seja promovida a uma transação distribuída. A conexão que cria a transação do MS DTC se torna originadora da transação. COMMIT TRANSACTION inicia uma confirmação coordenada do MS DTC. Se a opção **sp_configure remote proc trans** estiver ON, as chamadas de procedimento armazenado remoto em transações locais serão protegidas automaticamente como parte das transações distribuídas sem que seja necessário reescrever os aplicativos para emitir especificamente BEGIN DISTRIBUTED TRANSACTION em vez de BEGIN TRANSACTION.  
  
 Para obter mais informações sobre o ambiente e o processo de transação distribuída, consulte a documentação do Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 Esse exemplo exclui um candidato do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] tanto na instância local do [!INCLUDE[ssDE](../../includes/ssde-md.md)], quanto na instância de um servidor remoto. Ambos os bancos de dados locais e remotos confirmarão ou reverterão a transação.  
  
> [!NOTE]  
>  A menos que o MS DTC esteja instalado atualmente no computador que executa a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Esse exemplo emitirá uma mensagem de erro. Para obter mais informações sobre a instalação do MS DTC, consulte a documentação do Coordenador de Transações Distribuídas da Microsoft.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN DISTRIBUTED TRANSACTION;  
-- Delete candidate from local instance.  
DELETE AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
-- Delete candidate from remote instance.  
DELETE RemoteServer.AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
