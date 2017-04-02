---
title: "Inicializa&#231;&#227;o imediata de arquivo do banco de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "inicializando arquivos [SQL Server]"
  - "inicializações de arquivo instantâneas [SQL Server]"
  - "inicialização rápida de arquivo (SQL Server)"
  - "inicialização de arquivo [SQL Server]"
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Inicializa&#231;&#227;o imediata de arquivo do banco de dados
  Arquivos de dados e de log são inicializados para substituir todos os dados existentes que foram deixados no disco por arquivos excluídos anteriormente. Primeiro, os arquivos de dados e de log são inicializados ao serem completados com zeros quando você executa uma das seguintes operações:  
  
-   Criar um banco de dados.  
  
-   Adicionar arquivos, log ou dados a um banco de dados existente.  
  
-   Aumentar o tamanho de um arquivo existente (inclusive operações de aumento automático).  
  
-   Restaurar um banco de dados ou grupo de arquivos.  
  
 A inicialização dos arquivos faz com que essas operações demorem mais. Porém, quando os dados são gravados nos arquivos pela primeira vez, o sistema operacional não precisa completar os arquivos com zeros.  
  
## Inicialização imediata de arquivo  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os arquivos de dados podem ser inicializados de imediato. Isso permite execução rápida das operações de arquivo mencionadas anteriormente. A inicialização imediata de um arquivo recupera espaço em disco sem encher esse espaço com zeros. Em vez disso, o conteúdo do disco é substituído à medida que novos dados são gravados nos arquivos. Arquivos de log não podem ser inicializados de imediato.  
  
> [!NOTE]  
>  A Inicialização Instantânea de Arquivo está disponível apenas no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] ou [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] ou em versões posteriores.  
  
 A inicialização imediata de arquivos estará disponível somente se a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) tiver recebido SE_MANAGE_VOLUME_NAME. Os membros do grupo administrador do Windows têm esse direito e podem atribuí-lo a outros usuários adicionando-os à política de segurança **Executar tarefas de manutenção de volume** . Para obter mais informações sobre como atribuir direitos de usuário, consulte a documentação do Windows.  
  
 A inicialização instantânea de arquivo não está disponível quando a TDE está habilitada.  
  
 Para conceder a permissão `Perform volume maintenance tasks` a uma conta:  
  
1.  No computador em que o arquivo de backup será criado, abra o aplicativo **Política de Segurança Local** (`secpol.msc`).  
  
2.  No painel esquerdo, expanda **Políticas Locais**e, em seguida, clique em **Atribuição de Direitos de Usuário**.  
  
3.  No painel direito, clique duas vezes em **Executar tarefas de manutenção de volume**.  
  
4.  Clique em **Adicionar Usuário ou Grupo** e adicione as contas de usuário que são usadas ​​para backups.  
  
5.  Clique em **Aplicar**e feche todas as caixas de diálogo **Política de Segurança Local** .  
  
### Considerações sobre segurança  
 Como o conteúdo excluído do disco é substituído somente à medida que novos dados são gravados nos arquivos, o conteúdo excluído poderá ser acessado por uma entidade de segurança não autorizada. Embora o arquivo de banco de dados esteja associado à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa ameaça de divulgação de informações é reduzida pela lista de controle de acesso discricionário (DACL) no arquivo. Essa DACL permite acesso de arquivo somente à conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao administrador local. Porém, quando o arquivo é desassociado, ele pode ser acessado por um usuário ou serviço que não tenha SE_MANAGE_VOLUME_NAME. Existe uma ameaça semelhante ao se fazer backup do banco de dados. O conteúdo excluído pode ficar disponível para um usuário ou serviço não autorizado se o arquivo de backup não for protegido com uma DACL adequada.  
  
 Se o potencial de divulgação do conteúdo excluído for uma preocupação, você deve tomar uma ou ambas as providências seguintes:  
  
-   Sempre se certifique de que todos os arquivos de dados desassociados e arquivos de backup tenham DACL restritivas.  
  
-   Desabilite a inicialização de arquivo imediata para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revogando o direito SE_MANAGE_VOLUME_NAME da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Desabilitar a inicialização de arquivos imediata afeta somente os arquivos que forem criados ou tiverem seu tamanho aumentado após ser revogado o direito do usuário.  
  
## Consulte também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  