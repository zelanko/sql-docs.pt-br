---
title: sp_cursoroption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 581a154dfefa7823e9a1c0cefa53518352c66d55
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85869111"
---
# <a name="sp_cursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define opções de cursor ou retorna informações de cursor criadas pelo procedimento armazenado sp_cursoropen. sp_cursoroption é invocado especificando ID = 8 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 É um valor de *identificador* que é gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e retornado pelo procedimento armazenado sp_cursoropen. o *cursor* requer um valor de entrada **int** para execução.  
  
 *code*  
 Usado para estipular vários fatores dos valores de retorno de cursor. o *código* requer um dos seguintes valores de entrada **int** :  
  
|Valor|Nome|Descrição|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|Retorna o ponteiro de texto, e não os dados reais, para certos textos designados ou colunas de imagem.<br /><br /> TEXTPTR_ONLY permite que os ponteiros de texto sejam usados como *identificadores* para objetos de BLOB, que posteriormente podem ser recuperados seletivamente ou atualizados usando [!INCLUDE[tsql](../../includes/tsql-md.md)] ou DBLIB instalações (por exemplo, [!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT ou DBLIB dbwritetext).<br /><br /> Se um valor "0" for atribuído, todas as colunas de texto e imagem na lista selecionada retornarão ponteiros de texto, em vez de dados.|  
|0x0002|CURSOR_NAME|Atribui o nome especificado em *valor* ao cursor. Isso, por sua vez, permite que o ODBC use [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções UPDATE/DELETE posicionadas nos cursores abertos por meio de sp_cursoropen.<br /><br /> É possível especificar a cadeia de caracteres como qualquer tipo de dados de caractere ou Unicode.<br /><br /> Como as [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções UPDATE/DELETE posicionadas operam, por padrão, na primeira linha em um cursor de FAT, sp_cursor SETPOSITION deve ser usado para posicionar o cursor antes de emitir a instrução UPDATE/DELETE posicionada.|  
|0x0003|TEXTDATA|Retorna os dados reais, não o ponteiro de texto, para certas colunas de texto ou imagem em buscas subsequentes (isto é, desfaz o efeito de TEXTPTR_ONLY).<br /><br /> Se TEXTDATA for habilitado para uma coluna específica, a linha será buscada novamente ou atualizada e poderá ser definida outra vez como TEXTPTR_ONLY. Assim como ocorre com TEXTPTR_ONLY, o parâmetro de valor é um inteiro que especifica o número da coluna e um valor de zero retorna todas as colunas de texto ou imagem.|  
|0x0004|SCROLLOPT|Opção de rolagem. Consulte "Valores de códigos retornados" posteriormente neste tópico para obter informações adicionais.|  
|0x0005|CCOPT|Opção de controle de simultaneidade. Consulte "Valores de códigos retornados" posteriormente neste tópico para obter informações adicionais.|  
|0x0006|ROWCOUNT|O número de linhas atualmente no conjunto de resultados.<br /><br /> Observação: o número de linhas pode ter mudado desde o valor retornado por sp_cursoropen se a população assíncrona estiver sendo usada. O valor-1 será retornado se o número de linhas for desconhecido.|  
  
 *value*  
 Designa o valor retornado pelo *código*. *Value* é um parâmetro necessário que chama um valor de entrada de *código* 0x0001, 0x0002 ou 0x0003.  
  
> [!NOTE]  
>  Um valor de *código* de 2 é um tipo de dados de cadeia de caracteres. Qualquer outra entrada de valor de *código* ou retornada pelo *valor* é um inteiro.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O parâmetro *Value* pode retornar um dos valores de *código* a seguir.  
  
|Retornar valor|Descrição|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 O parâmetro *Value* retorna um dos seguintes valores de scrollopt.  
  
|Retornar valor|Descrição|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 O parâmetro *Value* retorna um dos seguintes valores de ccopt.  
  
|Retornar valor|Descrição|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 ou 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_cursor](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_cursoropen](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
