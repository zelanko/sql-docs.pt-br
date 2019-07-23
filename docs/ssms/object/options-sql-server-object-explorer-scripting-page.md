---
title: Opções (página Pesquisador de Objetos do SQL Server – Scripts) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ccd2812261b4d71fb7553f3f1ab40216cc89016
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264057"
---
# <a name="options-sql-server-object-explorer---scripting-page"></a>Opções (página Pesquisador de Objetos do SQL Server – Scripts)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use esta página para definir opções de script que se aplicam aos seguintes comandos nos menus de contexto de objeto no **Pesquisador de Objetos**:  
  
-   Comandos **Editar** para tabelas de usuário e exibições.  
  
-   Comandos **Script <object> as** para objetos criados pelo usuário.  
  
-   Comando **Modificar** para objetos criados pelo usuário.  
  
-   Esta página também define os padrões da opção de script para o **Assistente para Gerar Scripts do SQL Server**.  
  
## <a name="remarks"></a>Remarks  
Os comandos **Editar** e **Modificar** podem gerar resultados diferentes do comando **Script <object> as** para a mesma configuração de opção. Os comandos **Editar** e **Modificar** destinam-se a modificar objetos no banco de dados atual durante uma sessão do Editor de Consultas. O comando **Script <object> as** destina-se a gerar um script de modo que este possa ser usado mais adiante para criar objetos.  
  
## <a name="options"></a>Opções  
Especifique opções de script selecionando as configurações disponíveis na lista à direita de cada opção.  
  
