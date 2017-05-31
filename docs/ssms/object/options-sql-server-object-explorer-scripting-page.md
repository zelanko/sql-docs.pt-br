---
title: "Opções (página Pesquisador de Objetos do SQL Server – Scripts) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d5353c0732833516e95cc734a2d7bbe0f1258554
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="options-sql-server-object-explorer---scripting-page"></a>Opções (página Pesquisador de Objetos do SQL Server – Scripts)
Use esta página para definir opções de script que se aplicam aos seguintes comandos nos menus de contexto de objeto no **Pesquisador de Objetos**:  
  
-   Comandos **Editar** para tabelas de usuário e exibições.  
  
-   Comandos **Script <object> as** para objetos criados pelo usuário.  
  
-   Comando **Modificar** para objetos criados pelo usuário.  
  
-   Esta página também define os padrões da opção de script para o **Assistente para Gerar Scripts do SQL Server**.  
  
## <a name="remarks"></a>Comentários  
Os comandos **Editar** e **Modificar** podem gerar resultados diferentes do comando **Script <object> as** para a mesma configuração de opção. Os comandos **Editar** e **Modificar** destinam-se a modificar objetos no banco de dados atual durante uma sessão do Editor de Consultas. O comando **Script <object> as** destina-se a gerar um script de modo que este possa ser usado mais adiante para criar objetos.  
  
## <a name="options"></a>Opções  
Especifique opções de script selecionando as configurações disponíveis na lista à direita de cada opção.  
  
