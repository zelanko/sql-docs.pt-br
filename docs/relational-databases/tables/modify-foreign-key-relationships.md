---
title: Modificar relações de chave estrangeira | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65538
- vdt.ppg.relationships
helpviewer_keywords:
- foreign keys [SQL Server], modifying
- modifying foreign keys
ms.assetid: 0c9ca80d-d79b-44c4-a21e-0fce39c398ec
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: efe69599607fc60caf583ad8c2f57ca5e85bd05a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="modify-foreign-key-relationships"></a>Modificar relações de chave estrangeira
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode modificar parte da chave estrangeira de uma relação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Modificar a chave estrangeira de uma tabela altera as colunas que estão relacionadas às colunas na tabela de chaves primárias.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para modificar uma chave estrangeira usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 A nova coluna de chave estrangeira deve corresponder ao tipo de dados e ao tamanho da coluna de chave primária à qual está relacionada, com estas exceções:  
  
-   Uma coluna **char** ou **sysname** pode estar relacionada a uma coluna **varchar** .  
  
-   Uma coluna **binary** pode estar relacionada a uma coluna **varbinary** .  
  
-   Um tipo de dados de alias pode estar relacionado ao seu tipo base.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-foreign-key"></a>Para modificar uma chave estrangeira  
  
1.  No **Pesquisador de Objetos**, expanda a tabela com a chave estrangeira e expanda **Chaves**.  
  
2.  Clique com o botão direito do mouse na chave estrangeira a ser modificada e selecione **Modificar**.  
  
3.  Na caixa de diálogo **Relações de Chaves Estrangeiras** , você pode fazer as modificações a seguir.  
  
     **Relações Selecionadas**  
     Lista de relações existentes. Selecione uma relação para mostrar as propriedades na grade à direita. Se a lista estiver vazia, nenhuma relação foi definida para a tabela.  
  
     **Adicionar**  
     Crie uma nova relação. As **Especificações de Tabelas e Colunas** devem ser definidas antes de a relação tornar-se válida.  
  
     **Delete (excluir)**  
     Exclua a relação selecionada na lista de **Relações Selecionadas** . Para cancelar a adição de uma relação, use esse botão para remover a relação.  
  
     **Categoria Geral**  
     Expanda para mostrar **Verificar Dados Existentes ao Criar ou Habilitar Novamente** e **Especificações de Tabelas e Colunas**.  
  
     **Check Existing Data on Creation or Re-Enabling**  
     Verifique todos os dados anteriores existentes na tabela quando a restrição foi criada ou habilitada novamente, em relação à restrição.  
  
     **Categoria de Especificações de Tabelas e Colunas**  
     Expanda para mostrar quais colunas de quais tabelas atuam como a chave estrangeira e chave primária (ou exclusiva) na relação. Para editar ou definir esses valores, clique no botão de reticências (**…**) à direita do campo de propriedade.  
  
     **Tabela Base de Chaves Estrangeiras**  
     Mostra qual tabela contém a coluna que atua como uma chave estrangeira na relação selecionada.  
  
     **Colunas de Chave Estrangeira**  
     Mostra qual coluna atua como uma chave estrangeira na relação selecionada.  
  
     **Tabela Base de Chaves Primárias/Exclusivas**  
     Mostra qual tabela contém a coluna que atua como uma chave primária (ou exclusiva) na relação selecionada.  
  
     **Colunas de Chaves Primárias/Exclusivas**  
     Mostra qual coluna atua como uma chave primária (ou exclusiva) na relação selecionada.  
  
     **Categoria de identidade**  
     Expanda para mostrar os campos de propriedade para **Nome** e **Descrição**.  
  
     **Nome**  
     Mostra o nome da relação. Quando uma nova relação é criada, é determinado um nome padrão com base na tabela na janela ativa em **Designer de Tabela**. O nome pode ser alterado a qualquer momento.  
  
     **Descrição**  
     Descreve a relação. Para redigir uma descrição mais detalhada, clique em **Descrição** e nas reticências **(...)** que aparecem à direita do campo de propriedade. Isso criará uma área maior para a redação do texto.  
  
     **Categoria do Designer de Tabelas**  
     Expanda para mostrar informações por **Verificar Dados Existentes ao Criar ou Habilitar Novamente** e **Impor para Replicação**.  
  
     **Enforce For Replication**  
     Indica se a restrição será imposta quando um agente de replicação realizar uma inserção, atualização ou exclusão na tabela.  
  
     **Impor Restrição de Chave Estrangeira**  
     Especifique se alterações são permitidas para dados das colunas na relação, caso as alterações invalidem a integridade da relação de chave estrangeira. Escolha **Sim** se não deseja permitir mudanças, e escolha **Não** se deseja permiti-las.  
  
     **Categoria de Especificação INSERT e UPDATE**  
     Expanda para mostrar informações pelo **Excluir Regra** e o **Atualizar Regra** para a relação.  
  
     **Excluir Regra**  
     Especifique o que acontece se um usuário tenta excluir uma linha com dados que é envolvida em uma relação de chave estrangeira:  
  
    -   **Sem Ação** Uma mensagem de erro avisa ao usuário que a exclusão não é permitida e o DELETE será revertido.  
  
    -   **Cascata** Exclui todas as linhas que contêm dados envolvidos na relação de chave estrangeira. Não especifique CASCADE se a tabela for incluída em uma publicação de mesclagem que usa registros lógicos.  
  
    -   **Definir Nulo** Definirá o valor como nulo se todas as colunas de chave estrangeira da tabela puderem aceitar valores nulos.  
  
    -   **Definir Padrão** Definirá o valor para o valor padrão definido para a coluna, se todas as colunas de chave estrangeira para a tabela possuírem padrões definidos.  
  
     **Atualizar Regra**  
     Especifique o que ocorre se um usuário tenta atualizar uma linha com dados que é envolvida em uma relação de chave estrangeira:  
  
    -   **Sem Ação** Uma mensagem de erro avisa ao usuário que a atualização não é permitida e o UPDATE será revertido.  
  
    -   **Cascata** Atualiza todas as linhas que contêm dados envolvidos na relação de chave estrangeira. Não especifique CASCADE se a tabela for incluída em uma publicação de mesclagem que usa registros lógicos.  
  
    -   **Definir Nulo** Definirá o valor como nulo se todas as colunas de chave estrangeira da tabela puderem aceitar valores nulos.  
  
    -   **Definir Padrão** Define o valor como o valor padrão que é definido para a coluna se todas as colunas de chave estrangeira para a tabela têm padrões definidos.  
  
4.  No menu **Arquivo**, clique em **Salvar***nome da tabela*.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para modificar uma chave estrangeira**  
  
 Para modificar uma restrição FOREIGN KEY usando o Transact-SQL, exclua primeiramente a FOREIGN KEY já existente e, em seguida, recrie-a com a nova definição. Para obter mais informações, consulte [Delete Foreign Key Relationships](../../relational-databases/tables/delete-foreign-key-relationships.md) e [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md).  
  
###  <a name="TsqlExample"></a>  
