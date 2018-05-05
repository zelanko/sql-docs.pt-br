---
title: sp_control_dbmasterkey_password (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c98b88b5e057dad432a178317b5255f0c0111a45
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spcontroldbmasterkeypassword-transact-sql"></a>sp_control_dbmasterkey_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona ou descarta uma credencial que contém a senha necessária para abrir uma chave mestra de banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>Argumentos  
 @db_name= N'*database_name*'  
 Especifica o nome do banco de dados associado a essa credencial. Não pode ser um banco de dados do sistema. *Database_Name* é **nvarchar**.  
  
 @password= N'*senha*'  
 Especifica a senha da chave mestra. *senha* é **nvarchar**.  
  
 @action= N'add'  
 Especifica que uma credencial para o banco de dados especificado será adicionada ao armazenamento de credenciais. A credencial conterá a senha da chave mestra de banco de dados. O valor passado para @action é **nvarchar**.  
  
 @action= N'drop'  
 Especifica que uma credencial para o banco de dados especificado será descartada do armazenamento de credenciais. O valor passado para @action é **nvarchar**.  
  
## <a name="remarks"></a>Remarks  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa de uma chave mestra de banco de dados para descriptografar ou criptografar uma chave, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta descriptografar a chave mestra de serviço da instância. Se a descriptografia falhar, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisará o repositório de credenciais em busca das credenciais de chave mestra que têm o mesmo GUID de família do banco de dados cuja chave mestra é necessária. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta descriptografar a chave mestra de banco de dados com cada credencial compatível até que a descriptografia obtenha êxito ou não haja mais credenciais.  
  
> [!CAUTION]  
>  Não habilite a descriptografia de failover de um banco de dados que deva permanecer inacessível o sa e outros principais de servidor altamente privilegiados. É possível configurar um banco de dados de forma que sua hierarquia fundamental não possa ser descriptografada pela chave mestra de serviço. Essa opção tem suporte como uma defesa para bancos de dados contendo informações criptografadas que não devem estar acessíveis ao sa ou outros principais de servidor altamente privilegiados. A criação de uma credencial de chave mestra para esse banco de dados remove a defesa, permitindo que o sa e outros principais de servidor altamente privilegiados descriptografem o banco de dados.  
  
 As credenciais criadas pelo uso de sp_control_dbmasterkey_password são visíveis no [master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md) exibição do catálogo. Os nomes das credenciais que são criadas para chaves mestras de banco de dados têm o seguinte formato: `##DBMKEY_<database_family_guid>_<random_password_guid>##`. A senha é armazenada como o segredo de credencial. Para cada senha adicionada ao repositório de credenciais há uma linha em sys.credentials.  
  
 Não é possível usar sp_control_dbmasterkey_password ao criar uma credencial para os seguintes bancos de dados do sistema: mestre, modelo, msdbou tempdb.  
  
 sp_control_dbmasterkey_password não verifica se a senha pode abrir a chave mestra do banco de dados especificado.  
  
 Se você especificar uma senha que já esteja armazenada em uma credencial para o banco de dados especificado, sp_control_dbmasterkey_password falhará.  
  
> [!NOTE]  
>  Dois bancos de dados de instâncias de servidor diferentes podem compartilhar o mesmo GUID de família. Se isso acontecer, os bancos de dados compartilharão os mesmos registros de chave mestra no armazenamento de credenciais.  
  
 Os parâmetros passados a sp_control_dbmasterkey_password não são exibidos em rastreamentos.  
  
> [!NOTE]  
>  Quando você estiver usando a credencial que foi adicionada com o uso de sp_control_dbmasterkey_password para abrir a chave mestra do banco de dados, essa chave será criptografada novamente pela chave mestra de serviço. Se o banco de dados estiver no modo somente leitura, a operação de nova criptografia falhará e a chave mestra de banco de dados permanecerá não criptografada. Para o acesso subsequente à chave mestra de banco de dados, você deve usar a instrução OPEN MASTER KEY e uma senha. Para evitar o uso de uma senha, crie a credencial antes de mover o banco de dados para o modo somente leitura.  
  
 **Possível problema de compatibilidade com versões anteriores:** no momento, o procedimento armazenado não verifica se existe uma chave mestra. Isso é permitido para compatibilidade com versões anteriores, mas exibe um aviso. Este comportamento é preterido. Em uma versão futura, a chave mestra deve existir e a senha usada no procedimento armazenado **sp_control_dbmasterkey_password** deve ser a mesma senha usada para criptografar a chave mestra de banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>A. Criando uma credencial para a chave mestra AdventureWorks2012  
 O exemplo a seguir cria uma credencial para a chave mestra de banco de dados `AdventureWorks2012` e salva a senha de chave mestra como segredo na credencial. Como todos os parâmetros que são passados para `sp_control_dbmasterkey_password` devem ser do tipo de dados **nvarchar**, as cadeias de caracteres de texto são convertidas com o operador de conversão `N`.  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'add';  
GO  
```  
  
### <a name="b-dropping-a-credential-for-a-database-master-key"></a>B. Removendo uma credencial para uma chave mestra de banco de dados  
 O exemplo a seguir remove a credencial criada no exemplo A. Observe que todos os parâmetros são necessários, inclusive a senha.  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'drop';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
