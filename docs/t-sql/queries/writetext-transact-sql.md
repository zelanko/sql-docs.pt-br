---
title: WRITETEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WRITETEXT_TSQL
- WRITETEXT
dev_langs:
- TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c10e7259062316454e4e0ecf430f6fdb87c53caf
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67948101"
---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite a atualização interativa minimamente registrada de uma coluna de **text**, **ntext** ou **image** existente. WRITETEXT substitui quaisquer dados existentes na coluna afetada. WRITETEXT não pode ser usado em colunas de **text**, **ntext** e **image** em exibições.  
  
> [!IMPORTANT]
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use os tipos de dados de valor grande e a cláusula **.** WRITE da instrução [UPDATE](../../t-sql/queries/update-transact-sql.md) nesse caso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
 *table* **.column**  
 É o nome da tabela e da coluna de **text**, **ntext** ou **image** a ser atualizado. Os nomes de tabela e de coluna precisam estar de acordo com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md). A especificação do nome do banco de dados e de nomes de proprietários é opcional.  
  
 *text_ptr*  
 É um valor que armazena o ponteiro para os dados de **text**, **ntext** ou **image**. *text_ptr* precisa ser **binary(16)** . Para criar um ponteiro de texto, execute uma instrução [INSERT](../../t-sql/statements/insert-transact-sql.md) ou [UPDATE](../../t-sql/queries/update-transact-sql.md) com os dados não nulos para a coluna **text**, **ntext** ou **image**.  
  
 WITH LOG  
 Ignorado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A criação de log é determinada pelo modelo de recuperação em vigor para o banco de dados.  
  
 *data*  
 São os dados reais de **text**, **ntext** ou **image** a serem armazenados. *data* pode ser um literal ou um parâmetro. O comprimento máximo do texto que pode ser inserido de forma interativa com WRITETEXT é de aproximadamente 120 KB para dados de **text**, **ntext** e **image**.  
  
## <a name="remarks"></a>Comentários  
 Use WRITETEXT para substituir dados de **text**, **ntext** e **image** e UPDATETEXT para modificar dados de **text**, **ntext** e **image**. UPDATETEXT é mais flexível porque altera somente uma parte de uma coluna de **text**, **ntext** ou **image** e não a coluna inteira.  
  
 Para obter o melhor desempenho possível, recomenda-se que os dados de **text**, **ntext** e **image** sejam inseridos ou atualizados em partes com tamanhos que sejam múltiplos de 8040 bytes.  
  
 Se o modelo de recuperação do banco de dados for simples ou bulk-logged, as operações de **text**, **ntext** e **image** que usam WRITETEXT serão registradas minimamente quando novos dados forem inseridos ou anexados.  
  
> [!NOTE]  
>  A criação mínima de log não é usada quando valores existentes são atualizados.  
  
 Para que WRITETEXT funcione corretamente, a coluna já deve conter um ponteiro de texto válido.  
  
 Se a tabela não tiver texto em linha, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] economizará espaço com a não inicialização de colunas de **text** quando valores nulos explícitos ou implícitos forem adicionados em colunas de **text** com INSERT e quando nenhum ponteiro de texto puder ser obtido para esses nulos. Para inicializar colunas de **text** como NULL, use a instrução UPDATE. Se a tabela tiver texto em linha, não será necessário inicializar a coluna de texto para nulos e sempre será possível obter um ponteiro de texto.  
  
 A função ODBC SQLPutData é mais rápida e usa menos memória dinâmica que WRITETEXT. Esta função pode inserir até 2 gigabytes de dados de **text**, **ntext** ou **image**.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podem existir ponteiros de texto em linha para os dados de **text**, **ntext** ou **image**, mas talvez eles não sejam válidos. Para obter informações sobre a opção text in row, consulte [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obter informações sobre como invalidar ponteiros de texto, consulte [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
