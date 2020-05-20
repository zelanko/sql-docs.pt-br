---
title: sp_cursorexecute (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b3152e180ceb1681f259f0b1cfcfbccce224a68c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831730"
---
# <a name="sp_cursorexecute-transact-sql"></a>sp_cursorexecute (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria e popula um cursor com base no plano de execução criado por sp_cursorprepare. Esse procedimento, combinado com sp_cursorprepare, tem a mesma função que sp_cursoropen, mas é dividido em duas fases. sp_cursorexecute é invocado especificando ID = 4 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *prepared_handle*  
 É o valor do *identificador* de instrução preparado retornado por sp_cursorprepare. *prepared_handle* é um parâmetro necessário que chama um valor de entrada **int** .  
  
 *cursor*  
 É o identificador de cursor gerado pelo SQL Server. *cursor* é um parâmetro necessário que deve ser fornecido em todos os procedimentos subsequentes que atuam no cursor, como sp_cursorfetch  
  
 *scrollopt*  
 Opção de rolagem. *scrollopt* é um parâmetro opcional que requer um valor de entrada **int** . O parâmetro sp_cursorexecute*scrollopt* tem as mesmas opções de valor que aquelas para sp_cursoropen.  
  
> [!NOTE]  
>  Não há suporte para o valor PARAMETERIZED_STMT.  
  
> [!IMPORTANT]  
>  Se um valor de *scrollopt* não for especificado, o valor padrão será conjunto de chaves, independentemente do valor de *scrollopt* especificado em sp_cursorprepare.  
  
 *ccopt*  
 Opção de controle de moeda. *ccopt* é um parâmetro opcional que requer um valor de entrada **int** . O parâmetro sp_cursorexecute*ccopt* tem as mesmas opções de valor que aquelas para sp_cursoropen.  
  
> [!IMPORTANT]  
>  Se um valor de *ccopt* não for especificado, o valor padrão será otimista, independentemente do valor de *ccopt* especificado em sp_cursorprepare.  
  
 *linhas*  
 É um parâmetro opcional que significa o número de linhas de buffer de busca a ser usado com AUTO_FETCH. O padrão é 20 linhas. o *número de linhas* se comporta de forma diferente quando atribuído como um valor de entrada versus um valor de retorno.  
  
|Como valor de entrada|Como valor de retorno|  
|--------------------|---------------------|  
|Quando AUTO_FETCH é especificado com FAST_FORWARD os cursores de *linhas representa o* número de linhas a serem colocadas no buffer de busca.|Representa o número de linhas no conjunto de resultados. Quando o valor de AUTO_FETCH *scrollopt* é especificado, *RowCount* retorna o número de linhas que foram buscadas no buffer de busca.|  
  
 *bound_param*  
 Significa o uso opcional de parâmetros adicionais.  
  
> [!NOTE]  
>  Quaisquer parâmetros após o quinto são passados para o plano de instrução como parâmetros de entrada.  
  
## <a name="code-return-value"></a>Valor de retorno do código  
 *RowCount* pode retornar os valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|-1|Número de linhas desconhecidas.|  
|-n|Uma população assíncrona está em vigor.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="scrollopt-and-ccopt-parameters"></a>Parâmetros scrollopt e ccopt  
 *scrollopt* e *ccopt* são úteis quando os planos em cache são preempção para o cache do servidor, o que significa que o identificador preparado que identifica a instrução deve ser recompilado. Os valores de parâmetro *scrollopt* e *ccopt* devem corresponder aos valores enviados na solicitação original para sp_cursorprepare.  
  
> [!NOTE]  
>  PARAMETERIZED_STMT não deve ser atribuído a *scrollopt*.  
  
 A falha ao fornecer valores correspondentes resultará na recompilação dos planos, negando as operações de preparação e execução.  
  
## <a name="rpc-and-tds-considerations"></a>Considerações sobre RPC e TDS  
 O sinalizador de entrada RPC RETURN_METADATA pode ser definido como 1 para solicitar que os metadados da lista de seleção de cursor sejam retornados no fluxo TDS.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_cursoropen](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_cursorfetch](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
