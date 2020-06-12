---
title: Preparando bancos de dados do Access para migração (AccessToSQL) | Microsoft Docs
description: Saiba como determinar quais bancos de dados do Access devem ser migrados para o SQL Server ou para o Azure SQL Database e garantir que eles estejam prontos para a migração.
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
ms.openlocfilehash: 1b0fe1ef2f51da9e64954040e58440a9e7eee58e
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293714"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Preparando bancos de dados do Access para migração (AccessToSQL)
Antes de migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve determinar quais bancos de dados serão migrados e garantir que esses bancos de dados estejam prontos para a migração.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>Determinando quando migrar para o SQL Server  
O mecanismo de banco de dados Jet, que é usado como o mecanismo de banco de dados para o Access, é uma solução flexível e fácil de usar para o gerenciamento de dados. No entanto, à medida que os bancos de dados se tornam maiores e mais críticos, muitos usuários acham que exigem maior desempenho, segurança ou disponibilidade. Para aplicativos que exigem uma plataforma de dados mais robusta, considere a possibilidade de mover os bancos subjacentes para esses aplicativos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre como decidir quando migrar, consulte a [página informações de migração](https://go.microsoft.com/fwlink/?LinkId=68571) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] site da Web.  
  
Depois de migrar bancos de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode continuar a usar o acesso usando tabelas vinculadas ou pode migrar manualmente seus aplicativos para um [!INCLUDE[msCoName](../../includes/msconame_md.md)] código baseado em .NET Framework que interage diretamente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="determining-which-databases-to-migrate"></a>Determinando quais bancos de dados migrar  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) para Access pode localizar bancos de dados do Access para você. Em seguida, você pode exportar metadados sobre esses bancos de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre como exportar e consultar metadados, consulte [exportando um inventário de acesso](exporting-an-access-inventory-accesstosql.md).  

   > [!NOTE]
   > Nem todos os recursos de acesso e configurações têm suporte no, ou podem ser facilmente convertidos em, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Antes de começar a migrar bancos de dados, consulte [recursos de acesso incompatíveis](incompatible-access-features-accesstosql.md).
  
## <a name="preparing-for-migration"></a>Preparando para a migração  
Use as diretrizes a seguir para ajudar a preparar seus bancos de dados do Access para a migração para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="upgrading-older-access-databases"></a>Atualizando bancos de dados do Access mais antigos  
O SSMA para Access dá suporte ao Access 97 e versões posteriores. Se você tiver bancos de dados de versões anteriores do Access, abra e salve os bancos de dados no Access 97 ou em uma versão posterior.  
  
### <a name="removing-workgroup-protection"></a>Removendo a proteção do grupo de trabalho  
O SSMA não pode migrar bancos de dados que usam a proteção de grupo de trabalho. Para remover a proteção de grupo de trabalho de um banco de dados do Access, execute as seguintes etapas:  
  
1.  Copie o arquivo de banco de dados do Access para outro local.  
  
2.  Abra o banco de dados copiado.  
  
3.  No menu **ferramentas** , aponte para **segurança**e selecione **permissões de usuário e grupo**.  
  
4.  Selecione a opção **usuários** , selecione o usuário **administrador** e verifique se a permissão **administrar** está selecionada.  
  
5.  Selecione a opção **grupos** , selecione o grupo **usuários** e verifique se a permissão **administrar** está selecionada.  
  
6.  Clique em **OK**e, no menu **arquivo** , clique em **sair**.  
  
Agora você pode usar o SSMA para migrar o banco de dados copiado. Depois de carregar o esquema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode proteger manualmente o banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="backing-up-databases"></a>Fazendo backup de bancos de dados  
Antes de migrar seus bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve fazer backup dos bancos de dados do Access que serão migrados, bem como dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dado para os quais você vai migrar objetos de acesso.  
  
Para fazer backup de um banco de dados do Access, no menu **ferramentas** , aponte para **utilitários de banco de dados**e, em seguida, selecione **backup de banco**de dados.  
  
Para obter informações sobre como fazer backup de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados, consulte "fazendo backup e restaurando bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
### <a name="documenting-databases"></a>Documentando bancos de dados  
Você também pode querer documentar as propriedades, como listas de objetos de banco de dados, tamanhos de arquivo e permissões, de seus bancos de dados do Access. Para gerar essa documentação no Access, no menu **ferramentas** , aponte para **analisar**e clique em **documentado**.  
  
## <a name="see-also"></a>Veja também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vinculando aplicativos de acesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
