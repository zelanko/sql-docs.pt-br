---
title: Recursos do Access incompatíveis (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2c5819ffe66cfb6d80e19973cc9b3f2cba0251df
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392468"
---
# <a name="incompatible-access-features-accesstosql"></a>Recursos do Access incompatíveis (AccessToSQL)
Nem todos os recursos de banco de dados do Access são compatíveis com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e acesso têm conjuntos diferentes de palavras-chave reservadas. Problemas como esses podem impedir uma migração bem-sucedida para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use a tabela a seguir para saber mais sobre problemas de migração possíveis e que você pode fazer sobre eles.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>Configurações de banco de dados ou recursos que podem afetar a migração  
  
|Configuração de banco de dados ou o recurso de acesso|Problema de migração|  
|--------------------------------------|-------------------|  
|Tabelas do Access não têm índices exclusivos.|Se uma tabela que não tem um índice exclusivo é migrada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você não pode modificar a tabela após a migração. Isso pode levar a problemas de compatibilidade de aplicativos.<br /><br />Quando você converte objetos de banco de dados do Access, a janela de saída listará as tabelas de acesso que não têm índices exclusivos.<br /><br />Você pode configurar o acesso para adicionar uma chave primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela durante a conversão. Para obter mais informações, consulte [configurações do projeto (conversão)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388).|  
|Acessar tabelas tem colunas de replicação.|Se uma tabela do Access que inclui as colunas do sistema de replicação é migrada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], funcionalidade de replicação do Jet será quebrada após a migração.<br /><br />Após a migração, considere o uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] replicação para manter cópias sincronizadas dos seus bancos de dados.|  
|Acessar tabelas que têm índices exclusivos contêm vários valores nulos.|Acessar tabelas que têm índices exclusivos com vários valores nulos não podem ser transferidas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pois em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], índices exclusivos não permitir vários nulos. Migração falhará para essas tabelas.<br /><br />O SSMA sinalizará esse problema nos relatórios de avaliação. Para criar um relatório de avaliação, consulte [avaliar objetos do banco de dados do Access para conversão](assessing-access-database-objects-for-conversion-accesstosql.md).<br /><br />Se esse problema, certifique-se de que a chave primária não tem valores duplicados de nulos. Ou, você deve remover a chave primária ou índices exclusivos que contêm vários valores nulos.|  
|Tabelas do Access contêm valores de data que estão fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo.|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** tipo aceita datas no intervalo de 1 de janeiro de 1753 a 31 de dezembro 9999 apenas. Acesso aceita datas no intervalo de 100 1 de janeiro a 31 de dezembro 9999.<br /><br />O SSMA sinalizará esse problema nos relatórios de avaliação. Para criar um relatório de avaliação, consulte [avaliar objetos do banco de dados do Access para conversão](assessing-access-database-objects-for-conversion-accesstosql.md).<br /><br />Você pode configurar como o SSMA resolve as datas que estão fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo. Para obter mais informações, consulte [configurações do projeto (migração)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).|  
|Comprimentos de índice no Access excederem 900 bytes.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os índices têm um limite de 900 bytes para o tamanho total das colunas de chave de índice. Se suas tabelas do Access usam índices maiores, o SSMA exibirá um aviso.<br /><br />Se você continuar com a migração de dados, a migração poderá falhar.|  
|Nomes de objeto de acesso são [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] palavras-chave, ou contenha caracteres especiais.|Acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm conjuntos diferentes de palavras-chave reservadas e caracteres especiais. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceitará objetos que são nomeados usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] palavras-chave ou que contenham caracteres especiais se você usar identificadores entre colchetes ou entre aspas, como "select" ou [Selecionar] e. Para obter mais informações, consulte "Identificadores de delimitado (mecanismo de banco de dados)" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.<br /><br />**Observação:** para usar aspas para delimitar identificadores, SET QUOTED_IDENTIFIER deve estar ON.<br /><br />Por exemplo, `CREATE TABLE [schema](c1 [FOR])` é uma instrução válida, embora **esquema** e **para** são palavras-chave reservadas. Além disso, `CREATE TABLE [xxx*yyy](c1 x&y)` é uma instrução válida, mesmo que o nome de tabela e coluna conter os caracteres especiais  **\&#42;** e **&amp;**.<br /><br />Todas as consultas que fazem referência a esses objetos também devem usar os nomes com colchetes ou aspas. Por exemplo, a consulta `SELECT * FROM schema` falhará. A consulta correta é: `SELECT * FROM [schema]`.<br /><br />Quando você converte objetos de banco de dados do Access, o painel Saída listará qualquer acessar tabelas que usam as palavras-chave ou caracteres especiais. Você pode modificar as tabelas no Access e, em seguida, remover e adicionar o banco de dados novamente. ou você pode modificar as consultas que referenciam esses objetos para que as consultas usam colchetes ou aspas para delimitar identificadores. Se você não modificar suas consultas, seus aplicativos do Access podem retornar erros ou ter outros problemas.|  
|Tamanhos de campo diferem em relações de chave estrangeira/chave primárias.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a funcionalidade de Jet de vinculação de colunas que têm diferentes tipos de dados ou tamanhos com restrições de chave estrangeira.<br /><br />Quando você converte objetos de banco de dados do Access, a janela de saída listará qualquer primárias restrições de chave estrangeira/chave que não serão convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode alterar os tipos de dados e tamanhos em colunas de acesso para que eles corresponderem e, em seguida, remova e adicione novamente o banco de dados do Access. Ou, você pode migrar dados, embora essas restrições não serão criadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Tabelas referenciadas em relações de acesso tem nenhuma chave primária ou um índice exclusivo.|Acesso aceita a relação entre tabelas em que a tabela referenciada não tem uma chave primária ou um índice exclusivo. No entanto, isso não é suportado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br />Quando você converte objetos de banco de dados do Access, a janela de saída listará todas as tabelas que não têm relações, mas nenhuma chave primária ou índice exclusivo. Você pode alterar as tabelas para adicionar as chaves primárias ou índices exclusivos e, em seguida, remover e adicionar novamente o banco de dados do Access. Ou, você pode migrar dados, embora a relação entre as tabelas será quebrada.|  
|Acessar tabelas tem colunas de hiperlink.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não suporta **hiperlink** colunas. Em vez disso, as colunas são tratadas como colunas de memorando de acesso. Por padrão, essas colunas serão convertidas **nvarchar (max)** colunas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode personalizar o mapeamento. Para obter mais informações, consulte [tipos de dados de destino e origem do mapeamento](mapping-source-and-target-data-types-accesstosql.md).|  
|Expressões de regra de validação ou padrão contêm funções de acesso que não podem ser convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.|As expressões de acesso padrão ou as regras de validação podem incluir funções de sistema de acesso ou funções definidas pelo usuário que não são mapeados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Usando funções que não mapeiam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure impede o carregando o expressões padrão ou as regras de validação em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.|  
  
## <a name="see-also"></a>Consulte também  
[Preparar bancos de dados de acesso para a migração](preparing-access-databases-for-migration-accesstosql.md)  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
