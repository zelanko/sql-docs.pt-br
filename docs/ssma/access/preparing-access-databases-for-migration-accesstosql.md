---
title: Preparar bancos de dados de acesso para a migração (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: e78d5226a4ab726718eb7725640de22dd811a684
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764404"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Preparar bancos de dados de acesso para a migração (AccessToSQL)
Antes de migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve determinar quais bancos de dados para migrar e certifique-se de que esses bancos de dados estão prontos para a migração.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>Determinando quando migrar para o SQL Server  
O mecanismo de banco de dados Jet, que é usado como o mecanismo de banco de dados de acesso, é uma solução flexível e fácil de usar para gerenciamento de dados. No entanto, como bancos de dados ficam maiores e mais de missão crítica, muitos usuários consideram que precisam de maior desempenho, segurança ou disponibilidade. Para aplicativos que exigem uma plataforma mais robusta de dados, considere mover os bancos de dados subjacentes para esses aplicativos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como decidir quando migrar, consulte o [página de informações de migração](http://go.microsoft.com/fwlink/?LinkId=68571) sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] site da Web.  
  
Depois de migrar bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode continuar a usar o acesso usando tabelas vinculadas ou manualmente, você pode migrar seus aplicativos para o [!INCLUDE[msCoName](../../includes/msconame_md.md)] código baseado no .NET Framework que interage diretamente com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="determining-which-databases-to-migrate"></a>Determinando quais bancos de dados para migrar  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA (Migration Assistant) para acesso possam localizar bancos de dados do Access para você. Em seguida, você pode exportar metadados sobre esses bancos de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como exportar e consultar os metadados, consulte [exportando um inventário do Access](exporting-an-access-inventory-accesstosql.md).  

   > [!NOTE]
   > Nem todos os recursos de acesso e as configurações têm suporte, ou pode ser facilmente convertidas, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de iniciar a migração de bancos de dados, consulte [recursos do Access incompatíveis](incompatible-access-features-accesstosql.md).
  
## <a name="preparing-for-migration"></a>Preparação para migração  
Use as seguintes diretrizes para ajudar a preparar seus bancos de dados do Access para a migração para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="upgrading-older-access-databases"></a>Atualizando bancos de dados antigos de acesso  
SSMA para Access suporta Access 97 e versões posteriores. Se você tiver bancos de dados de versões anteriores do Access, abra e salve os bancos de dados no Access 97 ou posterior.  
  
### <a name="removing-workgroup-protection"></a>Remover a proteção do grupo de trabalho  
O SSMA não pode migrar bancos de dados que usam a proteção do grupo de trabalho. Para remover a proteção do grupo de trabalho de um banco de dados do Access, execute as seguintes etapas:  
  
1.  Copie o arquivo de banco de dados do Access para outro local.  
  
2.  Abra o banco de dados copiado.  
  
3.  Sobre o **ferramentas** , aponte para **Security**e, em seguida, selecione **permissões de usuário e grupo**.  
  
4.  Selecione o **os usuários** opção, selecione a **Admin** usuário e, em seguida, certifique-se de que o **administrar** permissão é selecionada.  
  
5.  Selecione o **grupos** opção, selecione a **usuários** agrupar e, em seguida, certifique-se de que o **administrar** permissão é selecionada.  
  
6.  Clique em **Okey**e, em seguida, o **arquivo** menu, clique em **sair**.  
  
Agora você pode usar o SSMA para migrar o banco de dados copiado. Depois de carregar o esquema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode proteger o banco de dados manualmente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="backing-up-databases"></a>Fazendo backup de bancos de dados  
Antes de migrar seus bancos de dados Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve fazer backup acesso bancos de dados que será migrado, bem como a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados no qual você irá migrar acessem objetos e dados.  
  
Para fazer backup de um banco de dados do Access, o **ferramentas** , aponte para **utilitários de banco de dados**e, em seguida, selecione **backup do banco de dados**.  
  
Para obter informações sobre como fazer backup [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados, consulte "Fazendo backup e restaurando bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
### <a name="documenting-databases"></a>Documentando bancos de dados  
Você também poderá documentar as propriedades, como listas de objetos de banco de dados, tamanhos de arquivo e permissões de seus bancos de dados do Access. Para gerar esta documentação no Access, o **ferramentas** , aponte para **analisar**e, em seguida, clique em **documentada**.  
  
## <a name="see-also"></a>Confira também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vincular aplicativos do Access para o SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
