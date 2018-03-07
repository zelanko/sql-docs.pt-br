---
title: "Defina as estatísticas e/s (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_IO_TSQL
- IO
- IO_TSQL
- SET STATISTICS IO
dev_langs:
- TSQL
helpviewer_keywords:
- disk I/O statistics [SQL Server]
- I/O [SQL Server], disk activity information
- disks [SQL Server], statement statistics
- STATISTICS IO option
- statements [SQL Server], statistical information
- SET STATISTICS IO statement
- statistical information [SQL Server], disk activity
ms.assetid: 7033aac9-a944-4156-9ff4-6ef65717a28b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3b2aad11610a23c3686e279daa60c57bf7c8154f
ms.sourcegitcommit: b09bccd6dfdba55b022355e892c29cb50aadd795
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="set-statistics-io-transact-sql"></a>SET STATISTICS IO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Faz o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibir informações referentes à quantidade de atividade em disco gerada pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET STATISTICS IO { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 Quando STATISTICS IO está ON, as informações de estatística são exibidas. Quando está OFF, as informações não são exibidas.  
  
 Depois que essa opção é definida como ON, todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] subsequentes retornam a informações de estatística até que a opção seja definida como OFF.  
  
 A tabela a seguir lista e descreve os itens de saída.  
  
|Item de saída|Significado|  
|-----------------|-------------|  
|**Table**|Nome da tabela.|  
|**Contagem de exame**|Número de buscas/exames iniciados depois de alcançar o nível folha em qualquer direção para recuperar todos os valores para construir o conjunto de dados final para a saída.<br /><br /> A contagem de exame será 0 se o índice usado for um índice exclusivo ou índice clusterizado em uma chave primária e se você estiver buscando somente um valor. Por exemplo, `WHERE Primary_Key_Column = <value>`.<br /><br /> Contagem de exame será 1 quando você está procurando um valor usando um índice clusterizado não exclusivo que é definido em uma coluna de chave não primária. Isto é feito para verificar se há valores duplicados para o valor de chave para o qual você está pesquisando. Por exemplo, `WHERE Clustered_Index_Key_Column = <value>`.<br /><br /> A contagem de exame será N quando N for o número de busca/exame diferente iniciado para a esquerda ou para a direita no nível folha depois de localizar um valor de chave usando a chave de índice.|  
|**leituras lógicas**|Número de páginas lidas do cache de dados.|  
|**Leituras físicas**|Número de páginas lidas do disco.|  
|**Leituras read-ahead**|Número de páginas colocadas no cache para a consulta.|  
|**leituras lógicas LOB**|Número de **texto**, **ntext**, **imagem**, ou o tipo de valor grande (**varchar (max)**, **nvarchar (max)**, **varbinary (max)**) páginas lidas do cache de dados.|  
|**Leituras físicas LOB**|Número de **texto**, **ntext**, **imagem** ou páginas de tipo de valor grande lidas do disco.|  
|**Leituras read-ahead LOB**|Número de **texto**, **ntext**, **imagem** ou páginas colocadas no cache para a consulta de tipo de valor grande.|  
  
 A configuração de SET STATISTICS IO é definida no momento da execução e não no momento da análise.  
  
> [!NOTE]  
>  Quando instruções Transact-SQL recuperam colunas LOB, algumas operações de recuperação de LOB podem requerer cruzamento de árvore de LOB várias vezes. Isso pode fazer com que SET STATISTICS IO informe um número maior de leituras lógicas do que o esperado.  
  
## <a name="permissions"></a>Permissões  
 Para usar SET STATISTICS IO, os usuários devem ter as permissões apropriadas para executar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. A permissão SHOWPLAN não é exigida.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo mostra quantas leituras lógicas e físicas são usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à medida que processa as instruções.  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS IO ON;  
GO  
SELECT *   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS IO OFF;  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
Table 'ProductCostHistory'. Scan count 1, logical reads 5, physical   
reads 0, read-ahead reads 0, lob logical reads 0, lob physical reads 0,   
lob read-ahead reads 0.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)  
  
  
