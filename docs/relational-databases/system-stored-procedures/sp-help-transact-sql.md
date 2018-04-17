---
title: sp_help (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help
- sp_help_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help
ms.assetid: 913cd5d4-39a3-4a4b-a926-75ed32878884
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: be83dee5f8f4fa4f9e5893bc71964dd3a8df4e3c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelp-transact-sql"></a>sp_help (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Relata informações sobre um objeto de banco de dados (qualquer objeto listado no **sysobjects** exibição de compatibilidade), um tipo de dados definido pelo usuário ou um tipo de dados.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help [ [ @objname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@objname=**] **'***name***'**  
 É o nome de qualquer objeto, em **sysobjects** ou digite quaisquer dados definidos pelo usuário a **systypes** tabela. *nome* é **nvarchar (**776**)**, com um padrão NULL. Nomes de banco de dados não são aceitáveis.  Dois ou três nomes de parte devem ser delimitados, como 'Person.AddressType' ou [Person.AddressType].   
   
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Os conjuntos de resultados retornados dependem se *nome* é especificado, quando ele é especificado e o objeto de banco de dados é.  
  
1.  Se **sp_help** é executado sem argumentos, as informações de resumo de objetos de todos os tipos existentes no banco de dados atual serão retornadas.  
  
    |Nome da coluna|Tipo de dados|Description|  
    |-----------------|---------------|-----------------|  
    |**Nome**|**nvarchar(**128**)**|Nome do objeto|  
    |**Proprietário**|**nvarchar(**128**)**|Proprietário do objeto (esta é a entidade de segurança do banco de dados que é a proprietária deste objeto. O padrão é o proprietário do esquema que contém o objeto.)|  
    |**object_type**|**nvarchar (**31**)**|Tipo de objeto|  
  
2.  Se *nome* é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados ou tipo de dados definido pelo usuário, **sp_help** retorna o conjunto de resultados.  
  
    |Nome da coluna|Tipo de dados|Description|  
    |-----------------|---------------|-----------------|  
    |**type_name**|**nvarchar(**128**)**|Nome do tipo de dados.|  
    |**Storage_type**|**nvarchar(**128**)**|Nome do tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
    |**Comprimento**|**smallint**|O comprimento físico do tipo de dados (em bytes).|  
    |**prec**|**Int**|Precisão (número total de dígitos).|  
    |**Escala**|**Int**|Número de dígitos à direita da casa decimal.|  
    |**Anulável**|**varchar (**35**)**|Indica se valores NULL são permitidos: Sim ou Não.|  
    |**default_name**|**nvarchar(**128**)**|Nome de uma associação padrão para esse tipo.<br /><br /> NULL = Nenhum padrão é associado.|  
    |**rule_name**|**nvarchar(**128**)**|Nome de uma associação de regra para esse tipo.<br /><br /> NULL = Nenhum padrão é associado.|  
    |**Agrupamento**|**sysname**|Agrupamento do tipo de dados. NULL para tipos de dados de não caracteres.|  
  
3.  Se *nome* é qualquer objeto de banco de dados que não seja um tipo de dados **sp_help** retorna esse resultado conjuntos de resultados de conjunto e também adicionais, com base no tipo de objeto especificado.  
  
    |Nome da coluna|Tipo de dados|Description|  
    |-----------------|---------------|-----------------|  
    |**Nome**|**nvarchar(**128**)**|Nome da tabela|  
    |**Proprietário**|**nvarchar(**128**)**|Proprietário da tabela|  
    |**Tipo**|**nvarchar (**31**)**|Tipo de tabela|  
    |**Created_datetime**|**datetime**|Tabela de data criada|  
  
     Dependendo do objeto de banco de dados especificado, **sp_help** retorna conjuntos de resultados adicionais.  
  
     Se *nome* é uma tabela do sistema, a tabela de usuário ou a exibição, **sp_help** retorna os seguintes conjuntos de resultados. Entretanto, o conjunto de resultados que descreve onde o arquivo de dados está localizado em um grupo de arquivos não é retornado para uma exibição.  
  
    -   Conjunto de resultados adicionais retornado em objetos de coluna:  
  
        |Nome da coluna|Tipo de dados|Description|  
        |-----------------|---------------|-----------------|  
        |**nome da coluna**|**nvarchar(**128**)**|Nome da coluna.|  
        |**Tipo**|**nvarchar(**128**)**|Tipo de dados da coluna.|  
        |**Computado**|**varchar (**35**)**|Indica se os valores na coluna são computados: Sim ou Não.|  
        |**Comprimento**|**Int**|Comprimento da coluna em bytes.<br /><br /> Observação: Se o tipo de dados de coluna é um tipo de valor grande (**varchar (max)**, **nvarchar (max)**, **varbinary (max)**, ou **xml**), o valor será Exibir como -1.|  
        |**prec**|**char (**5**)**|Precisão da coluna.|  
        |**Escala**|**char (**5**)**|Escala da coluna.|  
        |**Anulável**|**varchar (**35**)**|Indica se valores NULL são permitidos na coluna: Sim ou Não.|  
        |**TrimTrailingBlanks**|**varchar (**35**)**|Exclui os espaços em branco à direita. Retorna Sim ou Não.|  
        |**FixedLenNullInSource**|**varchar (**35**)**|Somente para compatibilidade com versões anteriores.|  
        |**Agrupamento**|**sysname**|Agrupamento da coluna. NULL para tipos de dados não são de caractere.|  
  
    -   Conjunto de resultados adicionais retornado em colunas de identidade:  
  
        |Nome da coluna|Tipo de dados|Description|  
        |-----------------|---------------|-----------------|  
        |**Identidade**|**nvarchar(**128**)**|Nome da coluna cujo tipo de dados é declarado como identidade.|  
        |**Semente**|**numeric**|O valor inicial para a coluna de identidade.|  
        |**Incremento**|**numeric**|Incremento a ser usado para obter valores nesta coluna.|  
        |**Não para replicação**|**Int**|A propriedade IDENTITY não é imposta quando um logon de replicação, como **sqlrepl**, insere dados na tabela:<br /><br /> 1 = True<br /><br /> 0 = False|  
  
    -   Conjunto de resultados adicionais retornado em colunas:  
  
        |Nome da coluna|Tipo de dados|Description|  
        |-----------------|---------------|-----------------|  
        |**RowGuidCol**|**sysname**|Nome da coluna de identificador exclusivo global.|  
  
    -   Conjunto de resultados adicionais retornado em grupos de arquivos:  
  
        |Nome da coluna|Tipo de dados|Description|  
        |-----------------|---------------|-----------------|  
        |**Data_located_on_filegroup**|**nvarchar(**128**)**|Grupo de arquivos no qual os dados estão localizados: Primário, Secundário ou Log de Transações.|  
  
    -   Conjunto de resultados adicionais retornado em índices:  
  
        |Nome da coluna|Tipo de dados|Description|  
        |-----------------|---------------|-----------------|  
        |**index_name**|**sysname**|Nome do índice.|  
        |**index_description**|**varchar (**210**)**|Descrição do índice.|  
        |**index_keys**|**nvarchar (**2078**)**|Nomes de coluna nas quais o índice é criado. Retorna NULL para índices columnstore xVelocity de memória otimizada.|  
  
    -   Conjunto de resultados adicionais retornado em restrições:  
  
        |Nome da coluna|Tipo de dados|Description|  
        |-----------------|---------------|-----------------|  
        |**Constraint_Type**|**nvarchar (**146**)**|Tipo de restrição.|  
        |**constraint_name**|**nvarchar(**128**)**|Nome da restrição.|  
        |**delete_action**|**nvarchar (**9**)**|Indica se a ação DELETE é: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT ou N/A.<br /><br /> Aplicável somente para restrições FOREIGN KEY.|  
        |**update_action**|**nvarchar (**9**)**|Indica se a ação UPDATE é: NO_ACTION, CASCADE, SET_NULL, SET_DEFAULT ou N/A.<br /><br /> Aplicável somente para restrições FOREIGN KEY.|  
        |**status_enabled**|**varchar (**8**)**|Indica se a restrição está habilitada: Habilitado, Desabilitado ou N/A.<br /><br /> Aplicável somente para restrições CHECK e FOREIGN KEY.|  
        |**status_for_replication**|**varchar (**19**)**|Indica se a restrição é para replicação.<br /><br /> Aplicável somente para restrições CHECK e FOREIGN KEY.|  
        |**constraint_keys**|**nvarchar (**2078**)**|Os nomes das colunas que compõem a restrição ou, no caso de padrões e regras, do texto que define o padrão ou a regra.|  
  
    -   Conjunto de resultados adicionais retornado em objetos de referência:  
  
        |Nome da coluna|Tipo de dados|Description|  
        |-----------------|---------------|-----------------|  
        |**A tabela é referenciada por**|**nvarchar (**516**)**|Identifica outros objetos de banco de dados que referenciam a tabela.|  
  
    -   Conjunto de resultados adicionais retornado em procedimentos armazenados, funções ou procedimentos armazenados estendidos.  
  
        |Nome da coluna|Tipo de dados|Description|  
        |-----------------|---------------|-----------------|  
        |**parameter_name**|**nvarchar(**128**)**|Nome de parâmetro de procedimento armazenado.|  
        |**Tipo**|**nvarchar(**128**)**|Tipo de dados do parâmetro de procedimento armazenado.|  
        |**Comprimento**|**smallint**|Comprimento máximo de armazenamento físico, em bytes.|  
        |**prec**|**Int**|Precisão ou número total de dígitos.|  
        |**Escala**|**Int**|Número de dígitos à direita da vírgula decimal.|  
        |**Param_order**|**smallint**|Ordem do parâmetro.|  
  
## <a name="remarks"></a>Remarks  
 O **sp_help** procedimento procurará um objeto de banco de dados atual.  
  
 Quando *nome* não for especificado, **sp_help** listas de nomes de objetos, proprietários e tipos de objeto para todos os objetos no banco de dados atual. **sp_helptrigger** fornece informações sobre gatilhos.  
  
 **sp_help** expõe apenas as colunas de índices; portanto, ele não expõe informações sobre índices XML ou índices espaciais.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . O usuário deve ter pelo menos uma permissão *objname*. Para exibir as chaves de restrição de coluna, padrões ou regras, você deve ter a permissão VIEW DEFINITION na tabela.  
  
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
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpindex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sysobjects &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)  
  
  
