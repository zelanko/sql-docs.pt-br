---
title: sp_cursoroption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b404bdb0b96883df1b1e39b9190285b4795aeaa4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spcursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define opções de cursor ou retorna informações de cursor criadas pelo procedimento armazenado sp_cursoropen. sp_cursoroption é invocado pela especificação de ID = 8 em um pacote de protocolo TDS de dados tabulares.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 É um *tratar* valor que é gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e retornado pelo procedimento armazenado sp_cursoropen. *cursor* requer um **int** valor para a execução de entrada.  
  
 *Código*  
 Usado para estipular vários fatores dos valores de retorno de cursor. *código* requer um dos seguintes **int** valores de entrada:  
  
|Value|Nome|Description|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|Retorna o ponteiro de texto, e não os dados reais, para certos textos designados ou colunas de imagem.<br /><br /> TEXTPTR_ONLY permite usar ponteiros de texto a ser usado como *identificadores* para objetos blob que podem ser recuperados seletivamente ou atualizados usando [!INCLUDE[tsql](../../includes/tsql-md.md)] ou instalações DBLIB (por exemplo, [!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT ou DBLIB DBWRITETEXT).<br /><br /> Se um valor "0" for atribuído, todas as colunas de texto e imagem na lista selecionada retornarão ponteiros de texto, em vez de dados.|  
|0x0002|CURSOR_NAME|Atribui o nome especificado no *valor* até o cursor. Isso, por sua vez, permite ao ODBC usar [!INCLUDE[tsql](../../includes/tsql-md.md)] posicionado instruções UPDATE/DELETE em cursores abertos via sp_cursoropen.<br /><br /> É possível especificar a cadeia de caracteres como qualquer tipo de dados de caractere ou Unicode.<br /><br /> Como [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções UPDATE/DELETE posicionadas operam, por padrão, na primeira linha em um cursor fat, sp_cursor SETPOSITION deve ser usado para posicionar o cursor antes de emitir a instrução UPDATE/DELETE posicionada.|  
|0x0003|TEXTDATA|Retorna os dados reais, não o ponteiro de texto, para certas colunas de texto ou imagem em buscas subsequentes (isto é, desfaz o efeito de TEXTPTR_ONLY).<br /><br /> Se TEXTDATA for habilitado para uma coluna específica, a linha será buscada novamente ou atualizada e poderá ser definida outra vez como TEXTPTR_ONLY. Assim como ocorre com TEXTPTR_ONLY, o parâmetro de valor é um inteiro que especifica o número da coluna e um valor de zero retorna todas as colunas de texto ou imagem.|  
|0x0004|SCROLLOPT|Opção de rolagem. Consulte "Valores de códigos retornados" posteriormente neste tópico para obter informações adicionais.|  
|0x0005|CCOPT|Opção de controle de simultaneidade. Consulte "Valores de códigos retornados" posteriormente neste tópico para obter informações adicionais.|  
|0x0006|ROWCOUNT|O número de linhas atualmente no conjunto de resultados.<br /><br /> Observação: O número de linhas pode ter mudado desde o valor retornado por sp_cursoropen se população assíncrona estiver sendo usada. O valor –1 será retornado se o número de linhas for desconhecido.|  
  
 *value*  
 Designa o valor retornado por *código*. *valor* é um parâmetro obrigatório que chama um 0x0001, 0x0002 ou 0x0003 *código* valor de entrada.  
  
> [!NOTE]  
>  Um *código* valor 2 é um tipo de dados de cadeia de caracteres. Qualquer outro *código* valor de entrada ou retornadas por *valor* é um inteiro.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 O *valor* parâmetro pode retornar um dos seguintes *código* valores.  
  
|Valor retornado|Description|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 O *valor* parâmetro retorna um dos valores SCROLLOPT a seguir.  
  
|Valor retornado|Description|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 O *valor* parâmetro retorna um dos valores CCOPT a seguir.  
  
|Valor retornado|Description|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 ou 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
