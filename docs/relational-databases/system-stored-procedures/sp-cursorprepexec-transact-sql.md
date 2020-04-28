---
title: sp_cursorprepexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
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
ms.openlocfilehash: 660a75f1e6fea9b5a825372501c2e65f2dd3874b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "69652431"
---
# <a name="sp_cursorprepexec-transact-sql"></a>sp_cursorprepexec (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Compila um plano para a instrução de cursor ou lote enviado e, em seguida, cria e popula o cursor. sp_cursorprepexec combina as funções de sp_cursorprepare e sp_cursorexecute. Esse procedimento é invocado especificando ID = 5 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link](../../database-engine/configure-windows/media/topic-link.gif "ícone de link") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
    [, '@parameter_name[,...n ]']
```  
  
## <a name="arguments"></a>Argumentos  
 *identificador preparado*  
 É um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador de *identificador* preparado gerado. o *identificador preparado* é necessário e retorna **int**.  
  
 *cursor*  
 É o identificador de cursor gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *cursor* é um parâmetro necessário que deve ser fornecido em todos os procedimentos subsequentes que atuam sobre esse cursor, por exemplo, sp_cursorfetch.  
  
 *params*  
 Identifica instruções parametrizadas. A definição *params* das variáveis é substituída por marcadores de parâmetro na instrução. *params* é um parâmetro necessário que chama um valor de entrada **ntext**, **nchar**ou **nvarchar** .  
  
> [!NOTE]  
>  Use uma cadeia de caracteres **ntext** como o valor de entrada quando *stmt* estiver parametrizada e o valor de PARAMETERIZED_STMT *scrollopt* for on.  
  
 *privacidade*  
 Define o conjunto de resultados do cursor. O parâmetro de *instrução* é obrigatório e chama um valor de entrada **ntext**, **nchar**ou **nvarchar** .  
  
> [!NOTE]  
>  As regras para especificar o valor stmt são as mesmas que as para sp_cursoropen, com a exceção de que o tipo de dados da cadeia de caracteres *stmt* deve ser **ntext**.  
  
 *options*  
 Um parâmetro opcional que retorna uma descrição das colunas do conjunto de resultados de cursor. * as opções exigem o valor de entrada **int** a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Opção SCROLL. *scrollopt* é um parâmetro opcional que requer um dos seguintes valores de entrada **int** .  
  
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
  
 Devido à possibilidade de que a opção solicitada não seja apropriada para o cursor definido por * \<stmt>*, esse parâmetro serve como entrada e saída. Nesses casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui um tipo apropriado e modifica esse valor.  
  
 *ccopt*  
 Opção de controle de simultaneidade. *ccopt* é um parâmetro opcional que requer um dos seguintes valores de entrada **int** .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (anteriormente conhecido como LOCKCC)|  
|0x0004|**Otimista** (anteriormente conhecido como OPTCC)|  
|0x0008|OPTIMISTIC (anteriormente conhecido como OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Assim como *scrollpt*com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] scrollpt, o pode atribuir um valor diferente daquele solicitado.  
  
 *linhas*  
 É um parâmetro opcional que significa o número de linhas de buffer de busca a ser usado com AUTO_FETCH. O padrão é 20 linhas. o *número de linhas* se comporta de forma diferente quando atribuído como um valor de entrada versus um valor de retorno.  
  
|Como valor de entrada|Como valor de retorno|  
|--------------------|---------------------|  
|Quando AUTO_FETCH é especificado com FAST_FORWARD os cursores de *linhas representa o* número de linhas a serem colocadas no buffer de busca.|Representa o número de linhas no conjunto de resultados. Quando o valor de AUTO_FETCH *scrollopt* é especificado, *RowCount* retorna o número de linhas que foram buscadas no buffer de busca.|  

*parameter_name* Designe um ou mais nomes de parâmetro, conforme definido no argumento params.  Deve haver um parâmetro fornecido para cada parâmetro incluído em params. Esse argumento não é necessário quando a instrução Transact-SQL ou o lote em params não tem parâmetros definidos.
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Se params retornar um valor nulo, a instrução não será parametrizada.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_cursoropen](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_cursorexecute](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_cursorprepare](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_cursorfetch](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
