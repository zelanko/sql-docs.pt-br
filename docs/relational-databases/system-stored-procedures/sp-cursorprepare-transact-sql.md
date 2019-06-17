---
title: sp_cursorprepare (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1f26ada2f116d684091f7e5e928d04e3530567f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724121"
---
# <a name="spcursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Compila a instrução de cursor ou processa em lotes em um plano de execução, mas não cria o cursor. A instrução compilada pode ser usada posteriormente por sp_cursorexecute. Neste procedimento, associado a sp_cursorexecute, tem a mesma função que sp_cursoropen, mas é dividido em duas fases. sp_cursorprepare é invocado pela especificação de ID = 3 em um pacote do protocolo TDS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *prepared_handle*  
 Um SQL Server preparado e gerado pelo *manipular* identificador que retorna um valor inteiro.  
  
> [!NOTE]  
>  *prepared_handle* é fornecido subsequentemente a um procedimento sp_cursorexecute para abrir um cursor. Quando um identificador é criado, ele existe até que você faça logoff ou remova-o explicitamente por meio de um procedimento sp_cursorunprepare.  
  
 *params*  
 Identifica instruções parametrizadas. O *params* definição de variáveis é substituída para marcadores de parâmetro na instrução. *params* é um parâmetro obrigatório que chama uma **ntext**, **nchar**, ou **nvarchar** valor de entrada. Insira um valor NULL se a instrução não for parametrizada.  
  
> [!NOTE]  
>  Use uma **ntext** cadeia de caracteres como a entrada de valor quando *stmt* é parametrizado e o *scrollopt* valor PARAMETERIZED_STMT for ON.  
  
 *stmt*  
 Define o conjunto de resultados do cursor. O *stmt* parâmetro é obrigatório e chamadas para um **ntext**, **nchar** ou **nvarchar** valor de entrada.  
  
> [!NOTE]  
>  As regras para especificar o *stmt* valor são as mesmas de sp_cursoropen, com exceção de que o *stmt* tipo de dados de cadeia de caracteres deve ser **ntext**.  
  
 *Opções*  
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
  
 Porque o valor solicitado talvez não seja apropriado para o cursor definido por *stmt*, este parâmetro serve como entrada e saída. Nesses casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui um valor apropriado.  
  
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
  
 Assim como acontece com *scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode atribuir um valor diferente do solicitado.  
  
## <a name="remarks"></a>Comentários  
 O parâmetro de status RPC é um dos seguintes:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Êxito|  
|0x0001|Failure|  
|1FF6|Não foi possível retornar metadados.<br /><br /> Observação: A razão para isso é que a instrução não produz um conjunto de resultados; Por exemplo, é uma instrução INSERT ou DDL.|  
  
## <a name="examples"></a>Exemplos  
 Quando *stmt* é parametrizado e o *scrollopt* valor PARAMETERIZED_STMT for ON, o formato da cadeia de caracteres é da seguinte maneira:  
  
 {  *\<nome da variável local > * *\<tipo de dados >* } [,... *n* ]  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
