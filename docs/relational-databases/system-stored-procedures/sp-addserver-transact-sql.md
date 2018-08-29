---
title: sp_addserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addserver
- sp_addserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addserver
- renaming servers
- machine names [SQL Server]
- computer names
ms.assetid: 160a6b29-5e80-44ab-80ec-77d4280f627c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1727c6388cf70b5df3a620b281cefffb701ac4e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024426"
---
# <a name="spaddserver-transact-sql"></a>sp_addserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define o nome da instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o computador que hospeda [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é renomeado, use **sp_addserver** para informar a instância da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] do novo nome do computador. Esse procedimento deve ser executado em todas as instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] hospedadas no computador. O nome da instância de [!INCLUDE[ssDE](../../includes/ssde-md.md)] não pode ser alterado. Para alterar o nome de instância de uma instância nomeada, instale uma nova instância com o nome desejado, desanexe os arquivos de bancos de dados da instância antiga, anexe os bancos de dados à nova instância e remova a instância antiga. Como alternativa, você pode criar um nome de alias de cliente no computador cliente, redirecionando a conexão para um nome de servidor e de instância diferente ou para uma combinação **server:port** sem alterar o nome da instância no computador do servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addserver [ @server = ] 'server' ,  
     [ @local = ] 'local'   
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@server =** ] **'***server***'**  
 É o nome do servidor. Os nomes de servidor devem ser exclusivos e seguir as regras de nomes do computador do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, embora não sejam permitidos espaços. *server* é **sysname**, sem padrão.  
  
 Quando várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão instalados em um computador, uma instância funciona como se ele está em um servidor separado. Especificar uma instância nomeada consultando *server* como *NomedoServidor \ NomedaInstância*.  
  
 [  **@local =** ] **'LOCAL'**  
 Especifica se o servidor que está sendo adicionado é um servidor local. **@local** está **varchar(10)**, com um padrão NULL. Especificando **@local** como **LOCAL** define **@server** como o nome do servidor local e faz com que o @@SERVERNAME função para retornar o valor dos *server*.  
  
 A Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define essa variável como o nome do computador durante a instalação. Por padrão, o nome do computador é os maneira como os usuários se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem a necessidade de configuração adicional.  
  
 A definição local entra em vigor apenas depois de o [!INCLUDE[ssDE](../../includes/ssde-md.md)] ser reiniciado. Apenas um servidor local pode ser definido em cada instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 [  **@duplicate_ok =** ] **'duplicate_OK'**  
 Especifica se um nome de servidor duplicado é permitido. **@duplicate_OK** está **varchar(13)**, com um padrão NULL. **@duplicate_OK** só pode ter o valor **duplicate_OK** ou nulo. Se **duplicate_OK** for especificado e o nome do servidor que está sendo adicionado já existe, nenhum erro será gerado. Se não forem usados parâmetros nomeados, **@local** deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Para definir ou limpar opções de servidor, use **sp_serveroption**.  
  
 **sp_addserver** não pode ser usado dentro de uma transação definida pelo usuário.  
  
 Usando o **sp_addserver** para adicionar um servidor remoto foi descontinuado. Em vez disso, use [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) .  
  
## <a name="permissions"></a>Permissões  
 Exige uma associação na função de servidor fixa **setupadmin** .  
  
## <a name="examples"></a>Exemplos  
 A exemplo a seguir altera a [!INCLUDE[ssDE](../../includes/ssde-md.md)] entrada para o nome do computador que hospeda [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para `ACCOUNTS`.  
  
```  
sp_addserver 'ACCOUNTS', 'local';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Renomear um computador que hospeda uma instância autônoma do SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
