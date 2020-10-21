---
description: Definir ou alterar a ordenação do servidor
title: Definir ou alterar a ordenação do servidor | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3ddd5615aafaa52a6bd0bb672f144e51d497c183
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193427"
---
# <a name="set-or-change-the-server-collation"></a>Definir ou alterar a ordenação do servidor

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  A ordenação do servidor atua como a ordenação padrão de todos os bancos de dados do sistema instalados com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e também com quaisquer bancos de dados de usuário recém-criados. Você deve escolher cuidadosamente a ordenação no nível do servidor porque ela afeta:
 - Regras de classificação e comparação em `=`, `JOIN`, `ORDER BY` e em outros operadores que comparam dados textuais.
 - Ordenação das colunas `CHAR`, `VARCHAR`, `NCHAR` e `NVARCHAR` em exibições do sistema e funções do sistema e dos objetos em TempDB (por exemplo, tabelas temporárias).
 - Nomes das variáveis, dos cursores e dos rótulos de `GOTO`. As variáveis @pi e @PI são consideradas como variáveis diferentes se a ordenação no nível do servidor diferencia maiúsculas de minúsculas e consideradas como as mesmas variáveis se a ordenação no nível do servidor diferencia maiúsculas de minúsculas.
  
## <a name="setting-the-server-collation-in-sql-server"></a>Definindo a ordenação do servidor no SQL Server

  A ordenação do servidor é especificada durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A ordenação padrão no nível do servidor é baseada na localidade do sistema operacional. Por exemplo, a ordenação padrão para sistemas que usam en-US (inglês dos Estados Unidos) é **SQL_Latin1_General_CP1_CI_AS**. As ordenações somente Unicode não podem ser especificadas como a ordenação no nível do servidor. Para obter mais informações, incluindo a lista de localidade do sistema operacional para mapeamentos de ordenação padrão, confira a seção "Ordenações no nível de servidor" de [Ordenação e suporte a Unicode](collation-and-unicode-support.md#Server-level-collations).

> [!NOTE]  
> A ordenação no nível de servidor para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o LocalDB Express é **SQL_Latin1_General_CP1_CI_AS** e não pode ser alterada durante nem após a instalação.  

## <a name="changing-the-server-collation-in-sql-server"></a>Alterando a ordenação do servidor no SQL Server

 A alteração da ordenação padrão para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser uma operação complexa e engloba as seguintes etapas:  
  
- Verifique se você tem todas as informações ou scripts necessários para recriar seus bancos de dados de usuário e todos os objetos neles.  
  
- Exporte todos os seus dados usando uma ferramenta como [bcp Utility](../../tools/bcp-utility.md). Para obter mais informações, consulte [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
- Descarte todos os bancos de dados de usuário.  
  
- Reconstrua o banco de dados mestre especificando a nova ordenação na propriedade SQLCOLLATION do comando **setup** . Por exemplo:  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]
    /SQLCOLLATION=CollationName  
    ```  
  
     Para obter mais informações, consulte [Recriar bancos de dados do sistema](../../relational-databases/databases/rebuild-system-databases.md).  
  
- Crie todos os bancos de dados e todos os objetos neles.  
  
- Importe todos os dados.  
  
> [!NOTE]  
> Em vez de alterar a ordenação padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode especificar uma ordenação para cada banco de dados que criar por meio da cláusula `COLLATE` das instruções `CREATE DATABASE` e `ALTER DATABASE`. Para saber mais, veja [Definir ou alterar a ordenação de banco de dados](set-or-change-the-database-collation.md).  
  
## <a name="setting-the-server-collation-in-managed-instance"></a>Definindo a ordenação do servidor na Instância Gerenciada
A ordenação em nível de servidor na instância gerenciada do SQL do Azure pode ser especificada quando a instância é criada e não pode ser alterada posteriormente. Você pode definir a ordenação no nível de servidor por meio [portal do Azure](/azure/sql-database/sql-database-managed-instance-get-started#create-a-managed-instance) ou do [modelo do PowerShell e do Resource Manager](/azure/sql-database/scripts/sql-managed-instance-create-powershell-azure-resource-manager-template) enquanto você estiver criando a instância. A ordenação padrão no nível do servidor é **SQL_Latin1_General_CP1_CI_AS**. As ordenações somente Unicode e UTF-8 novas não podem ser especificadas como ordenação em nível do servidor.
Se estiver migrando bancos de dados do SQL Server para a Instância Gerenciada, verifique a ordenação do servidor no SQL Server de origem usando a função `SERVERPROPERTY(N'Collation')` e crie uma Instância Gerenciada que corresponde à ordenação do SQL Server. A migração de um banco de dados do SQL Server para a Instância Gerenciada com ordenações no nível do servidor que não são correspondentes poderá causar vários erros inesperados nas consultas. Não é possível alterar a ordenação no nível do servidor na Instância Gerenciada existente.

## <a name="see-also"></a>Consulte Também

 [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [Definir ou alterar a ordenação de banco de dados](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [Definir ou alterar a ordenação de coluna](../../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Recompilar bancos de dados do sistema](../../relational-databases/databases/rebuild-system-databases.md)  
