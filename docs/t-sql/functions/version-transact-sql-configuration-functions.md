---
title: '@@VERSION (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: c9fc3634abc5ca23c96f46adf2a52881ee15c40c
ms.contentlocale: pt-br
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40version---transact-sql-configuration-functions"></a>& #x 40; & #x 40. Versão - Transact SQL funções de configuração
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de compilação e sistema para a instalação atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@VERSION  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Comentários  
 O @@VERSION resultados são apresentados como uma cadeia de caracteres nvarchar. Você pode usar o [SERVERPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/serverproperty-transact-sql.md) função para recuperar os valores de propriedade individuais.  
  
 Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as informações a seguir são retornadas.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Versão  
  
-   Arquitetura do processador  
  
-   Data de compilação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Instrução de direitos autorais  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edição  
  
-   Versão do sistema operacional  
  
 Para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as informações a seguir são retornadas.  
  
-   Edição - "Banco de Dados SQL do Windows Azure"  
  
-   Nível de produto - "(CTP)" ou "(RTM)"  
  
-   Versão do produto  
  
-   Data de compilação  
  
-   Instrução de direitos autorais  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-the-current-version-of-includessnoversionincludesssnoversion-mdmd"></a>R: retornar a versão atual do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O exemplo a seguir mostra o retorno das informações de versão da instalação atual.  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-includessdwincludesssdw-mdmd"></a>B. Retornar a versão atual do[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>Consulte também  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  