### <a name="general-scripting-options"></a>Opções de script gerais  
**Delimitar instruções individuais**  
Separa instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] individuais usando um separador de lote. Para alterar o separador de lote padrão para o **Editor de Consultas**, selecione **Ferramentas**/**Opções**/**Execução de Consulta**/**SQL Server**/**Geral**/**Separador de lote**. O padrão é Falso. Para obter mais informações, consulte [GO (Transact-SQL)](https://msdn.microsoft.com/b2ca6791-3a07-4209-ba8e-2248a92dd738).  
  
**Incluir cabeçalhos descritivos**  
Adiciona comentários descritivos ao script separando o script em seções para cada objeto. O padrão é True. Para obter mais informações, consulte [/ *...* / (Comment) (Transact-SQL)](https://msdn.microsoft.com/4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c).  
  
**Incluir a habilitação da compactação vardecimal**  
Inclui as opções de armazenamento vardecimal. O padrão é Falso. Para obter mais informações, consulte [sp_db_vardecimal_storage_format (Transact-SQL)](https://msdn.microsoft.com/9920b2f7-b802-4003-913c-978c17ae4542).  
  
**Controle de alteração de script**  
Inclui informações de controle de alteração no script.  
  
**Catálogos de texto completo de script**  
Inclui um script para catálogos de texto completo. O padrão é Falso. Para obter mais informações, veja [CREATE FULLTEXT CATALOG (Transact-SQL)](https://msdn.microsoft.com/d7a8bd93-e2d7-4a40-82ef-39069e65523b).  
  
**Script USE <database>**  
Adiciona a instrução USE DATABASE ao script para criar objetos do banco de dados no contexto do banco de dados do **Pesquisador de Objetos** atual. Quando se espera que o script seja usado em um banco de dados diferente, selecione Falso para omitir. O padrão é True. Para obter mais informações, consulte [USE (Transact-SQL)](https://msdn.microsoft.com/c05acac8-c063-4770-8e36-d7f71d500b10).  
  
### <a name="object-scripting-options"></a>Opções de script de objeto  

**Verificar a existência do objeto** Verifique se existe um objeto com o nome fornecido antes de remover ou alterar ou se um objeto com esse nome não existe antes de criar. Para obter mais informações, consulte [IF...ELSE (Transact-SQL)](https://msdn.microsoft.com/676c881f-dee1-417a-bc51-55da62398e81) e [EXISTS (Transact-SQL)](https://msdn.microsoft.com/b6510a65-ac38-4296-a3d5-640db0c27631).

**Gerar script para objetos dependentes**  
Gera um script para objetos adicionais que são necessários quando o script para o objeto selecionado é executado. O padrão é Falso.  
  
**Qualificar nomes de objetos do esquema**  
Qualifica nomes de objeto com o esquema de objeto. O padrão é Falso. Para obter mais informações, consulte [Criar um esquema de banco de dados](../../relational-databases/security/authentication-access/create-a-database-schema.md).  

**Opções de compactação de dados de script** inclui opções de compactação de dados no script. O padrão é Falso.

**Propriedades estendidas do script**  
Inclui propriedades estendidas no script se o objeto possui propriedades estendidas. O padrão é Falso. Para obter mais informações, veja [sp_addextendedproperty (Transact-SQL)](https://msdn.microsoft.com/565483ea-875b-4133-b327-d0006d2d7b4c).  
  
**Proprietário do script**  
Inclui o proprietário no script gerado. O padrão é Falso.  
  
**Permissões de script**  
Inclui permissões em objetos de banco de dados do script. O padrão é True. Para obter mais informações, consulte [Permissões](../../relational-databases/security/permissions-database-engine.md).  
  
### <a name="tableview-options"></a>Opções de tabela/exibição  
As opções a seguir são válidas somente para scripts de tabelas ou exibições.  
  
**Converter tipos de dados definidos pelo usuário em tipos de base**  
Converte tipos de dados definidos pelo usuário em tipos de base a partir dos quais foram criados. Use Verdadeiro quando os tipos de dados definidos pelo usuário no banco de dados de origem não existirem no banco de dados em que o script será executado. Use Falso para manter os tipos de dados definidos pelo usuário. O padrão é Falso. Para obter mais informações, veja [CREATE TYPE (Transact-SQL)](https://msdn.microsoft.com/2202236b-e09f-40a1-bbc7-b8cff7488905).  
  
**Gerar comandos SET ANSI PADDING**  
Adiciona a instrução SET ANSI_PADDING antes e depois de cada instrução CREATE TABLE. O padrão é True. Para obter mais informações, veja [SET ANSI_PADDING (Transact-SQL)](https://msdn.microsoft.com/92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0).  
  
**Incluir ordenação**  
Inclui ordenação na definição de coluna. O padrão é True. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
**Incluir propriedade IDENTITY**  
Inclui definições para semente IDENTITY e incremento IDENTITY. O padrão é True. Para obter mais informações, consulte [IDENTITY (Property) (Transact-SQL)](https://msdn.microsoft.com/8429134f-c821-4033-a07c-f782a48d501c).  
  
**Qualificar referências de chave estrangeira do esquema**  
Adiciona o nome de esquema a referências de tabela para restrições FOREIGN KEY. O padrão é True.  
  
**Padrões e regras associados por script**  
Inclui as chamadas dos procedimentos armazenados associados **sp_bindefault** e **sp_bindrule** . O padrão é True. Para obter mais informações, consulte [sp_bindefault (Transact-SQL)](https://msdn.microsoft.com/3da70c10-68d0-4c16-94a5-9e84c4a520f6) e [sp_bindrule (Transact-SQL)](https://msdn.microsoft.com/2606073e-c52f-498d-a923-5026b9d97e67).  
  
**Restrições de script CHECK**  
Adiciona [Restrições CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md) ao script. O padrão é True.  
  
**Padrões de script**  
Inclui valores padrão de coluna no script. O padrão é Falso. Para obter mais informações, veja [CREATE DEFAULT (Transact-SQL)](https://msdn.microsoft.com/08475db4-7d90-486a-814c-01a99d783d41).  
  
**Grupos de arquivos de script**  
Especifica o grupo de arquivos na cláusula ON para definições de tabela. O padrão é Falso. Para obter mais informações, veja [CREATE TABLE (Transact-SQL)](https://msdn.microsoft.com/1e068443-b9ea-486a-804f-ce7b6e048e8b).  
  
**Chaves estrangeiras do script**  
Inclui [Restrições FOREIGN KEY](../../relational-databases/tables/primary-and-foreign-key-constraints.md) no script. O padrão é Falso.  
  
**Índices de texto completo do script**  
Inclui índices de texto completo no script. O padrão é Falso. Para obter mais informações, veja [CREATE FULLTEXT INDEX (Transact-SQL)](https://msdn.microsoft.com/8b80390f-5f8b-4e66-9bcc-cabd653c19fd).  
  
**Índices de script**  
Inclui índices clusterizados, não clusterizados e XML no script. O padrão é True. Para obter mais informações, veja [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/d2297805-412b-47b5-aeeb-53388349a5b9).  
  
**Esquemas de partição de script**  
Inclui esquemas de partição de tabela no script. O padrão é Falso. Para obter mais informações, veja [CREATE PARTITION SCHEME (Transact-SQL)](https://msdn.microsoft.com/5b21c53a-b4f4-4988-89a2-801f512126e4).  
  
**Chaves primárias de script**  
Inclui [Restrições de chave primária e estrangeira](../../relational-databases/tables/primary-and-foreign-key-constraints.md) no script. O padrão é True.  
  
**Estatísticas de script**  
Inclui estatísticas definidas pelo usuário no script. O padrão é Falso. Para obter mais informações, veja [CREATE STATISTICS (Transact-SQL)](https://msdn.microsoft.com/b23e2f6b-076c-4e6d-9281-764bdb616ad2).  
  
**Gatilhos de script**  
Inclui gatilhos no script. O padrão é Falso. Para obter mais informações, veja [CREATE TRIGGER (Transact-SQL)](https://msdn.microsoft.com/edeced03-decd-44c3-8c74-2c02f801d3e7).  
  
**Chaves exclusivas do script**  
Inclui [Restrições exclusivas e restrições de verificação](../../relational-databases/tables/unique-constraints-and-check-constraints.md) no script. O padrão é Falso.  
  
**Colunas de exibição de script**  
Declara colunas de exibição em cabeçalhos de exibição. O padrão é Falso. Para obter mais informações, veja [CREATE VIEW (Transact-SQL)](https://msdn.microsoft.com/aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9).  
  
**Incluir nomes de sistema dri**  
Inclui nomes de restrições geradas pelo sistema para forçar a integridade referencial declarativa. O padrão é Falso. Para obter mais informações, veja [REFERENTIAL_CONSTRAINTS (Transact-SQL)](https://msdn.microsoft.com/5d358f18-0a85-4b55-af4b-98d5f4cd1020).  
  
### <a name="version-options"></a>Opções de versão

**Corresponder as configurações de script com a origem** Se habilitado, a versão de destino, a edição do mecanismo e o tipo de mecanismo dos scripts gerados serão definidos com os valores do servidor do objeto que está sendo inserido no script. Isso desabilitará (e ignorará) as outras opções de versão. 

**Script para edição do mecanismo de banco de dados** Scripts gerados serão direcionados para a [Edição do mecanismo](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.edition.aspx) especificada.

**Script para tipo de mecanismo de banco de dados** Scripts gerados serão direcionados para o [Tipo do mecanismo de banco de dados](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.databaseenginetype.aspx) especificado.

**Script para a versão do servidor**  
Scripts gerados serão direcionados para a versão especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Recursos que são novos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não podem ter seu script executado em versões anteriores. Alguns scripts criados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não podem ser executados em servidores que estão executando uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou em um banco de dados que tem uma [configuração de nível de compatibilidade do banco de dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)anterior.  

## <a name="see-also"></a>Confira também  
[Gerar scripts (SQL Server Management Studio)](https://msdn.microsoft.com/9711c617-3c68-4e5a-aea3-befc64d51524)  
  
