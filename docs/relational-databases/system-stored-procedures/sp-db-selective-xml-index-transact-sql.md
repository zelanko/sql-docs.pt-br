---
title: sp_db_selective_xml_index (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
ms.assetid: 017301a2-4a23-4e68-82af-134f3d4892b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9b1752b5e567c2a26080422874e5bf6e31bc568
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528598"
---
# <a name="spdbselectivexmlindex-transact-sql"></a>sp_db_selective_xml_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Habilita e desabilita a funcionalidade seletiva do índice XML em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se for chamado sem qualquer parâmetro, o procedimento armazenado retornará 1 se o índice XML seletivo estiver habilitado em um banco de dados específico.  
  
> [!NOTE]  
>  Para desabilitar o índice XML seletivo usando esse procedimento armazenado, o banco de dados deve ser colocado em modo de recuperação simples usando o [opções ALTER DATABASE SET &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) comando.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ db_name = ] 'db_name'` O nome do banco de dados para habilitar ou desabilitar o índice XML seletivo. Se *db_name* for NULL, o banco de dados atual será assumido.  
  
`[ @action = ] 'action'` Determina se é habilitar ou desabilitar o índice. Se outro valor, exceto 'on', 'true', 'off' ou 'false' é passado, um erro será gerado.  
  
```  
  
Allowed values: 'on', 'off', 'true', 'false'  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **1** se o índice XML seletivo está habilitado em um determinado banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-enable-selective-xml-index-functionality"></a>A. Habilitar a funcionalidade seletiva de índice XML  
 O exemplo a seguir habilita o índice XML seletivo no banco de dados atual.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'on';  
GO  
```  
  
 O exemplo a seguir habilita o índice XML seletivo no banco de dados AdventureWorks2012.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'true';  
GO  
```  
  
### <a name="b-disable-selective-xml-index-functionality"></a>B. Desabilitar a funcionalidade seletiva de índice XML  
 O exemplo a seguir desabilita o índice XML seletivo no banco de dados atual.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'off';  
GO  
```  
  
 O exemplo a seguir desabilita o índice XML seletivo no banco de dados AdventureWorks2012.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'false';  
GO  
```  
  
### <a name="c-detect-if-selective-xml-index-is-enabled"></a>C. Detectar se o índice XML seletivo está habilitado  
 O exemplo a seguir detecta se o índice XML seletivo está habilitado. Retorna 1 se o índice XML seletivo está habilitado.  
  
```  
EXECUTE sys.sp_db_selective_xml_index;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
