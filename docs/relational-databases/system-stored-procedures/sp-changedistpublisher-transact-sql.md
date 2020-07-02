---
title: sp_changedistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8aec9e25008c8dfe3b14bbe838f8122bb93fb756
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717409"
---
# <a name="sp_changedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera as propriedades do Publicador de distribuição. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do editor. o *Publicador* é **sysname**, sem padrão.  
  
`[ @property = ] 'property'`É uma propriedade a ser alterada para o Publicador fornecido. a *Propriedade* é **sysname** e pode ser um desses valores.  
  
`[ @value = ] 'value'`É o valor para a propriedade fornecida. o *valor* é **nvarchar (255)**, com um padrão de NULL.  
  
`[ @storage_connection_string = ] 'storage_connection_string'`É necessário para a instância gerenciada do banco de dados SQL, deve corresponder à chave de acesso do volume de armazenamento do banco de dados SQL do Azure. 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 Esta tabela descreve as propriedades de Publicadores e os valores para essas propriedades.  
  
|Propriedade|Valores|Descrição|  
|--------------|------------|-----------------|  
|**active**|**true**|Ativa o Publicador.|  
||**false**|Desativa o Publicador.|  
|**distribution_db**||Nome do banco de dados de distribuição.|  
|**entrar**||Nome de logon.|  
|**password**||Senha forte para o logon fornecido.|  
|**security_mode**|**1**|Use a Autenticação do Windows ao se conectar ao Publicador. *Isso não pode ser alterado para um não-* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Editor.*|  
||**0**|Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se conectar ao Publicador. *Isso não pode ser alterado para um não-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Editor.*|  
|**working_directory**||Diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação.|  
|NULL (padrão)||Todas as opções de *Propriedade* disponíveis são impressas.| 
|**storage_connection_string**| Chave de acesso | A chave de acesso para o diretório de trabalho quando o banco de dados é Instância Gerenciada do Banco de Dados SQL do Azure. 
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changedistpublisher** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_changedistpublisher**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar as propriedades do distribuidor e do Publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [&#41;&#40;Transact-SQL de sp_adddistpublisher](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdistpublisher](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
