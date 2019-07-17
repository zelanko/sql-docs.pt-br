---
title: sp_cursorprepexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorprepexec_TSQL
- sp_cursorprepexec
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorprepexec
ms.assetid: 8094fa90-35b5-4cf4-8012-0570cb2ba1e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: c344948b5eab2de6c7987494a29fe1131c47f35a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108409"
---
# <a name="spcursorprepexec-transact-sql"></a>sp_cursorprepexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Compila um plano para a instrução de cursor ou lote enviado e, em seguida, cria e popula o cursor. sp_cursorprepexec combina as funções de sp_cursorprepare e sp_cursorexecute. Esse procedimento é invocado pela especificação de ID = 5 em um pacote TDS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *identificador preparado*  
 É um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerado preparado *manipular* identificador. *identificador preparado* é obrigatório e retorna **int**.  
  
 *cursor*  
 É o identificador de cursor gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *cursor* é um parâmetro obrigatório que deve ser fornecido em todos os procedimentos subsequentes que atuam nesse cursor, por exemplo, sp_cursorfetch.  
  
 *params*  
 Identifica instruções parametrizadas. O *params* definição de variáveis é substituída para marcadores de parâmetro na instrução. *params* é um parâmetro obrigatório que chama uma **ntext**, **nchar**, ou **nvarchar** valor de entrada.  
  
> [!NOTE]  
>  Use uma **ntext** cadeia de caracteres como a entrada de valor quando *stmt* é parametrizado e o *scrollopt* valor PARAMETERIZED_STMT for ON.  
  
 *instrução*  
 Define o conjunto de resultados do cursor. O *instrução* parâmetro é obrigatório e chamadas para um **ntext**, **nchar** ou **nvarchar** valor de entrada.  
  
> [!NOTE]  
>  As regras para especificar o valor stmt são as mesmas de sp_cursoropen, com exceção de que o *stmt* tipo de dados de cadeia de caracteres deve ser **ntext**.  
  
 *options*  
 Um parâmetro opcional que retorna uma descrição das colunas do conjunto de resultados de cursor. *as opções* exige o seguinte **int** valor de entrada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Opção de rolagem. *scrollopt* é um parâmetro opcional que requer um dos seguintes **int** valores de entrada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 Devido à possibilidade de que a opção solicitada não é apropriada para o cursor definido por  *\<stmt >* , este parâmetro serve como entrada e saída. Nesses casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui um tipo apropriado e modifica esse valor.  
  
 *ccopt*  
 Opção de controle de simultaneidade. *ccopt* é um parâmetro opcional que requer um dos seguintes **int** valores de entrada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (anteriormente conhecido como LOCKCC)|  
|0x0004|**OTIMISTA** (anteriormente conhecido como OPTCC)|  
|0x0008|OPTIMISTIC (anteriormente conhecido como OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Assim como acontece com *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode atribuir um valor diferente daquele que foi solicitado.  
  
 *rowcount*  
 É um parâmetro opcional que significa o número de linhas de buffer de busca a ser usado com AUTO_FETCH. O padrão é 20 linhas. *número de linhas* tem um comportamento diferente quando atribuído como um valor de entrada versus um valor de retorno.  
  
|Como valor de entrada|Como valor de retorno|  
|--------------------|---------------------|  
|Quando AUTO_FETCH é especificado com cursores FAST_FORWARD *rowcount* representa o número de linhas a serem colocadas no buffer de busca.|Representa o número de linhas no conjunto de resultados. Quando o *scrollopt* valor AUTO_FETCH é especificado, *rowcount* retorna o número de linhas que foram buscadas no buffer de busca.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Se *params* retorna um valor nulo, em seguida, a instrução não é parametrizada.  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursorprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
