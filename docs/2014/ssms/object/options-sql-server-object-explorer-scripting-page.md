---
title: Opções (página Gerenciador de script de objeto do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 74dfa7eec9ed7f014e9baf09cf4ddcf30cd12901
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118030"
---
# <a name="options-sql-server-object-explorer-scripting-page"></a>Opções (página Gerenciador de script de objeto do SQL Server)
  Use esta página para definir opções de script que se aplicam aos seguintes comandos nos menus de contexto de objeto no **Pesquisador de Objetos**:  
  
-   Comandos **Editar** para tabelas de usuário e exibições.  
  
-   **Script \<objeto > como** comandos para objetos criados pelo usuário.  
  
-   Comando **Modificar** para objetos criados pelo usuário.  
  
-   Esta página também define os padrões da opção de script para o **Assistente para Gerar Scripts do SQL Server**.  
  
## <a name="remarks"></a>Remarks  
 O **editar** e **modificar** comandos podem produzir resultados diferentes do **Script \<objeto > como** comando para a mesma configuração de opção. Os comandos **Editar** e **Modificar** destinam-se a modificar objetos no banco de dados atual durante uma sessão do Editor de Consultas. O **Script \<objeto > como** comando é projetado para gerar um script para que ele pode ser usado posteriormente para criar objetos.  
  
## <a name="options"></a>Opções  
 Especifique opções de script selecionando as configurações disponíveis na lista à direita de cada opção.  
  
### <a name="general-scripting-options"></a>Opções gerais de script  
 **Delimitar instruções individuais**  
 Separa instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] individuais usando um separador de lote. Para alterar o separador de lote padrão para o **Editor de Consultas**, selecione **Ferramentas**/**Opções**/**Execução de Consulta**/**SQL Server**/**Geral**/**Separador de lote**. O padrão é Falso. Para obter mais informações, consulte [VÁ &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/sql-server-utilities-statements-go).  
  
 **Incluir cabeçalhos descritivos**  
 Adiciona comentários descritivos ao script separando o script em seções para cada objeto. O padrão é True. Para obter mais informações, consulte [comentário &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/comment-transact-sql).  
  
 **Incluir opções vardecimal**  
 Inclui as opções de armazenamento vardecimal. O padrão é Falso. Para obter mais informações, consulte e [sp_db_vardecimal_storage_format &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql).  
  
 **Controle de alteração de script**  
 Inclui informações de controle de alteração no script.  
  
 **Script para a versão do servidor**  
 Cria um script que pode ser executado na versão selecionada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Recursos que são novos no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] não podem ter seu script executado em versões anteriores. Alguns scripts criados para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] não podem ser executados em servidores que estão executando uma versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ou em um banco de dados que tem uma [configuração de nível de compatibilidade do banco de dados](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)anterior.  
  
 **Catálogos de texto completo de script**  
 Inclui um script para catálogos de texto completo. O padrão é Falso. Para obter mais informações, consulte [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql).  
  
 **USO de script \<banco de dados >**  
 Adiciona a instrução USE DATABASE ao script para criar objetos do banco de dados no contexto do banco de dados do **Pesquisador de Objetos** atual. Quando se espera que o script seja usado em um banco de dados diferente, selecione Falso para omitir. O padrão é True. Para obter mais informações, veja [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
### <a name="object-scripting-options"></a>Opções de script de objeto  
 **Gerar script para objetos dependentes**  
 Gera um script para objetos adicionais que são necessários quando o script para o objeto selecionado é executado. O padrão é Falso.  
  
 **Incluir cláusula If NOT EXISTS**  
 Inclui uma instrução para verificar se cada objeto não existe no banco de dados antes de tentar criar o objeto. O padrão é Falso. Para obter mais informações, consulte [IF... ELSE &#40;Transact-SQL&#41; ](/sql/t-sql/language-elements/if-else-transact-sql) e [EXISTS &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/exists-transact-sql).  
  
 **Qualificar nomes de objetos do esquema**  
 Qualifica nomes de objeto com o esquema de objeto. O padrão é Falso. Para obter mais informações, consulte [Criar um esquema de banco de dados](../../relational-databases/security/authentication-access/create-a-database-schema.md).  
  
 **Propriedades estendidas do script**  
 Inclui propriedades estendidas no script se o objeto possui propriedades estendidas. O padrão é Falso. Para obter mais informações, veja [sp_addextendedproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql).  
  
 **Proprietário do script**  
 Inclui o proprietário no script gerado. O padrão é Falso.  
  
 **Permissões de script**  
 Inclui permissões em objetos de banco de dados do script. O padrão é True. Para obter mais informações, consulte [permissões &#40;mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
### <a name="tableview-options"></a>Opções de tabela/exibição  
 As opções a seguir são válidas somente para scripts de tabelas ou exibições.  
  
 **Converter tipos de dados definidos pelo usuário em tipos de base**  
 Converte tipos de dados definidos pelo usuário em tipos de base a partir dos quais foram criados. Use Verdadeiro quando os tipos de dados definidos pelo usuário no banco de dados de origem não existirem no banco de dados em que o script será executado. Use Falso para manter os tipos de dados definidos pelo usuário. O padrão é Falso. Para obter mais informações, consulte [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql).  
  
 **Gerar comandos SET ANSI PADDING**  
 Adiciona a instrução SET ANSI_PADDING antes e depois de cada instrução CREATE TABLE. O padrão é True. Para obter mais informações, veja [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).  
  
 **Incluir agrupamento**  
 Inclui agrupamento na definição de coluna. O padrão é True. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 **Incluir propriedade IDENTITY**  
 Inclui definições para semente IDENTITY e incremento IDENTITY. O padrão é True. Para obter mais informações, consulte [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property).  
  
 **Qualificar referências de chave estrangeira do esquema**  
 Adiciona o nome de esquema a referências de tabela para restrições FOREIGN KEY. O padrão é True.  
  
 **Padrões e regras associados por script**  
 Inclui as chamadas dos procedimentos armazenados associados **sp_bindefault** e **sp_bindrule** . O padrão é True. Para obter mais informações, consulte [sp_bindefault &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-bindefault-transact-sql) e [sp_bindrule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindrule-transact-sql).  
  
 **Restrições de script CHECK**  
 Adiciona [Restrições CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md) ao script. O padrão é True.  
  
 **Padrões de script**  
 Inclui valores padrão de coluna no script. O padrão é Falso. Para obter mais informações, veja [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
 **Grupos de arquivos de script**  
 Especifica o grupo de arquivos na cláusula ON para definições de tabela. O padrão é Falso. Para obter mais informações, consulte [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
 **Chaves estrangeiras do script**  
 Inclui [Restrições FOREIGN KEY](../../relational-databases/tables/primary-and-foreign-key-constraints.md) no script. O padrão é Falso.  
  
 **Índices de texto completo do script**  
 Inclui índices de texto completo no script. O padrão é Falso. Para obter mais informações, consulte [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql).  
  
 **Índices de script**  
 Inclui índices clusterizados, não clusterizados e XML no script. O padrão é True. Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
 **Esquemas de partição de script**  
 Inclui esquemas de partição de tabela no script. O padrão é Falso. Para obter mais informações, consulte [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-partition-scheme-transact-sql).  
  
 **Chaves primárias de script**  
 Inclui [Restrições de chave primária e estrangeira](../../relational-databases/tables/primary-and-foreign-key-constraints.md) no script. O padrão é True.  
  
 **Estatísticas de script**  
 Inclui estatísticas definidas pelo usuário no script. O padrão é Falso. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Gatilhos de script**  
 Inclui gatilhos no script. O padrão é Falso. Para obter mais informações, veja [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
 **Chaves exclusivas do script**  
 Inclui [Restrições exclusivas e restrições de verificação](../../relational-databases/tables/unique-constraints-and-check-constraints.md) no script. O padrão é Falso.  
  
 **Colunas de exibição de script**  
 Declara colunas de exibição em cabeçalhos de exibição. O padrão é Falso. Para obter mais informações, veja [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql).  
  
 **ScriptDriIncludeSystemNames**  
 Inclui nomes de restrições geradas pelo sistema para forçar a integridade referencial declarativa. O padrão é Falso. Para obter mais informações, consulte [REFERENTIAL_CONSTRAINTS &#40;Transact-SQL&#41;](/sql/relational-databases/system-information-schema-views/referential-constraints-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [Gerar scripts &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)  
  
  
