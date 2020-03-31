---
title: xp_cmdshell (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2020
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
ms.openlocfilehash: 2ce32fc31373077418e77d31ce064d60e23f1b24
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402687"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera um shell de comando do Windows e passa em uma cadeia de caracteres para execução. Qualquer saída é retornada como linhas de texto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **command_string** *command_string* **'**  
 É a cadeia de caracteres que contém um comando a ser passado para o sistema operacional. *command_string* é **varchar(8000)** ou **nvarchar(4000)**, sem padrão. *command_string* não pode conter mais de um conjunto de aspas duplas. Um único par de aspas é necessário se algum espaço estiver presente nos caminhos de arquivo ou nomes de programas referenciados em *command_string*. Se você tiver dificuldade com espaços inseridos, considere o uso de nomes de arquivo FAT 8.3 como uma solução alternativa.  
  
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
  
 As linhas são devolvidas em uma coluna **nvarchar(255).** Se a opção **no_output** for usada, apenas as seguintes serão devolvidas:  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>Comentários  
 O processo do Windows gerado por **xp_cmdshell** tem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os mesmos direitos de segurança que a conta de serviço.  
  
 **xp_cmdshell** opera sincronicamente. O controle não é voltado ao chamador até que o comando do shell de comandos seja concluído.  
  
 **xp_cmdshell** podem ser habilitados e desativados usando o Gerenciamento Baseado em Políticas ou executando **sp_configure**. Para obter mais informações, consulte [Configuração da área de superfície](../../relational-databases/security/surface-area-configuration.md) e opção de [configuração do servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
> [!IMPORTANT]
>  Se **xp_cmdshell** for executada dentro de um lote e retornar um erro, o lote falhará.
  
## <a name="xp_cmdshell-proxy-account"></a>Conta proxy xp_cmdshell  
 Quando é chamado por um usuário que não é membro da função servidor fixo **sysadmin,** **xp_cmdshell** se conecta ao Windows usando o nome da conta e senha armazenados na credencial chamada **##xp_cmdshell_proxy_account##**. Se essa credencial proxy não existir, **xp_cmdshell** falharão.  
  
 A credencial da conta proxy pode ser criada executando **sp_xp_cmdshell_proxy_account**. Como argumentos, esse procedimento armazenado possui um nome de usuário e uma senha do Windows. Por exemplo, o comando a seguir cria uma credencial de proxy para o usuário de domínio do Windows `SHIPPING\KobeR` que possui a senha do Windows `sdfh%dkc93vcMt0`.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 Para obter mais informações, consulte [sp_xp_cmdshell_proxy_account &#40;transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Como usuários mal-intencionados às vezes tentam elevar seus privilégios usando **xp_cmdshell,** **xp_cmdshell** é desativado por padrão. Use **sp_configure** ou **Gerenciamento Baseado em Políticas** para habilitá-lo. Para obter mais informações, veja [Opção de configuração de servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
 Quando habilitado pela primeira vez, **xp_cmdshell** requer permissão do CONTROL SERVER para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executar e o processo do Windows criado por **xp_cmdshell** tem o mesmo contexto de segurança que a conta de serviço. A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço muitas vezes tem mais permissões do que o necessário para o trabalho realizado pelo processo criado por **xp_cmdshell**. Para aumentar a segurança, o acesso a **xp_cmdshell** deve ser restrito a usuários altamente privilegiados.  
  
 Para permitir que os não-administradores usem **xp_cmdshell**e permitir criar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processos filho com o token de segurança de uma conta menos privilegiada, siga estas etapas:  
  
1.  Crie e personalize uma conta de usuário local do Windows ou uma conta de domínio com os privilégios mínimos que seus processos exigeem.  
  
2.  Use o procedimento **do sistema sp_xp_cmdshell_proxy_account** para configurar **xp_cmdshell** de usar essa conta menos privilegiada.  
  
    > [!NOTE]  
    >  Você também pode configurar essa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] conta proxy usando clicando com o botão direito do mouse **Propriedades** no nome do servidor no Object Explorer e olhando na guia **Segurança** para a seção **conta proxy do servidor.**  
  
3.  Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], usando o banco `GRANT exec ON xp_cmdshell TO N'<some_user>';` de dados mestre, executar a instrução para dar aos usuários não-sysadmin específicos a capacidade de executar **xp_cmdshell**.**sysadmin** O usuário especificado deve existir no banco de dados mestre.  
  
 Agora, os não-administradores podem iniciar processos de sistema operacional com **xp_cmdshell** e esses processos são executados com as permissões da conta proxy que você configurou. Os usuários com permissão do SERVIDOR CONTROL (membros da função servidor fixo **sysadmin)** continuarão a receber as permissões da conta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço para processos infantis que são lançados por **xp_cmdshell**.  
  
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
 No exemplo a `xp_cmdshell` seguir, o procedimento armazenado estendido também sugere o status de retorno. O valor de código de retorno é armazenado na variável `@result`.  
  
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
 [Procedimentos gerais de armazenalidade estendida &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Opção de configuração do servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [Configuração da área de superfície](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
