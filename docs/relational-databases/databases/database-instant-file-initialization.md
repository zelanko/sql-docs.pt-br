---
title: "Inicialização imediata de arquivo do banco de dados | Microsoft Docs"
ms.custom: 
ms.date: 11/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization (SQL Server)
- file initialization [SQL Server]
- IFI [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3f0ef2d2c733a0ab1f349d42d621303cc6c133a5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="database-file-initialization"></a>Inicialização de arquivos de bancos de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Arquivos de dados e de log são inicializados para substituir todos os dados existentes que foram deixados no disco por arquivos excluídos anteriormente. Os arquivos de dados e de log são inicializados pela primeira vez ao anular os arquivos (preenchimento com zeros) quando você executa uma das seguintes operações:  
  
- Criar um banco de dados.  
  
- Adicionar dados ou arquivos de log a um banco de dados existente.  
  
- Aumentar o tamanho de um arquivo existente (inclusive operações de aumento automático).  
  
- Restaurar um banco de dados ou grupo de arquivos.  
  
A inicialização dos arquivos faz com que essas operações demorem mais. Porém, quando os dados são gravados nos arquivos pela primeira vez, o sistema operacional não precisa completar os arquivos com zeros.  
  
# <a name="instant-file-initialization-ifi"></a>IFI (Inicialização Instantânea de Arquivo)  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os arquivos de dados podem ser inicializados de imediato para evitar as operações de anulação. A inicialização instantânea de arquivo permite execução rápida das operações de arquivo mencionadas anteriormente. A inicialização imediata de um arquivo recupera espaço em disco sem encher esse espaço com zeros. Em vez disso, o conteúdo do disco é substituído à medida que novos dados são gravados nos arquivos. Arquivos de log não podem ser inicializados de imediato.  
  
> [!NOTE]  
>  A Inicialização Instantânea de Arquivo está disponível apenas no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] ou [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] ou em versões posteriores.  

> [!IMPORTANT]
> A inicialização instantânea de arquivo está disponível apenas para os arquivos de dados. Os arquivos de log sempre serão anulados quando forem criados ou tiverem aumento de tamanho.
  
A inicialização instantânea de arquivo estará disponível somente se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de inicialização do serviço tiver recebido *SE_MANAGE_VOLUME_NAME*. Os membros do grupo administrador do Windows têm esse direito e podem atribuí-lo a outros usuários adicionando-os à política de segurança **Executar tarefas de manutenção de volume** .  
  
O uso de alguns recursos, como o [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md), pode impedir a Inicialização Instantânea de Arquivo.  
  
Para conceder a permissão `Perform volume maintenance tasks` a uma conta:  
  
1.  No computador em que o arquivo de backup será criado, abra o aplicativo **Política de Segurança Local** (`secpol.msc`).  
  
2.  No painel esquerdo, expanda **Políticas Locais**e, em seguida, clique em **Atribuição de Direitos de Usuário**.  
  
3.  No painel direito, clique duas vezes em **Executar tarefas de manutenção de volume**.  
  
4.  Clique em **Adicionar Usuário ou Grupo** e adicione as contas de usuário que são usadas ​​para backups.  
  
5.  Clique em **Aplicar**e feche todas as caixas de diálogo **Política de Segurança Local** .  
  
### <a name="security-considerations"></a>Considerações sobre segurança  
 Como o conteúdo excluído do disco é substituído somente à medida que novos dados são gravados nos arquivos, o conteúdo excluído poderá ser acessado por uma entidade de segurança não autorizada, até que outros dados sejam gravados naquela área específica do arquivo de dados. Embora o arquivo de banco de dados esteja associado à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse risco de divulgação de informações é reduzido pela DACL (lista de controle de acesso discricionário) no arquivo. Essa DACL permite acesso de arquivo somente à conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao administrador local. Porém, quando o arquivo é desassociado, ele pode ser acessado por um usuário ou serviço que não tenha *SE_MANAGE_VOLUME_NAME*. Existe uma consideração similar quando é feito o backup do banco de dados: se o arquivo de backup não estiver protegido com uma DACL adequada, o conteúdo excluído poderá ficar disponível para um usuário ou um serviço não autorizado.  
 
 Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver instalado em um ambiente seguro, os benefícios de desempenho da habilitação da IFI podem compensar o risco de segurança e, portanto, o motivo dessa recomendação.
  
 Se houver preocupação com a possível divulgação do conteúdo excluído, você deverá executar uma das seguintes ações ou ambas:  
  
- Sempre se certifique de que todos os arquivos de dados desassociados e arquivos de backup tenham DACL restritivas.  
  
- Desabilite a inicialização instantânea de arquivo para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revogando *SE_MANAGE_VOLUME_NAME* da conta de inicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> Desabilitar a inicialização de arquivos imediata afeta somente os arquivos que forem criados ou tiverem seu tamanho aumentado após ser revogado o direito do usuário.  
  
## <a name="see-also"></a>Consulte também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
