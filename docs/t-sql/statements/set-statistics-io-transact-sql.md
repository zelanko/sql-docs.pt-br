---
title: SET STATISTICS IO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 20099478d1d2dd047b1f17fe963c8fc45b1418fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670257"
---
# <a name="set-statistics-io-transact-sql"></a>SET STATISTICS IO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Faz o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibir informações referentes à quantidade de atividade em disco gerada pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
|**Contagem de verificações**|Número de buscas/exames iniciados depois de alcançar o nível folha em qualquer direção para recuperar todos os valores para construir o conjunto de dados final para a saída.<br /><br /> A contagem de exame será 0 se o índice usado for um índice exclusivo ou índice clusterizado em uma chave primária e se você estiver buscando somente um valor. Por exemplo, `WHERE Primary_Key_Column = <value>`.<br /><br /> A contagem da verificação será 1 quando você estiver pesquisando um valor usando um índice clusterizado não exclusivo que é definido em uma coluna de chave não primária. Isto é feito para verificar se há valores duplicados para o valor de chave para o qual você está pesquisando. Por exemplo, `WHERE Clustered_Index_Key_Column = <value>`.<br /><br /> A contagem de exame será N quando N for o número de busca/exame diferente iniciado para a esquerda ou para a direita no nível folha depois de localizar um valor de chave usando a chave de índice.|  
|**leituras lógicas**|Número de páginas lidas do cache de dados.|  
|**physical reads**|Número de páginas lidas do disco.|  
|**leituras antecipadas**|Número de páginas colocadas no cache para a consulta.|  
|**leituras lógicas lob**|Número de páginas **text**, **ntext**, **image** ou de tipo de valor grande (**varchar(max)**, **nvarchar(max)**, **varbinary(max)**) lidas do cache de dados.|  
|**leituras físicas lob**|Número de páginas de tipo **text**, **ntext**, **image** ou de valor grande lidas do disco.|  
|**leituras antecipadas lob**|Número de páginas **text**, **ntext**, **image** ou de tipo de valor grande colocadas no cache para a consulta.|  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)  
  
  
