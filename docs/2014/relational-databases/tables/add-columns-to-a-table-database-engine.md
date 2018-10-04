---
title: Adicionar colunas a uma tabela (mecanismo de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- adding columns
ms.assetid: abeb8d52-d562-4e29-9e1e-2923ae874859
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 05ecf02c8fcc706e2f3823fd52538e375a091019
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124306"
---
# <a name="add-columns-to-a-table-database-engine"></a>Adicionar colunas a uma tabela (Mecanismo de Banco de Dados)
  Este tópico descreve como adicionar novas colunas a uma tabela no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para inserir colunas, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Usar a instrução ALTER TABLE para adicionar colunas a uma tabela automaticamente adiciona essas colunas ao final da tabela. Se você desejar que as colunas fiquem em uma ordem específica na tabela, use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, observe que esta não é uma prática recomendada de design de banco de dados. A prática recomendada é especificar a ordem em que as colunas serão retornadas nos níveis de aplicativo e de consulta. Você não deve confiar no uso de SELECT * para retornar todas as colunas na ordem esperada com base na ordem em que são definidas na tabela. Sempre especifique as colunas por nome em suas consultas e aplicativos na ordem em que você gostaria que elas aparecessem.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-insert-columns-into-a-table-with-table-designer"></a>Para inserir colunas em uma tabela com o Designer de Tabela  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela à qual você deseja adicionar colunas e selecione **Design**.  
  
2.  Clique na primeira célula vazia da coluna **Nome da Coluna** .  
  
3.  Digite o nome de coluna na célula. O nome da coluna é um valor obrigatório.  
  
4.  Pressione a tecla TAB para ir para a célula **Tipo de Dados** e selecione um tipo de dados no menu suspenso. Trata-se também de um valor obrigatório, e será atribuído o valor padrão caso você não selecione um.  
  
    > [!NOTE]  
    >  O valor padrão de **Opções** pode ser alterado na caixa de diálogo de **Ferramentas do Banco de Dados**.  
  
5.  Prossiga com a definição de outras propriedades de coluna na guia **Propriedades da Coluna** .  
  
    > [!NOTE]  
    >  Valores padrão de propriedades de coluna são adicionados quando uma nova coluna é criada. Contudo, é possível alterá-los na guia **Propriedades da Coluna** .  
  
6.  Quando tiver terminado de adicionar colunas, do **arquivo** menu, escolha **Salvar * * * nome da tabela*.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-insert-columns-into-a-table"></a>Para inserir colunas em uma tabela  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  O exemplo a seguir adiciona duas colunas à tabela `dbo.doc_exa`. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
```  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL, column_c INT NULL ;  
```  
  
##  <a name="FollowUp"></a> Para obter mais informações, consulte [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
