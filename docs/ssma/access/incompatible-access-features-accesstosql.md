---
title: Recursos de acesso incompatíveis (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2cc48fa530730beec07aaca4bfb933c9ff8fb2b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67986349"
---
# <a name="incompatible-access-features-accesstosql"></a>Recursos de acesso incompatíveis (AccessToSQL)
Nem todos os recursos do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do Access são compatíveis com o. Por exemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o acesso tem diferentes conjuntos de palavras-chave reservadas. Problemas como esses podem impedir uma migração bem-sucedida para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o. Use a tabela a seguir para saber mais sobre possíveis problemas de migração e o que você pode fazer sobre eles.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>Configurações de banco de dados ou recursos que podem afetar a migração  
  
|Configuração ou recurso do banco de dados de acesso|Problema de migração|  
|--------------------------------------|-------------------|  
|As tabelas do Access não têm índices exclusivos.|Se uma tabela que não tem um índice exclusivo for migrada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o, você não poderá modificar a tabela após a migração. Isso pode levar a problemas de compatibilidade de aplicativos.<br /><br />Quando você converte objetos de banco de dados do Access, a janela saída listará todas as tabelas de acesso que não têm índices exclusivos.<br /><br />Você pode configurar o acesso para adicionar uma chave primária na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela durante a conversão. Para obter mais informações, consulte [configurações do projeto (conversão)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388).|  
|As tabelas do Access têm colunas de replicação.|Se uma tabela de acesso que inclui colunas do sistema de replicação for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]migrada para o, a funcionalidade de replicação do Jet será interrompida após a migração.<br /><br />Após a migração, considere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o uso da replicação para manter cópias sincronizadas dos bancos de dados.|  
|As tabelas do Access com índices exclusivos contêm vários valores nulos.|As tabelas do Access com índices exclusivos com vários valores nulos não podem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ser transferidas para, porque no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os índices exclusivos não permitem vários nulos. A migração falhará para essas tabelas.<br /><br />O SSMA sinalizará esse problema nos relatórios de avaliação. Para criar um relatório de avaliação, consulte [avaliando objetos de banco de dados do Access para conversão](assessing-access-database-objects-for-conversion-accesstosql.md).<br /><br />Se esse problema existir, você deverá certificar-se de que a chave primária não tenha valores nulos duplicados. Ou, você deve remover a chave primária ou os índices exclusivos que contêm vários valores nulos.|  
|As tabelas do Access contêm valores de data fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo.|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **DateTime** aceita datas no intervalo de 1 Jan 1753 a 31 Dec 9999 apenas. O Access aceita datas no intervalo de 1 Jan 100 a 31 Dec 9999.<br /><br />O SSMA sinalizará esse problema nos relatórios de avaliação. Para criar um relatório de avaliação, consulte [avaliando objetos de banco de dados do Access para conversão](assessing-access-database-objects-for-conversion-accesstosql.md).<br /><br />Você pode configurar como o SSMA resolve as datas que estão fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo. Para obter mais informações, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).|  
|Os comprimentos de índice no Access excedem 900 bytes.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]os índices têm um limite de 900 bytes para o tamanho total das colunas de chave de índice. Se as tabelas do Access usarem índices maiores, o SSMA exibirá um aviso.<br /><br />Se você continuar com a migração de dados, a migração poderá falhar.|  
|Os nomes de objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Access são palavras-chave ou contêm caracteres especiais.|Acesse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tenha diferentes conjuntos de palavras-chave reservadas e caracteres especiais. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o aceitará objetos que são nomeados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando palavras-chave ou que contêm caracteres especiais se você usar identificadores entre colchetes ou entre aspas, como "Select" ou [SELECT]. p. Para obter mais informações, consulte "identificadores delimitados (Mecanismo de Banco de Dados) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " nos manuais online do.<br /><br />**Observação:** Para usar aspas para delimitar identificadores, defina QUOTED_IDENTIFIER deve estar ativado.<br /><br />Por exemplo, `CREATE TABLE [schema](c1 [FOR])` é uma instrução válida, embora o **esquema** e o **para** sejam palavras-chave reservadas. Além disso `CREATE TABLE [xxx*yyy](c1 x&y)` , é uma instrução válida, embora o nome da tabela e da coluna contenha os caracteres ** \&especiais #42;** e. **&amp;**<br /><br />Todas as consultas que fazem referência a esses objetos também devem usar os nomes com colchetes ou aspas. Por exemplo, a consulta `SELECT * FROM schema` falhará. A consulta correta é: `SELECT * FROM [schema]`.<br /><br />Quando você converte objetos de banco de dados do Access, o painel saída listará todas as tabelas de acesso que usam palavras-chave ou caracteres especiais. Você pode modificar as tabelas no Access e, em seguida, remover e adicionar o banco de dados novamente; ou você pode modificar consultas que fazem referência a esses objetos para que as consultas usem colchetes ou aspas para delimitar identificadores. Se você não modificar suas consultas, seus aplicativos de acesso poderão retornar erros ou ter outros problemas.|  
|Os tamanhos de campo diferem em relações de chave primária/Foreign Key.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o não oferece suporte à funcionalidade Jet de vinculação de colunas que têm diferentes tipos de dados ou tamanhos com restrições Foreign Key.<br /><br />Quando você converte objetos de banco de dados do Access, a janela saída listará todas as restrições de chave primária/chave estrangeira [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]que não serão convertidas em. Você pode alterar os tipos e tamanhos de dados em colunas de acesso para que eles correspondam e, em seguida, removam e adicionem novamente o banco de dado do Access. Ou, você pode migrar dados embora essas restrições não sejam criadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|As tabelas referenciadas nas relações de acesso não têm uma chave primária nem um índice exclusivo.|O acesso aceita a relação entre as tabelas em que a tabela referenciada não tem uma chave primária ou um índice exclusivo. No entanto, isso não é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]suportado pelo.<br /><br />Quando você converte objetos de banco de dados do Access, a janela saída listará todas as tabelas que têm relações, mas nenhuma chave primária ou índice exclusivo. Você pode alterar as tabelas para adicionar chaves primárias ou índices exclusivos e, em seguida, remover e adicionar novamente o banco de dados do Access. Ou, você pode migrar dados, embora a relação entre as tabelas seja interrompida.|  
|As tabelas do Access têm colunas de hiperlink.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não oferece suporte a colunas de **hiperlink** . Em vez disso, as colunas são tratadas como colunas de memorando de acesso. Por padrão, essas colunas serão convertidas em colunas **nvarchar (max)** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode personalizar o mapeamento. Para obter mais informações, consulte [mapeando tipos de dados de origem e de destino](mapping-source-and-target-data-types-accesstosql.md).|  
|As expressões de regra padrão ou de validação contêm funções de acesso que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser convertidas para ou SQL Azure.|Acessar expressões padrão ou regras de validação podem incluir funções do sistema de acesso ou funções definidas pelo usuário que não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são mapeadas para ou SQL Azure. O uso de funções que não são [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeadas para ou SQL Azure impedirá que você carregue as expressões padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou regras de validação no ou SQL Azure.|  
  
## <a name="see-also"></a>Consulte Também  
[Preparar bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md)  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