### <a name="general-scripting-options"></a>Opções gerais de script  
**Delimitar instruções individuais**  
Separa instruções [!INCLUDE[tsql](../../includes/tsql_md.md)] individuais usando um separador de lote. Para alterar o separador de lote padrão para o **Editor de Consultas**, selecione **Ferramentas**/**Opções**/**Execução de Consulta**/**SQL Server**/**Geral**/**Separador de lote**. O padrão é Falso. Para obter mais informações, consulte [GO (Transact-SQL)](http://msdn.microsoft.com/en-us/b2ca6791-3a07-4209-ba8e-2248a92dd738).  
  
**Incluir cabeçalhos descritivos**  
Adiciona comentários descritivos ao script separando o script em seções para cada objeto. O padrão é True. Para obter mais informações, consulte [/*...*/ (Comment) (Transact-SQL)](http://msdn.microsoft.com/en-us/4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c).  
  
**Incluir opções vardecimal**  
Inclui as opções de armazenamento vardecimal. O padrão é Falso. Para obter mais informações, consulte [sp_db_vardecimal_storage_format (Transact-SQL)](http://msdn.microsoft.com/en-us/9920b2f7-b802-4003-913c-978c17ae4542).  
  
**Controle de alteração de script**  
Inclui informações de controle de alteração no script.  
  
**Script para a versão do servidor**  
Cria um script que pode ser executado na versão selecionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Recursos que são novos no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] não podem ter seu script executado em versões anteriores. Alguns scripts criados para o [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] não podem ser executados em servidores que estão executando uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ou em um banco de dados que tem uma [configuração de nível de compatibilidade do banco de dados](http://msdn.microsoft.com/en-us/ca5fd220-d5ea-4182-8950-55d4101a86f6)anterior.  
  
**Catálogos de texto completo de script**  
Inclui um script para catálogos de texto completo. O padrão é Falso. Para obter mais informações, veja [CREATE FULLTEXT CATALOG (Transact-SQL)](http://msdn.microsoft.com/en-us/d7a8bd93-e2d7-4a40-82ef-39069e65523b).  
  
**Script USE <database>**  
Adiciona a instrução USE DATABASE ao script para criar objetos do banco de dados no contexto do banco de dados do **Pesquisador de Objetos** atual. Quando se espera que o script seja usado em um banco de dados diferente, selecione Falso para omitir. O padrão é True. Para obter mais informações, consulte [USE (Transact-SQL)](http://msdn.microsoft.com/en-us/c05acac8-c063-4770-8e36-d7f71d500b10).  
  
### <a name="object-scripting-options"></a>Opções de script de objeto  
**Gerar script para objetos dependentes**  
Gera um script para objetos adicionais que são necessários quando o script para o objeto selecionado é executado. O padrão é Falso.  
  
**Incluir cláusula If NOT EXISTS**  
Inclui uma instrução para verificar se cada objeto não existe no banco de dados antes de tentar criar o objeto. O padrão é Falso. Para obter mais informações, consulte [IF...ELSE (Transact-SQL)](http://msdn.microsoft.com/en-us/676c881f-dee1-417a-bc51-55da62398e81) e [EXISTS (Transact-SQL)](http://msdn.microsoft.com/en-us/b6510a65-ac38-4296-a3d5-640db0c27631).  
  
**Qualificar nomes de objetos do esquema**  
Qualifica nomes de objeto com o esquema de objeto. O padrão é Falso. Para obter mais informações, consulte [Criar um esquema de banco de dados](http://msdn.microsoft.com/en-us/ed2a5522-f4d2-4111-95a4-d3e1e5081739).  
  
**Propriedades estendidas do script**  
Inclui propriedades estendidas no script se o objeto possui propriedades estendidas. O padrão é Falso. Para obter mais informações, veja [sp_addextendedproperty (Transact-SQL)](http://msdn.microsoft.com/en-us/565483ea-875b-4133-b327-d0006d2d7b4c).  
  
**Proprietário do script**  
Inclui o proprietário no script gerado. O padrão é Falso.  
  
**Permissões de script**  
Inclui permissões em objetos de banco de dados do script. O padrão é True. Para obter mais informações, consulte [Permissões](http://msdn.microsoft.com/en-us/f28e3dea-24e6-4a81-877b-02ec4c7e36b9).  
  
### <a name="tableview-options"></a>Opções de tabela/exibição  
As opções a seguir são válidas somente para scripts de tabelas ou exibições.  
  
**Converter tipos de dados definidos pelo usuário em tipos de base**  
Converte tipos de dados definidos pelo usuário em tipos de base a partir dos quais foram criados. Use Verdadeiro quando os tipos de dados definidos pelo usuário no banco de dados de origem não existirem no banco de dados em que o script será executado. Use Falso para manter os tipos de dados definidos pelo usuário. O padrão é Falso. Para obter mais informações, veja [CREATE TYPE (Transact-SQL)](http://msdn.microsoft.com/en-us/2202236b-e09f-40a1-bbc7-b8cff7488905).  
  
**Gerar comandos SET ANSI PADDING**  
Adiciona a instrução SET ANSI_PADDING antes e depois de cada instrução CREATE TABLE. O padrão é True. Para obter mais informações, veja [SET ANSI_PADDING (Transact-SQL)](http://msdn.microsoft.com/en-us/92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0).  
  
**Incluir agrupamento**  
Inclui agrupamento na definição de coluna. O padrão é True. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](http://msdn.microsoft.com/en-us/92d34f48-fa2b-47c5-89d3-a4c39b0f39eb).  
  
**Incluir propriedade IDENTITY**  
Inclui definições para semente IDENTITY e incremento IDENTITY. O padrão é True. Para obter mais informações, consulte [IDENTITY (Property) (Transact-SQL)](http://msdn.microsoft.com/en-us/8429134f-c821-4033-a07c-f782a48d501c).  
  
**Qualificar referências de chave estrangeira do esquema**  
Adiciona o nome de esquema a referências de tabela para restrições FOREIGN KEY. O padrão é True.  
  
**Padrões e regras associados por script**  
Inclui as chamadas dos procedimentos armazenados associados **sp_bindefault** e **sp_bindrule** . O padrão é True. Para obter mais informações, consulte [sp_bindefault (Transact-SQL)](http://msdn.microsoft.com/en-us/3da70c10-68d0-4c16-94a5-9e84c4a520f6) e [sp_bindrule (Transact-SQL)](http://msdn.microsoft.com/en-us/2606073e-c52f-498d-a923-5026b9d97e67).  
  
**Restrições de script CHECK**  
Adiciona [Restrições CHECK](http://msdn.microsoft.com/en-us/637098af-2567-48f8-90f4-b41df059833e) ao script. O padrão é True.  
  
**Padrões de script**  
Inclui valores padrão de coluna no script. O padrão é Falso. Para obter mais informações, veja [CREATE DEFAULT (Transact-SQL)](http://msdn.microsoft.com/en-us/08475db4-7d90-486a-814c-01a99d783d41).  
  
**Grupos de arquivos de script**  
Especifica o grupo de arquivos na cláusula ON para definições de tabela. O padrão é Falso. Para obter mais informações, veja [CREATE TABLE (Transact-SQL)](http://msdn.microsoft.com/en-us/1e068443-b9ea-486a-804f-ce7b6e048e8b).  
  
**Chaves estrangeiras do script**  
Inclui [Restrições FOREIGN KEY](http://msdn.microsoft.com/en-us/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd) no script. O padrão é Falso.  
  
**Índices de texto completo do script**  
Inclui índices de texto completo no script. O padrão é Falso. Para obter mais informações, veja [CREATE FULLTEXT INDEX (Transact-SQL)](http://msdn.microsoft.com/en-us/8b80390f-5f8b-4e66-9bcc-cabd653c19fd).  
  
**Índices de script**  
Inclui índices clusterizados, não clusterizados e XML no script. O padrão é True. Para obter mais informações, veja [CREATE INDEX (Transact-SQL)](http://msdn.microsoft.com/en-us/d2297805-412b-47b5-aeeb-53388349a5b9).  
  
**Esquemas de partição de script**  
Inclui esquemas de partição de tabela no script. O padrão é Falso. Para obter mais informações, veja [CREATE PARTITION SCHEME (Transact-SQL)](http://msdn.microsoft.com/en-us/5b21c53a-b4f4-4988-89a2-801f512126e4).  
  
**Chaves primárias de script**  
Inclui [Restrições de chave primária e estrangeira](http://msdn.microsoft.com/en-us/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd) no script. O padrão é True.  
  
**Estatísticas de script**  
Inclui estatísticas definidas pelo usuário no script. O padrão é Falso. Para obter mais informações, veja [CREATE STATISTICS (Transact-SQL)](http://msdn.microsoft.com/en-us/b23e2f6b-076c-4e6d-9281-764bdb616ad2).  
  
**Gatilhos de script**  
Inclui gatilhos no script. O padrão é Falso. Para obter mais informações, veja [CREATE TRIGGER (Transact-SQL)](http://msdn.microsoft.com/en-us/edeced03-decd-44c3-8c74-2c02f801d3e7).  
  
**Chaves exclusivas do script**  
Inclui [Restrições exclusivas e restrições de verificação](http://msdn.microsoft.com/en-us/637098af-2567-48f8-90f4-b41df059833e) no script. O padrão é Falso.  
  
**Colunas de exibição de script**  
Declara colunas de exibição em cabeçalhos de exibição. O padrão é Falso. Para obter mais informações, veja [CREATE VIEW (Transact-SQL)](http://msdn.microsoft.com/en-us/aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9).  
  
**ScriptDriIncludeSystemNames**  
Inclui nomes de restrições geradas pelo sistema para forçar a integridade referencial declarativa. O padrão é Falso. Para obter mais informações, veja [REFERENTIAL_CONSTRAINTS (Transact-SQL)](http://msdn.microsoft.com/en-us/5d358f18-0a85-4b55-af4b-98d5f4cd1020).  
  
## <a name="see-also"></a>Consulte também  
[Gerar scripts (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/9711c617-3c68-4e5a-aea3-befc64d51524)  
  

