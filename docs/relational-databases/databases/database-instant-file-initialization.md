---
title: Inicialização imediata de arquivo do banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41906481891908c85daf22c223e77826baa27766
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581989"
---
# <a name="database-file-initialization"></a>Inicialização de arquivos de bancos de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Arquivos de dados e de log são inicializados para substituir todos os dados existentes que foram deixados no disco por arquivos excluídos anteriormente. Os arquivos de dados e de log são inicializados pela primeira vez ao anular os arquivos (preenchimento com zeros) quando você executa uma das seguintes operações:  
  
- Criar um banco de dados.  
- Adicionar dados ou arquivos de log a um banco de dados existente.  
- Aumentar o tamanho de um arquivo existente (inclusive operações de aumento automático).  
- Restaurar um banco de dados ou grupo de arquivos.  
  
A inicialização dos arquivos faz com que essas operações demorem mais. Porém, quando os dados são gravados nos arquivos pela primeira vez, o sistema operacional não precisa completar os arquivos com zeros.  
  
## <a name="instant-file-initialization-ifi"></a>IFI (Inicialização Instantânea de Arquivo)  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os arquivos de dados podem ser inicializados de imediato para evitar as operações de anulação. A inicialização instantânea de arquivo permite execução rápida das operações de arquivo mencionadas anteriormente. A inicialização imediata de um arquivo recupera espaço em disco sem encher esse espaço com zeros. Em vez disso, o conteúdo do disco é substituído à medida que novos dados são gravados nos arquivos. Arquivos de log não podem ser inicializados de imediato.  
  
> [!NOTE]
> A Inicialização Instantânea de Arquivo está disponível apenas no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] ou [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] ou em versões posteriores.  
> 
> [!IMPORTANT]
> A inicialização instantânea de arquivo está disponível apenas para os arquivos de dados. Os arquivos de log sempre serão anulados quando forem criados ou tiverem aumento de tamanho.
  
A inicialização instantânea de arquivo estará disponível somente se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de inicialização do serviço tiver recebido *SE_MANAGE_VOLUME_NAME*. Os membros do grupo administrador do Windows têm esse direito e podem atribuí-lo a outros usuários adicionando-os à política de segurança **Executar tarefas de manutenção de volume** .  
  
> [!IMPORTANT]
> O uso de alguns recursos, como o [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md), pode impedir a Inicialização Instantânea de Arquivo.  
  
Para conceder a permissão `Perform volume maintenance tasks` a uma conta:  
  
1.  No computador em que o arquivo de dados será criado, abra o aplicativo **Política de Segurança Local** (`secpol.msc`).  
  
2.  No painel esquerdo, expanda **Políticas Locais**e, em seguida, clique em **Atribuição de Direitos de Usuário**.  
  
3.  No painel direito, clique duas vezes em **Executar tarefas de manutenção de volume**.  
  
4.  Clique em **Adicionar usuário ou grupo** e adicione a conta que executa o serviço SQL Server.  
  
5.  Clique em **Aplicar**e feche todas as caixas de diálogo **Política de Segurança Local** .  

1. Reinicie o serviço SQL Server.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

> [!NOTE]
> A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], essa permissão pode ser concedida à conta de serviço no momento da instalação. Se estiver usando a [instalação do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), adicione o argumento /SQLSVCINSTANTFILEINIT ou marque a caixa *Conceder privilégio Realizar Tarefa de Manutenção de Volume para o Serviço de Mecanismo de Banco de Dados do SQL Server* no [assistente de instalação](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).

> [!NOTE]
> A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 e do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a coluna *instant_file_initialization_enabled* na DMV [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) pode ser usada para identificar se a inicialização instantânea de arquivo está habilitada.

## <a name="remarks"></a>Remarks
Se a conta de inicialização de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receber *SE_MANAGE_VOLUME_NAME*, uma mensagem informativa semelhante à seguinte será registrada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante a inicialização: 

`Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

Se a conta de inicialização de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **não** receber *SE_MANAGE_VOLUME_NAME*, uma mensagem informativa semelhante à seguinte será registrada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante a inicialização: 

`Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

## <a name="security-considerations"></a>Considerações sobre segurança  
Ao usar a IFI (Inicialização Instantânea de Arquivo), como o conteúdo excluído do disco é substituído somente à medida que novos dados são gravados nos arquivos, o conteúdo excluído poderá ser acessado por uma entidade de segurança não autorizada, até que outros dados sejam gravados nessa área específica do arquivo de dados. Embora o arquivo de banco de dados esteja associado à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse risco de divulgação de informações é reduzido pela DACL (lista de controle de acesso discricionário) no arquivo. Essa DACL permite acesso de arquivo somente à conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao administrador local. Porém, quando o arquivo é desassociado, ele pode ser acessado por um usuário ou serviço que não tenha *SE_MANAGE_VOLUME_NAME*. Existe uma consideração similar quando é feito o backup do banco de dados: se o arquivo de backup não estiver protegido com uma DACL adequada, o conteúdo excluído poderá ficar disponível para um usuário ou um serviço não autorizado.  

Outra consideração é que, quando um arquivo é aumentado usando IFI, um administrador do SQL Server pode, potencialmente, acessar o conteúdo da página bruta e ver o conteúdo excluído anteriormente.

Se os arquivos de banco de dados estão hospedados em uma rede de área de armazenamento, também é possível que a rede de área de armazenamento apresente sempre novas páginas como pré-inicializadas e, fazer com que o sistema operacional reinicialize as páginas, poderá gerar uma sobrecarga desnecessária.
 
> [!NOTE]
> Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver instalado em um ambiente físico seguro, os benefícios de desempenho da habilitação da inicialização instantânea de arquivo poderão compensar o risco de segurança. Daí, o motivo dessa recomendação.
  
Se houver preocupação com a possível divulgação do conteúdo excluído, você deverá executar uma das seguintes ações ou ambas:  
  
- Sempre se certifique de que todos os arquivos de dados desassociados e arquivos de backup tenham DACL restritivas.  
- Desabilite a inicialização instantânea de arquivo para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revogando *SE_MANAGE_VOLUME_NAME* da conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!IMPORTANT]
> A desabilitação da inicialização instantânea de arquivo aumentará os tempos de alocação para arquivos de dados.  
  
> [!NOTE]  
> Desabilitar a inicialização de arquivos imediata afeta somente os arquivos que forem criados ou tiverem seu tamanho aumentado após ser revogado o direito do usuário.  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
