---
title: sp_help (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fb5e9a1ab72140a08423fa50c10eeb1f2d06ad79
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909092"
---
# <a name="sp_help-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Relata informações sobre um objeto Database (qualquer objeto listado na exibição de compatibilidade **Sys. sysobjects** ), um tipo de dados definido pelo usuário ou um tipo de dados.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'name'` é o nome de qualquer objeto, em **sysobjects** ou qualquer tipo de dados definido pelo usuário na tabela **systypes** . *Name* é **nvarchar (** 776 **)** , com um padrão de NULL. Nomes de banco de dados não são aceitáveis.  Dois ou três nomes de parte devem ser delimitados, como 'Person.AddressType' ou [Person.AddressType].   
   
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Os conjuntos de resultados retornados dependem se o *nome* é especificado, quando é especificado, e qual é o objeto de banco de dados.  
  
1.  Se **sp_help** for executado sem argumentos, serão retornadas informações resumidas de objetos de todos os tipos existentes no banco de dados atual.  
  
    |Nome da coluna|Tipo de dados|Descrição|  
    |-----------------|---------------|-----------------|  
    |**Nome**|**nvarchar(** 128 **)**|Nome do objeto|  
    |**Proprietário**|**nvarchar(** 128 **)**|Proprietário do objeto (esta é a entidade de segurança do banco de dados que é a proprietária deste objeto. O padrão é o proprietário do esquema que contém o objeto.)|  
    |**Object_type**|**nvarchar(** 31 **)**|Tipo de objeto|  
  
2.  Se *Name* for um tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um tipo de dados definido pelo usuário, **sp_help** retornará esse conjunto de resultados.  
  
    |Nome da coluna|Tipo de dados|Descrição|  
    |-----------------|---------------|-----------------|  
    |**Type_name**|**nvarchar(** 128 **)**|Nome do tipo de dados.|  
    |**Storage_type**|**nvarchar(** 128 **)**|Nome do tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
    |**Comprimento**|**smallint**|O comprimento físico do tipo de dados (em bytes).|  
    |**Prec**|**int**|Precisão (número total de dígitos).|  
    |**Escala**|**int**|Número de dígitos à direita da casa decimal.|  
    |**Permite valor nulo**|**varchar(** 35 **)**|Indica se valores NULL são permitidos: Sim ou Não.|  
    |**Default_name**|**nvarchar(** 128 **)**|Nome de uma associação padrão para esse tipo.<br /><br /> NULL = Nenhum padrão é associado.|  
    |**Rule_name**|**nvarchar(** 128 **)**|Nome de uma associação de regra para esse tipo.<br /><br /> NULL = Nenhum padrão é associado.|  
    |**Ordenação**|**sysname**|Ordenação do tipo de dados. NULL para tipos de dados de não caracteres.|  
  
3.  Se *Name* for qualquer objeto Database diferente de um tipo de dados, **sp_help** retornará esse conjunto de resultados e também conjuntos de resultados adicionais, com base no tipo de objeto especificado.  

    |Nome da coluna|Tipo de dados|Descrição|  
    |-----------------|---------------|-----------------|  
    |**Nome**|**nvarchar(** 128 **)**|Nome da tabela|  
    |**Proprietário**|**nvarchar(** 128 **)**|Proprietário da tabela|  
    |**Tipo**|**nvarchar(** 31 **)**|Tipo de tabela|  
    |**Created_datetime**|**datetime**|Tabela de data criada|  
  
     Dependendo do objeto de banco de dados especificado, **sp_help** retorna conjuntos de resultados adicionais.  
  
     Se *nome* for uma tabela do sistema, uma tabela de usuário ou uma exibição, **sp_help** retornará os seguintes conjuntos de resultados. Entretanto, o conjunto de resultados que descreve onde o arquivo de dados está localizado em um grupo de arquivos não é retornado para uma exibição.  
  
    -   Conjunto de resultados adicionais retornado em objetos de coluna:  
  
        |Nome da coluna|Tipo de dados|Descrição|  
        |-----------------|---------------|-----------------|  
        |**Column_name**|**nvarchar(** 128 **)**|Nome da coluna.|  
        |**Tipo**|**nvarchar(** 128 **)**|Tipo de dados da coluna.|  
        |**Computada**|**varchar(** 35 **)**|Indica se os valores na coluna são computados: Sim ou Não.|  
        |**Comprimento**|**int**|Comprimento da coluna em bytes.<br /><br /> Observação: se o tipo de dados da coluna for um tipo de valor grande (**varchar (max)** , **nvarchar (max)** , **varbinary (max)** ou **XML**), o valor será exibido como-1.|  
        |**Prec**|**char(** 5 **)**|Precisão da coluna.|  
        |**Escala**|**char(** 5 **)**|Escala de coluna.|  
        |**Permite valor nulo**|**varchar(** 35 **)**|Indica se valores NULL são permitidos na coluna: Sim ou Não.|  
        |**TrimTrailingBlanks**|**varchar(** 35 **)**|Exclui os espaços em branco à direita. Retorna Sim ou Não.|  
        |**FixedLenNullInSource**|**varchar(** 35 **)**|Somente para compatibilidade com versões anteriores.|  
        |**Ordenação**|**sysname**|Ordenação da coluna. NULO para tipos de dados não caracteres.|  
  
    -   Conjunto de resultados adicionais retornado em colunas de identidade:  
  
        |Nome da coluna|Tipo de dados|Descrição|  
        |-----------------|---------------|-----------------|  
        |**Identidade**|**nvarchar(** 128 **)**|Nome da coluna cujo tipo de dados é declarado como identidade.|  
        |**Semente**|**numeric**|O valor inicial para a coluna de identidade.|  
        |**Incremento**|**numeric**|Incremento a ser usado para obter valores nesta coluna.|  
        |**Não para replicação**|**int**|A propriedade IDENTITY não é imposta quando um logon de replicação, como **sqlrepl**, insere dados na tabela:<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   Conjunto de resultados adicionais retornado em colunas:  
  
        |Nome da coluna|Tipo de dados|Descrição|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|Nome da coluna de identificador exclusivo global.|  
  
    -   Conjunto de resultados adicionais retornado em grupos de arquivos:  
  
        |Nome da coluna|Tipo de dados|Descrição|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar(** 128 **)**|Grupo de arquivos no qual os dados estão localizados: Primário, Secundário ou Log de Transações.|  
  
    -   Conjunto de resultados adicionais retornado em índices:  
  
        |Nome da coluna|Tipo de dados|Descrição|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|Nome do índice.|  
        |**Index_description**|**varchar(** 210 **)**|Descrição do índice.|  
        |**index_keys**|**nvarchar(** 2078 **)**|Nomes de coluna nas quais o índice é criado. Retorna NULL para índices columnstore xVelocity de memória otimizada.|  
  
    -   Conjunto de resultados adicionais retornado em restrições:  
  
        |Nome da coluna|Tipo de dados|Descrição|  
        |-----------------|---------------|-----------------|  
        |**constraint_type**|**nvarchar(** 146 **)**|Tipo de restrição.|  
        |**constraint_name**|**nvarchar(** 128 **)**|Nome da restrição.|  
        |**delete_action**|**nvarchar(** 9 **)**|Indica se a ação DELETE é: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT ou N/A.<br /><br /> Aplicável somente para restrições FOREIGN KEY.|  
        |**update_action**|**nvarchar(** 9 **)**|Indica se a ação UPDATE é: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT ou N/A.<br /><br /> Aplicável somente para restrições FOREIGN KEY.|  
        |**status_enabled**|**varchar(** 8 **)**|Indica se a restrição está habilitada: Habilitado, Desabilitado ou N/A.<br /><br /> Aplicável somente para restrições CHECK e FOREIGN KEY.|  
        |**status_for_replication**|**varchar(** 19 **)**|Indica se a restrição é para replicação.<br /><br /> Aplicável somente para restrições CHECK e FOREIGN KEY.|  
        |**constraint_keys**|**nvarchar(** 2078 **)**|Os nomes das colunas que compõem a restrição ou, no caso de padrões e regras, do texto que define o padrão ou a regra.|  
  
    -   Conjunto de resultados adicionais retornado em objetos de referência:  
  
        |Nome da coluna|Tipo de dados|Descrição|  
        |-----------------|---------------|-----------------|  
        |**A tabela é referenciada por**|**nvarchar(** 516 **)**|Identifica outros objetos de banco de dados que referenciam a tabela.|  
  
    -   Conjunto de resultados adicionais retornado em procedimentos armazenados, funções ou procedimentos armazenados estendidos.  
  
        |Nome da coluna|Tipo de dados|Descrição|  
        |-----------------|---------------|-----------------|  
        |**Parameter_name**|**nvarchar(** 128 **)**|Nome de parâmetro de procedimento armazenado.|  
        |**Tipo**|**nvarchar(** 128 **)**|Tipo de dados do parâmetro de procedimento armazenado.|  
        |**Comprimento**|**smallint**|Comprimento máximo de armazenamento físico, em bytes.|  
        |**Prec**|**int**|Precisão ou número total de dígitos.|  
        |**Escala**|**int**|Número de dígitos à direita da vírgula decimal.|  
        |**Param_order**|**smallint**|Ordem do parâmetro.|  
  
## <a name="remarks"></a>Remarks  
 O procedimento **sp_help** procura um objeto somente no banco de dados atual.  
  
 Quando o *nome* não é especificado, **sp_help** lista os nomes de objeto, os proprietários e os tipos de objeto para todos os objetos no banco de dados atual. **sp_helptrigger** fornece informações sobre gatilhos.  
  
 **sp_help** expõe apenas colunas de índice ordenáveis; Portanto, ele não expõe informações sobre índices XML ou índices espaciais.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . O usuário deve ter pelo menos uma permissão em *objname*. Para exibir as chaves de restrição de coluna, padrões ou regras, você deve ter a permissão VIEW DEFINITION na tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-information-about-all-objects"></a>A. Retornando informações sobre todos os objetos  
 O exemplo a seguir lista informações sobre cada objeto no banco de dados `master`.  
  
```  
USE master;  
GO  
EXEC sp_help;  
GO  
```  
  
### <a name="b-returning-information-about-a-single-object"></a>B. Retornando informações sobre um único objeto  
 O exemplo a seguir exibe informações sobre a tabela `Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help 'Person.Person';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Mecanismo de banco de dados procedimentos &#40;armazenados  Transact-&#41; SQL](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
 [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sysobjects &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
