---
title: UPDATETEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49bd324f97f6ba1d2e8a8120bb502199b4ca0f06
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="updatetext-transact-sql"></a>UPDATETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza uma existente **texto**, **ntext**, ou **imagem** campo. Use UPDATETEXT para alterar apenas uma parte de um **texto**, **ntext**, ou **imagem** coluna em vigor. Use WRITETEXT para atualizar e substituir um todo **texto**, **ntext**, ou **imagem** campo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use os tipos de dados de valor grande e o **.** A cláusula de gravação a [atualização](../../t-sql/queries/update-transact-sql.md) instrução em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 É o nome da tabela e **texto**, **ntext**, ou **imagem** coluna a ser atualizada. Nomes de tabela e nomes de coluna devem estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). A especificação do nome do banco de dados e de nomes de proprietários é opcional.  
  
 *dest_text_ptr*  
 Um ponteiro de texto valor (retornado pela função TEXTPTR) que aponta para o **texto**, **ntext**, ou **imagem** dados a serem atualizados. *dest_text_ptr* devem ser **binário (**16**)**.  
  
 *insert_offset*  
 É a posição inicial baseada em zero para a atualização. Para **texto** ou **imagem** colunas, *insert_offset* é o número de bytes a serem ignorados desde o início da coluna existente antes de inserir novos dados. Para **ntext** colunas, *insert_offset*é o número de caracteres (cada **ntext** caractere usa 2 bytes). Existente **texto**, **ntext**, ou **imagem** dados que começam nessa posição inicial com base em zero são deslocados à direita para liberar espaço para novos dados. Um valor de 0 insere os novos dados no início dos dados existentes. Um valor NULL acrescenta os novos dados ao valor dos dados existentes.  
  
 *delete_length*  
 É o comprimento dos dados a serem excluídos do existente **texto**, **ntext**, ou **imagem** coluna, iniciando no *insert_offset* posição. O *delete_length*valor é especificado em bytes para **texto** e **imagem** colunas e em caracteres para **ntext** colunas. Cada **ntext** caractere usa 2 bytes. Um valor de 0 não exclui nenhum dado. Um valor NULL exclui todos os dados do *insert_offset* posição final da existente **texto** ou **imagem** coluna.  
  
 WITH LOG  
 A criação de log é determinada pelo modelo de recuperação em vigor para o banco de dados.  
  
 *inserted_data*  
 Os dados a serem inseridos na existente **texto**, **ntext**, ou **imagem** coluna no *insert_offset* local. Este é um único **char**, **nchar**, **varchar**, **nvarchar**, **binário**,  **varbinary**, **texto**, **ntext**, ou **imagem** valor. *inserted_data* pode ser um literal ou uma variável.  
  
 *table_name.src_column_name*  
 É o nome da tabela e **texto**, **ntext**, ou **imagem** coluna usada como a fonte de dados inseridos. Os nomes de tabela e de coluna devem estar em conformidade com as regras para identificadores.  
  
 *src_text_ptr*  
 Um ponteiro de texto valor (retornado pela função TEXTPTR) que aponta para um **texto**, **ntext**, ou **imagem** coluna usada como a fonte de dados inseridos.  
  
> [!NOTE]  
>  *scr_text_ptr* valor não deve ser o mesmo que *dest_text_ptr*valor.  
  
## <a name="remarks"></a>Comentários  
 Os dados recém-inseridos podem ser um único *inserted_data* constante, o nome da tabela, o nome da coluna ou o ponteiro de texto.  
  
|Ação de atualizar|Parâmetros UPDATETEXT|  
|-------------------|---------------------------|  
|Para substituir dados existentes|Especifique um nonnull *insert_offset* valor, uma diferente de zero *delete_length* valor e os novos dados a ser inserido.|  
|Para excluir dados existentes|Especifique um nonnull *insert_offset* valor e um diferente de zero *delete_length*. Não especifique novos dados a serem inseridos.|  
|Para inserir novos dados|Especifique o *insert_offset* valor, uma *delete_length* 0 e os novos dados a ser inserido.|  
  
 Para melhor desempenho, recomendamos que **texto**, **ntext** e **imagem** dados sejam inseridos ou atualizados em tamanhos de blocos que sejam múltiplos de 8.040 bytes.  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ponteiros de texto em linha **texto**, **ntext**, ou **imagem** dados podem existir mas talvez não sejam válidos. Para obter informações sobre a opção text in row, consulte [sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obter informações sobre como invalidar ponteiros de texto, consulte [sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 Para inicializar **texto** colunas como NULL, use WRITETEXT; UPDATETEXT inicializa **texto** colunas em uma cadeia de caracteres vazia.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [READTEXT &#40; Transact-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40; Transact-SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  

