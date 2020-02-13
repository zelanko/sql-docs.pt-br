---
title: UPDATETEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATETEXT
- UPDATETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text updates [SQL Server]
- updating data [SQL Server]
- data updates [SQL Server], UPDATETEXT statement
- UPDATETEXT statement
ms.assetid: d73c28ee-3972-4afd-af8d-ebbbd9e50793
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b858cc4930cdfe9792e08c991c3ebdf8f319d0f0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67948229"
---
# <a name="updatetext-transact-sql"></a>UPDATETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza um campo **text**, **ntext** ou **image** existente. Use UPDATETEXT para alterar apenas uma parte de uma coluna **text**, **ntext** ou **image** em vigor. Use WRITETEXT para atualizar e substituir todo um campo **text**, **ntext** ou **image**.  
  
> [!IMPORTANT]
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use os tipos de dados de valor grande e a cláusula **.** WRITE da instrução [UPDATE](../../t-sql/queries/update-transact-sql.md) nesse caso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPDATETEXT [BULK] { table_name.dest_column_name dest_text_ptr }  
  { NULL | insert_offset }  
     { NULL | delete_length }  
     [ WITH LOG ]  
     [ inserted_data  
    | { table_name.src_column_name src_text_ptr } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 BULK  
 Permite carregar ferramentas para carregar um fluxo de dados binários. O fluxo deve ser fornecido pela ferramenta no nível do protocolo TDS. Quando o fluxo de dados não está presente, o processador de consulta ignora a opção de BULK.  
  
> [!IMPORTANT]  
>  Nós recomendamos que a opção de BULK não seja usada em aplicativos baseados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção deve ser alterada ou removida em uma futura versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *table_name* **.** *dest_column_name*  
 É o nome da tabela e da coluna **text**, **ntext** ou **image** a ser atualizado. Os nomes de tabela e de coluna devem obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md). A especificação do nome do banco de dados e de nomes de proprietários é opcional.  
  
 *dest_text_ptr*  
 É um valor de ponteiro de texto (retornado pela função TEXTPTR) que aponta para os dados **text**, **ntext** ou **image** a serem atualizados. *dest_text_ptr* deve ser **binary(** 16 **)** .  
  
 *insert_offset*  
 É a posição inicial baseada em zero para a atualização. Para colunas **text** ou **image**, *insert_offset* é o número de bytes a ser ignorado do início da coluna existente antes de inserir novos dados. Para colunas **ntext**, *insert_offset* é o número de caracteres (cada caractere **ntext** usa 2 bytes). Os dados **text**, **ntext** ou **image** existentes que começam nessa posição inicial baseada em zero são deslocados para a direita, dando lugar aos novos dados. Um valor de 0 insere os novos dados no início dos dados existentes. Um valor NULL acrescenta os novos dados ao valor dos dados existentes.  
  
 *delete_length*  
 É o tamanho dos dados a serem excluídos da coluna **text**, **ntext** ou **image** existente, começando na posição *insert_offset*. O valor de *delete_length* é especificado em bytes para colunas **text** e **image** e em caracteres para colunas **ntext**. Cada caractere **ntext** usa 2 bytes. Um valor de 0 não exclui nenhum dado. Um valor NULL exclui todos os dados da posição *insert_offset* até o final da coluna **text** ou **image** existente.  
  
 WITH LOG  
 A criação de log é determinada pelo modelo de recuperação em vigor para o banco de dados.  
  
 *inserted_data*  
 São os dados a serem inseridos na coluna **text**, **ntext** ou **image** existente no local *insert_offset*. Esse é um único valor **char**, **nchar**, **varchar**, **nvarchar**, **binary**, **varbinary**, **text**, **ntext** ou **image**. *inserted_data* pode ser um literal ou uma variável.  
  
 *table_name.src_column_name*  
 É o nome da tabela e da coluna **text**, **ntext** ou **image** usada como a origem dos dados inseridos. Os nomes de tabela e de coluna devem estar em conformidade com as regras para identificadores.  
  
 *src_text_ptr*  
 É um valor de ponteiro de texto (retornado pela função TEXTPTR) que aponta para uma coluna **text**, **ntext** ou **image** usada como a origem dos dados inseridos.  
  
> [!NOTE]  
>  O valor de *scr_text_ptr* não deve ser o mesmo que o valor *dest_text_ptr*.  
  
## <a name="remarks"></a>Comentários  
 Os dados recém-inseridos podem ser uma única constante *inserted_data*, um nome de tabela, um nome de coluna ou um ponteiro de texto.  
  
|Ação de atualizar|Parâmetros UPDATETEXT|  
|-------------------|---------------------------|  
|Para substituir dados existentes|Especifique um valor de *insert_offset* não nulo, um valor de *delete_length* diferente de zero e os novos dados a serem inseridos.|  
|Para excluir dados existentes|Especifique um valor não nulo de *insert_offset* e um *delete_length* diferente de zero. Não especifique novos dados a serem inseridos.|  
|Para inserir novos dados|Especifique o valor de *insert_offset*, um *delete_length* igual a 0 e os novos dados a serem inseridos.|  
  
 Para obter um melhor desempenho, recomendamos que os dados **text**, **ntext** e **image** sejam inseridos ou atualizados em tamanhos de partes que sejam múltiplos de 8.040 bytes.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os ponteiros de texto em linha para os dados **text**, **ntext** ou **image** podem existir, mas podem não ser válidos. Para obter informações sobre a opção text in row, consulte [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obter informações sobre como invalidar ponteiros de texto, consulte [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 Para inicializar colunas **text** com NULL, use WRITETEXT; UPDATETEXT inicializa colunas **text** com uma cadeia de caracteres vazia.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão UPDATE na tabela especificada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir coloca o ponteiro de texto na variável local `@ptrval` e, depois, usa `UPDATETEXT` para atualizar um erro ortográfico.  
  
> [!NOTE]  
>  Para executar este exemplo, é necessário instalar o banco de dados pubs.  
  
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
UPDATETEXT pub_info.pr_info @ptrval 88 1 'b';  
GO  
ALTER DATABASE pubs SET RECOVERY FULL;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
