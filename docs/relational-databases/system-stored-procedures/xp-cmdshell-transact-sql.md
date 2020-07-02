---
title: xp_cmdshell (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2ffe3197f74e274792ee1a3f97d700492a018bef
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633747"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Gera um shell de comando do Windows e passa em uma cadeia de caracteres para execução. Qualquer saída é retornada como linhas de texto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *command_string* **'**  
 É a cadeia de caracteres que contém um comando a ser passado para o sistema operacional. *command_string* é **varchar (8000)** ou **nvarchar (4000)**, sem padrão. *command_string* não pode conter mais de um conjunto de aspas duplas. Um único par de aspas será necessário se algum espaço estiver presente nos caminhos de arquivo ou nomes de programa referenciados em *command_string*. Se você tiver dificuldade com espaços inseridos, considere o uso de nomes de arquivo FAT 8.3 como uma solução alternativa.  
  
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
  
 As linhas são retornadas em uma coluna **nvarchar (255)** . Se a opção **no_output** for usada, somente o seguinte será retornado:  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>Comentários  
 O processo do Windows gerado por **xp_cmdshell** tem os mesmos direitos de segurança que a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço.  
  
 **xp_cmdshell** funciona de forma síncrona. O controle não é voltado ao chamador até que o comando do shell de comandos seja concluído.  
  
 **xp_cmdshell** pode ser habilitado e desabilitado usando o gerenciamento baseado em políticas ou executando **sp_configure**. Para obter mais informações, consulte [configuração da área de superfície](../../relational-databases/security/surface-area-configuration.md) e opção de configuração de [servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
> [!IMPORTANT]
>  Se **xp_cmdshell** for executado em um lote e retornar um erro, o lote falhará. É uma alteração de comportamento. Em versões anteriores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lote, continuaria a ser executado.  
  
## <a name="xp_cmdshell-proxy-account"></a>Conta proxy xp_cmdshell  
 Quando ele é chamado por um usuário que não é membro da função de servidor fixa **sysadmin** , **xp_cmdshell** se conecta ao Windows usando o nome da conta e a senha armazenados na credencial **# #xp_cmdshell_proxy_account #**#. Se essa credencial de proxy não existir, **xp_cmdshell** irá falhar.  
  
 A credencial da conta proxy pode ser criada executando **sp_xp_cmdshell_proxy_account**. Como argumentos, esse procedimento armazenado possui um nome de usuário e uma senha do Windows. Por exemplo, o comando a seguir cria uma credencial de proxy para o usuário de domínio do Windows `SHIPPING\KobeR` que possui a senha do Windows `sdfh%dkc93vcMt0`.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 Para obter mais informações, consulte [sp_xp_cmdshell_proxy_account &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Como os usuários mal-intencionados às vezes tentam elevar seus privilégios usando **xp_cmdshell**, o **xp_cmdshell** é desabilitado por padrão. Use **sp_configure** ou **Gerenciamento baseado em políticas** para habilitá-lo. Para obter mais informações, veja [Opção de configuração de servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
 Quando habilitada pela primeira vez, **xp_cmdshell** requer a permissão Control Server para executar e o processo do Windows criado pelo **xp_cmdshell** tem o mesmo contexto de segurança que a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço. A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço geralmente tem mais permissões do que o necessário para o trabalho executado pelo processo criado pelo **xp_cmdshell**. Para aumentar a segurança, o acesso a **xp_cmdshell** deve ser restrito a usuários altamente privilegiados.  
  
 Para permitir que não administradores usem **xp_cmdshell**e permitir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a criação de processos filho com o token de segurança de uma conta com menos privilégios, siga estas etapas:  
  
1.  Crie e personalize uma conta de usuário local do Windows ou uma conta de domínio com os privilégios mínimos que seus processos exigeem.  
  
2.  Use o procedimento do sistema **sp_xp_cmdshell_proxy_account** para configurar **xp_cmdshell** para usar essa conta com privilégios mínimos.  
  
    > [!NOTE]  
    >  Você também pode configurar essa conta proxy usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] clicando com o botão direito do mouse em **Propriedades** no nome do servidor no Pesquisador de objetos e examinando a guia **segurança** da seção **conta proxy do servidor** .  
  
3.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , usando o banco de dados mestre, execute a `GRANT exec ON xp_cmdshell TO N'<some_user>';` instrução para fornecer aos usuários não-**sysadmin** específicos a capacidade de executar **xp_cmdshell**. O usuário especificado deve existir no banco de dados mestre.  
  
 Agora, não administradores podem iniciar processos do sistema operacional com **xp_cmdshell** e esses processos são executados com as permissões da conta proxy que você configurou. Os usuários com permissão CONTROL SERVER (membros da função de servidor fixa **sysadmin** ) continuarão a receber as permissões da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço para processos filho que são iniciados pelo **xp_cmdshell**.  
  
 Para determinar a conta do Windows que está sendo usada pelo **xp_cmdshell** ao iniciar processos do sistema operacional, execute a seguinte instrução:  
  
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
  
### <a name="a-returning-a-list-of-executable-files"></a>a. Retornando uma lista de arquivos executáveis  
 O exemplo a seguir mostra o procedimento armazenado estendido `xp_cmdshell` executando um comando de diretório.  
  
```  
EXEC master..xp_cmdshell 'dir *.exe'  
```  
  
### <a name="b-returning-no-output"></a>B. Não retornando nenhuma saída  
 O exemplo a seguir usa `xp_cmdshell` para executar uma cadeia de caracteres de comando sem retornar a saída ao cliente.  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks', NO_OUTPUT;  
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
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Opção de configuração de servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [Configuração da Área de Superfície](../../relational-databases/security/surface-area-configuration.md)   
 [&#41;&#40;Transact-SQL de sp_xp_cmdshell_proxy_account](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
