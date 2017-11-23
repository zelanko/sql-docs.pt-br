---
title: WRITETEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WRITETEXT_TSQL
- WRITETEXT
dev_langs: TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
caps.latest.revision: "52"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 534fa1494ec97efb8258222f512902d15efa1f36
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite a atualização interativa minimamente registrada de um objeto existente **texto**, **ntext**, ou **imagem** coluna. WRITETEXT substitui quaisquer dados existentes na coluna afetada. WRITETEXT não pode ser usado em **texto**, **ntext**, e **imagem** colunas nos modos de exibição.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use os tipos de dados de valor grande e o **.** A cláusula de gravação a [atualização](../../t-sql/queries/update-transact-sql.md) instrução em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WRITETEXT [BULK]  
  { table.column text_ptr }  
  [ WITH LOG ] { data }  
```  
  
## <a name="arguments"></a>Argumentos  
 BULK  
 Permite carregar ferramentas para carregar um fluxo de dados binários. O fluxo deve ser fornecido pela ferramenta no nível do protocolo TDS. Quando o fluxo de dados não está presente, o processador de consulta ignora a opção de BULK.  
  
> [!IMPORTANT]  
>  Nós recomendamos que a opção de BULK não seja usada em aplicativos baseados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção deve ser alterada ou removida em uma futura versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *tabela* **.column**  
 É o nome da tabela e **texto**, **ntext**, ou **imagem** coluna para atualizar. Nomes de tabela e coluna devem estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). A especificação do nome do banco de dados e de nomes de proprietários é opcional.  
  
 *text_ptr*  
 É um valor que armazena o ponteiro para o **texto**, **ntext**, ou **imagem** dados. *text_ptr* devem ser **binário (16)**. Para criar um ponteiro de texto, execute uma [inserir](../../t-sql/statements/insert-transact-sql.md) ou [atualização](../../t-sql/queries/update-transact-sql.md) instrução com dados que não sejam nulos para o **texto**, **ntext**, ou **imagem** coluna.  
  
 WITH LOG  
 Ignorado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A criação de log é determinada pelo modelo de recuperação em vigor para o banco de dados.  
  
 *dados*  
 É o valor real **texto**, **ntext** ou **imagem** dados serão armazenados. *dados* pode ser um literal ou um parâmetro. O comprimento máximo do texto que pode ser inserido interativamente com WRITETEXT é aproximadamente 120 KB para **texto**, **ntext**, e **imagem** dados.  
  
## <a name="remarks"></a>Comentários  
 Use WRITETEXT para substituir **texto**, **ntext**, e **imagem** dados e UPDATETEXT para modificar **texto**, **ntext**, e **imagem** dados. UPDATETEXT é mais flexível porque altera somente uma parte de um **texto**, **ntext**, ou **imagem** coluna em vez da coluna inteira.  
  
 Para melhor desempenho, recomendamos que **texto**, **ntext**, e **imagem** dados sejam inseridos ou atualizados em tamanhos de bloco que sejam múltiplos de 8040 bytes.  
  
 Se o modelo de recuperação do banco de dados for simples ou bulk-logged, **texto**, **ntext**, e **imagem** operações que usem WRITETEXT serão operações minimamente registradas quando novos dados inseridos ou anexados.  
  
> [!NOTE]  
>  A criação mínima de log não é usada quando valores existentes são atualizados.  
  
 Para que WRITETEXT funcione corretamente, a coluna já deve conter um ponteiro de texto válido.  
  
 Se a tabela não tiver texto em linha, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] economiza espaço por não inicializar **texto** colunas quando valores nulos explícitos ou implícitos forem adicionados em **texto** colunas com INSERT e nenhum ponteiro de texto podem ser obtido para tais nulos. Para inicializar **texto** colunas como NULL, use a instrução UPDATE. Se a tabela tiver texto em linha, não será necessário inicializar a coluna de texto para nulos e sempre será possível obter um ponteiro de texto.  
  
 A função SQLPutData ODBC é mais rápida e usa menos memória dinâmica que WRITETEXT. Esta função pode inserir até 2 gigabytes de **texto**, **ntext**, ou **imagem** dados.  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], na linha ponteiros de texto **texto**, **ntext**, ou **imagem** dados podem existir mas talvez não sejam válidos. Para obter informações sobre a opção text in row, consulte [sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obter informações sobre como invalidar ponteiros de texto, consulte [sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão UPDATE na tabela especificada. A permissão será transferível quando a permissão UPDATE for transferida.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir coloca o ponteiro de texto na variável local `@ptrval` e, depois, `WRITETEXT` coloca a nova cadeia de caracteres de texto na linha apontada por `@ptrval`.  
  
> [!NOTE]  
>  Para executar este exemplo, você deve instalar o banco de dados de exemplo pubs.  
  
```  
USE pubs;  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
DECLARE @ptrval binary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books'  
WRITETEXT pub_info.pr_info @ptrval 'New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!';  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40; Transact-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
