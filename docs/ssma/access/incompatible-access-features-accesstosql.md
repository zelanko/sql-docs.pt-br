---
title: "Recursos de acesso incompatível (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b60bab1d71142a74c8558ce05a6ca96451e7cfc9
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="incompatible-access-features-accesstosql"></a>Recursos de acesso incompatível (AccessToSQL)
Nem todos os recursos de banco de dados do Access são compatíveis com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Por exemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e acesso têm conjuntos diferentes de palavras-chave reservadas. Problemas, como eles podem impedir uma migração bem-sucedida para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Use a tabela a seguir para saber mais sobre problemas de migração possíveis e que você pode fazer sobre eles.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>Configurações de banco de dados ou recursos que podem afetar a migração  
  
|Configuração de banco de dados ou o recurso de acesso|Problema de migração|  
|--------------------------------------|-------------------|  
|Tabelas do Access não têm índices exclusivos.|Se uma tabela que não tem um índice exclusivo é migrada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você não pode modificar a tabela após a migração. Isso pode levar a problemas de compatibilidade do aplicativo.<br /><br />Quando você converte objetos de banco de dados do Access, a janela de saída listará qualquer acessar tabelas que não têm índices exclusivos.<br /><br />Você pode configurar o acesso para adicionar uma chave primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tabela durante a conversão. Para obter mais informações, consulte [configurações do projeto (conversão)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388).|  
|Acessar tabelas têm colunas de replicação.|Se uma tabela do Access que inclui colunas de sistema de replicação é migrada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], funcionalidade de replicação do Jet será interrompida após a migração.<br /><br />Após a migração, considere o uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] replicação para manter cópias sincronizadas de seus bancos de dados.|  
|Acessar tabelas com índices exclusivos contenham diversos valores nulos.|Acessar tabelas com índices exclusivos com vários valores nulos não podem ser transferidas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], pois em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], índices exclusivos não permitir vários nulos. Migração falhará para essas tabelas.<br /><br />O SSMA marcará esse problema nos relatórios de avaliação. Para criar um relatório de avaliação, consulte [avaliar objetos do banco de dados do Access para conversão](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441).<br /><br />Se esse problema, você deve se certificar que a chave primária não tem valores duplicados de nulo. Ou, você deve remover a chave primária ou índices exclusivos que contêm vários valores nulos.|  
|Acessar tabelas contêm valores de data que estão fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intervalo.|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime** tipo aceita datas no intervalo de 1 de janeiro de 1753 a 31 de dezembro 9999 apenas. Acesso aceita datas no intervalo de 100 1 de janeiro a 31 de dezembro 9999.<br /><br />O SSMA marcará esse problema nos relatórios de avaliação. Para criar um relatório de avaliação, consulte [avaliar objetos do banco de dados do Access para conversão](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441).<br /><br />Você pode configurar como o SSMA resolve as datas que estão fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intervalo. Para obter mais informações, consulte [configurações do projeto (migração)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).|  
|Comprimentos de índice no Access excederem 900 bytes.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]os índices têm um limite de 900 bytes para o tamanho total das colunas de chave de índice. Se suas tabelas do Access usam índices maiores, o SSMA exibirá um aviso.<br /><br />Se você continuar com a migração de dados, a migração poderá falhar.|  
|Os nomes de objeto de acesso são [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] palavras-chave, ou conter caracteres especiais.|Acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] têm conjuntos diferentes de palavras-chave reservadas e caracteres especiais. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]aceitará objetos que são nomeados usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] palavras-chave ou que contenham caracteres especiais se você usa identificadores entre colchetes ou entre aspas, como "select" ou [Selecionar]. p. Para obter mais informações, consulte "Identificadores de delimitado (mecanismo de banco de dados)" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.<br /><br />**Observação:** para usar aspas para delimitar identificadores, SET QUOTED_IDENTIFIER deve estar ON.<br /><br />Por exemplo, `CREATE TABLE [schema](c1 [FOR])` é uma instrução válida, embora **esquema** e **para** são palavras-chave reservadas. Além disso, `CREATE TABLE [xxx*yyy](c1 x&y)` é uma instrução válida, mesmo que o nome de tabela e coluna contenha os caracteres especiais  **\&#42;** e  **&amp;** .<br /><br />Todas as consultas que fazem referência a esses objetos também devem usar os nomes com colchetes ou aspas. Por exemplo, a consulta `SELECT * FROM schema` falhará. A consulta correta é: `SELECT * FROM [schema]`.<br /><br />Quando você converte objetos de banco de dados do Access, o painel Saída listará qualquer acessar tabelas que usam as palavras-chave ou caracteres especiais. Você pode modificar as tabelas no Access e, em seguida, remover e adicionar o banco de dados novamente. ou você pode modificar as consultas que referenciam esses objetos para que as consultas usam colchetes ou aspas para delimitar identificadores. Se você não modificar suas consultas, seus aplicativos do Access podem retornar erros ou ter outros problemas.|  
|Tamanhos de campo diferem primárias/chave relações de chave estrangeira.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]não oferece suporte à funcionalidade de Jet de vinculação colunas que têm diferentes tipos de dados ou tamanhos com restrições de chave estrangeira.<br /><br />Quando você converte objetos de banco de dados do Access, a janela de saída listará qualquer primárias restrições de chave key/foreign que não serão convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você pode alterar os tipos de dados e tamanhos em colunas de acesso para que eles corresponderem e, em seguida, remova e adicione novamente o banco de dados. Ou, você pode migrar dados apesar dessas restrições não serão criadas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|Tabelas referenciadas em relações de acesso tem uma chave primária, nem um índice exclusivo.|Acesso aceita a relação entre tabelas em que a tabela referenciada não tem uma chave primária ou um índice exclusivo. No entanto, isso não é suportado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br />Quando você converte objetos de banco de dados do Access, a janela de saída listará todas as tabelas que não têm relações, mas nenhuma chave primária ou índice exclusivo. Você pode alterar as tabelas para adicionar as chaves primárias ou índices exclusivos e, em seguida, remover e adicionar novamente o banco de dados. Ou, você pode migrar dados apesar da relação entre as tabelas será quebrada.|  
|Acessar tabelas têm colunas de hiperlink.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]não oferece suporte a **hiperlink** colunas. Em vez disso, as colunas são tratadas como colunas de memorando de acesso. Por padrão, essas colunas serão convertidas em **nvarchar (max)** colunas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você pode personalizar o mapeamento. Para obter mais informações, consulte [tipos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).|  
|Expressões de regra padrão ou validação contêm funções de acesso que não podem ser convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.|Expressões de padrão de acesso ou as regras de validação podem incluir funções de sistema de acesso ou funções definidas pelo usuário que não são mapeados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Usando funções que não são mapeados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure impede o carregamento expressões padrão ou as regras de validação em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.|  
  
## <a name="see-also"></a>Consulte também  
[Preparar bancos de dados do Access para a migração](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

