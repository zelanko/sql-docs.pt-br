---
title: xp_cmdshell (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs: TSQL
helpviewer_keywords: xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: bb3fcd3cba2be225c4c45514b2dcbc021683c0db
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="xpcmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera um shell de comando do Windows e passa em uma cadeia de caracteres para execução. Qualquer saída é retornada como linhas de texto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *command_string* **'**  
 É a cadeia de caracteres que contém um comando a ser passado para o sistema operacional. *command_string* é **varchar(8000)** ou **nvarchar (4000)**, sem padrão. *command_string* não pode conter mais de um conjunto de aspas duplas. Um único par de aspas será necessário se qualquer espaço está presente nos caminhos de arquivo ou nomes de programa referenciados em *command_string*. Se você tiver dificuldade com espaços inseridos, considere o uso de nomes de arquivo FAT 8.3 como uma solução alternativa.  
  
 **no_output**  
 É um parâmetro opcional, especificando que nenhuma saída deve ser retornada ao cliente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A execução da seguinte instrução `xp_cmdshell` retorna uma lista de diretório do diretório atual.  
  
```  
EXEC xp_cmdshell 'dir *.exe';  
GO  
```  
  
 As linhas são retornadas em uma **nvarchar (255)** coluna. Se o **no_output** opção for usada, apenas o seguinte será retornado:  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>Comentários  
 O processo de Windows gerado por **xp_cmdshell** tem os mesmos direitos de segurança que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço.  
  
 **xp_cmdshell** opera de forma síncrona. O controle não é voltado ao chamador até que o comando do shell de comandos seja concluído.  
  
 **xp_cmdshell** pode ser habilitado e desabilitado usando o gerenciamento baseado em políticas ou executando **sp_configure**. Para obter mais informações, consulte [configuração da área de superfície](../../relational-databases/security/surface-area-configuration.md) e [opção de configuração de servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
> [!IMPORTANT]  
>  Se **xp_cmdshell** é executado dentro de um lote e retornar um erro, o lote falhará. É uma alteração de comportamento. Em versões anteriores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o lote continuaria a ser executado.  
  
## <a name="xpcmdshell-proxy-account"></a>Conta proxy xp_cmdshell  
 Quando ele é chamado por um usuário que não é um membro do **sysadmin** função fixa de servidor **xp_cmdshell** se conecta ao Windows usando o nome de conta e senha armazenadas na credencial chamada **# # xp_cmdshell_proxy_account # #**. Se essa credencial de proxy não existir, **xp_cmdshell** falhará.  
  
 A credencial da conta proxy pode ser criada executando **sp_xp_cmdshell_proxy_account**. Como argumentos, esse procedimento armazenado possui um nome de usuário e uma senha do Windows. Por exemplo, o comando a seguir cria uma credencial de proxy para o usuário de domínio do Windows `SHIPPING\KobeR` que possui a senha do Windows `sdfh%dkc93vcMt0`.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 Para obter mais informações, consulte [sp_xp_cmdshell_proxy_account &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Como usuários mal-intencionados às vezes tentam elevar seus privilégios usando **xp_cmdshell**, **xp_cmdshell** é desabilitada por padrão. Use **sp_configure** ou **gerenciamento baseado em políticas** para habilitá-lo. Para obter mais informações, veja [Opção de configuração de servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
 Quando habilitado pela primeira vez, **xp_cmdshell** requer a permissão CONTROL SERVER para executar e o processo do Windows criado pelo **xp_cmdshell** tem o mesmo contexto de segurança como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço geralmente tem mais permissões que são necessárias para o trabalho realizado pelo processo criado pelo **xp_cmdshell**. Para aumentar a segurança, acesse **xp_cmdshell** deve ser restrito a usuários altamente privilegiados.  
  
 Para permitir que não administradores usem **xp_cmdshell**e permitir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crie processos filho com o token de segurança de uma conta com privilégios mínimos, siga estas etapas:  
  
1.  Crie e personalize uma conta de usuário local do Windows ou uma conta de domínio com os privilégios mínimos que seus processos exigeem.  
  
2.  Use o **sp_xp_cmdshell_proxy_account** procedimento de sistema para configurar o **xp_cmdshell** para usar a conta com menos privilégios.  
  
    > [!NOTE]  
    >  Você também pode configurar esta conta de proxy usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] clicando com o **propriedades** no nome do servidor no Pesquisador de objetos e consultando o **segurança** guia para o **Server conta proxy** seção.  
  
3.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], usando o banco de dados mestre, execute o `GRANT exec ON xp_cmdshell TO '<somelogin>'` instrução para conceder específicos não**sysadmin** os usuários a capacidade de executar **xp_cmdshell**. O logon especificado deve ser mapeado para um usuário no banco de dados mestre.  
  
 Agora que não são administradores podem iniciar processos do sistema operacional com **xp_cmdshell** e os processos executados com as permissões da conta proxy que você configurou. Os usuários com permissão CONTROL SERVER (membros do **sysadmin** função de servidor fixa) continuará a receber as permissões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço conta para processos filho iniciados pelo **xp_cmdshell** .  
  
 Para determinar a conta do Windows que está sendo usada por **xp_cmdshell** ao iniciar processos do sistema operacional, execute a seguinte instrução:  
  
```  
xp_cmdshell 'whoami.exe'  
  
```  
  
 Para determinar o contexto de segurança para outro logon, execute o seguinte:  
  
```  
EXECUTE AS LOGIN = '<other_login>' ;  
GO  
xp_cmdshell 'whoami.exe' ;  
REVERT ;  
  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-a-list-of-executable-files"></a>A. Retornando uma lista de arquivos executáveis  
 O exemplo a seguir mostra o procedimento armazenado estendido `xp_cmdshell` executando um comando de diretório.  
  
```  
EXEC master..xp_cmdshell 'dir *.exe''  
```  
  
### <a name="b-returning-no-output"></a>B. Não retornando nenhuma saída  
 O exemplo a seguir usa `xp_cmdshell` para executar uma cadeia de caracteres de comando sem retornar a saída ao cliente.  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks, NO_OUTPUT';  
GO  
```  
  
### <a name="c-using-return-status"></a>C. Usando o status de retorno  
 No exemplo a seguir, o `xp_cmdshell` procedimento armazenado estendido também sugere o status de retorno. O valor de código de retorno é armazenado na variável `@result`.  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>D. Escrevendo conteúdos de variável em um arquivo  
 O exemplo a seguir grava o conteúdo da variável `@var` em um arquivo chamado `var_out.txt` no diretório de servidor atual.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>E. Capturando o resultado de um comando em um arquivo  
 O exemplo a seguir grava o conteúdo do diretório atual em um arquivo chamado `dir_out.txt` no diretório de servidor atual.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Estendidos gerais procedimentos armazenados &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Opção de configuração de servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [Configuração da Área de Superfície](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
