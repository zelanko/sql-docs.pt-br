---
title: "Preparar bancos de dados do Access para a migração (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "20"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: fb7743e870b97882ad2bcec0428b3047f28f538d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Preparar bancos de dados do Access para a migração (AccessToSQL)
Antes de migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você deve determinar quais bancos de dados para migrar e certifique-se de que esses bancos de dados estão prontos para a migração.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>Determinando quando a migração para o SQL Server  
O mecanismo de banco de dados Jet, que é usado como o mecanismo de banco de dados de acesso, é uma solução flexível e fácil de usar para gerenciamento de dados. No entanto, como bancos de dados ficam maiores e mais essenciais, muitos usuários localizar que precisam de maior desempenho, segurança ou disponibilidade. Para aplicativos que exigem uma plataforma de dados mais robusta, considere mover os bancos de dados subjacentes para esses aplicativos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações sobre como decidir quando a migração, consulte o [página de informações de migração](http://go.microsoft.com/fwlink/?LinkId=68571) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] site da Web.  
  
Depois de migrar os bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode continuar a usar o acesso usando tabelas vinculadas ou manualmente, você pode migrar seus aplicativos para [!INCLUDE[msCoName](../../includes/msconame_md.md)] código baseado no .NET Framework que interagem diretamente com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="determining-which-databases-to-migrate"></a>Determinando quais bancos de dados para migrar  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSMA (Migration Assistant) para acesso possam localizar bancos de dados para você. Em seguida, você pode exportar metadados sobre os bancos de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações sobre como exportar e metadados de consulta, consulte [exportando um inventário de acesso](http://msdn.microsoft.com/7e1941fb-3d14-4265-aff6-c77a4026d0ed).  

   > [!NOTE]
   > Nem todos os recursos do Access e as configurações com suporte, ou podem ser convertidas facilmente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Antes de iniciar a migração de bancos de dados, consulte [recursos incompatíveis de acesso](http://msdn.microsoft.com/99d45b9c-e3b9-4d56-8c25-b594b887ace1).
  
## <a name="preparing-for-migration"></a>Preparação para migração  
Use as seguintes diretrizes para ajudar a preparar seus bancos de dados do Access para a migração para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="upgrading-older-access-databases"></a>Atualizando bancos de dados mais antigos  
O SSMA para Access dá suporte a acesso 97 e versões posteriores. Se você tiver bancos de dados de versões anteriores do Access, abra e salve os bancos de dados do Access 97 ou posterior.  
  
### <a name="removing-workgroup-protection"></a>Remover a proteção do grupo de trabalho  
O SSMA não pode migrar bancos de dados que usam a proteção do grupo de trabalho. Para remover a proteção do grupo de trabalho de um banco de dados, execute as seguintes etapas:  
  
1.  Copie o arquivo de banco de dados do Access para outro local.  
  
2.  Abra o banco de dados copiado.  
  
3.  Sobre o **ferramentas** , aponte para **segurança**e, em seguida, selecione **permissões de usuário e grupo**.  
  
4.  Selecione o **usuários** opção, selecione o **Admin** usuário e, em seguida, verifique se o **administrar** permissão é selecionada.  
  
5.  Selecione o **grupos** opção, selecione o **usuários** de grupo e, em seguida, verifique se o **administrar** permissão é selecionada.  
  
6.  Clique em **Okey**e, em seguida, o **arquivo** menu, clique em **saída**.  
  
Agora você pode usar o SSMA para migrar o banco de dados copiado. Depois de carregar o esquema em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode proteger o banco de dados manualmente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="backing-up-databases"></a>Fazendo backup de bancos de dados  
Antes de migrar seus bancos de dados Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você deve fazer backup acesso bancos de dados que você está fazendo a migração, bem como a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] acessam a bancos de dados no qual você irá migrar objetos e dados.  
  
Para fazer backup de um banco de dados, no **ferramentas** , aponte para **utilitários de banco de dados**e, em seguida, selecione **backup do banco de dados**.  
  
Para obter informações sobre como fazer backup [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados, consulte "Fazendo backup e restaurando bancos de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
### <a name="documenting-databases"></a>Documentando bancos de dados  
Você também poderá documentar as propriedades, como listas de objetos de banco de dados, tamanhos de arquivos e permissões de seus bancos de dados do Access. Para gerar esta documentação no Access, o **ferramentas** , aponte para **analisar**e, em seguida, clique em **documentadas**.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Vinculando a aplicativos de acesso ao SQL Server](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)
