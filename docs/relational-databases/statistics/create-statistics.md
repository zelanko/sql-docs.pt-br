---
title: Criar estatísticas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.stat.properties.f1
- sql13.swb.statistics.filter.f1
- sql13.swb.stat.columns.f1
- sql13.swb.statistics.propertis.f1
helpviewer_keywords:
- creating statistics
- statistics [SQL Server], creating
ms.assetid: 95a455fb-664d-4c95-851e-c6b62d7ebe04
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1876c16455876931d6a5c1d091d9d4c0dc860fcc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103418"
---
# <a name="create-statistics"></a>Criar estatísticas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Você pode criar estatísticas de otimização de consulta em uma ou mais colunas de uma tabela ou exibição indexada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para a maioria das consultas, o otimizador de consulta já gera as estatísticas necessárias para um plano de consulta de alta qualidade; em alguns casos, é necessário criar estatísticas adicionais.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar estatísticas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Antes de criar estatísticas com a instrução de CREATE STATISTICS, verifique se a opção AUTO_CREATE_STATISTICS está definida no nível do banco de dados. Isso assegurará que o otimizador de consulta continue criando rotineiramente estatísticas de coluna única para colunas de predicado de consulta.  
  
-   Você pode listar até 32 colunas por objeto de estatísticas.  
  
-   Não é possível descartar, renomear ou alterar a definição de uma coluna de tabela definida em um predicado de estatísticas filtrado.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 exige que o usuário seja o proprietário da tabela ou exibição indexada ou um membro de uma das seguintes funções: função de servidor fixa **sysadmin** , função de banco de dados fixa **db_owner** ou função de banco de dados fixa **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-statistics"></a>Para criar estatísticas  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o banco de dados no qual você deseja criar uma nova estatística.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição ao lado da tabela na qual você deseja criar uma nova estatística.  
  
4.  Clique com o botão direito do mouse na pasta **Estatísticas** e selecione **Novas Estatísticas...** .  
  
     As propriedades a seguir são mostradas na página **Geral** na caixa de diálogo **Novas Estatísticas na Tabela**_table\_name_.  
  
     **Nome da tabela**  
     Exibe o nome da tabela descrito pelas estatísticas.  
  
     **Nome das Estatísticas**  
     Exibe o nome do objeto de banco de dados onde as estatísticas são armazenadas.  
  
     **Colunas de Estatísticas**  
     Essa grade mostra as colunas descritas por esse conjunto de estatísticas. Todos os valores na grade são somente leitura.  
  
     **Nome**  
     Exibe o nome da coluna descrito pelas estatísticas. Esse pode ser uma única coluna ou uma combinação de colunas em uma única tabela.  
  
     **Tipo de Dados**  
     Indica o tipo de dados das colunas descritas pelas estatísticas.  
  
     **Tamanho**  
     Exibe o tamanho do tipo de dados para cada coluna.  
  
     **Identidade**  
     Indica uma coluna de identidade quando é verificado.  
  
     **Permitir Nulos**  
     Indica se a coluna aceita valores nulos.  
  
     **Adicionar**  
     Adiciona colunas da tabela à grade de estatísticas.  
  
     **Remover**  
     Remove a coluna selecionada da grade de estatísticas.  
  
     **Mover para Cima**  
     Move a coluna selecionada para um local anterior na grade de estatísticas. O local na grade pode ter um impacto significativo na utilidade das estatísticas.  
  
     **Mover para Baixo**  
     Move a coluna selecionada a um local posterior na grade de estatísticas.  
  
     **Estatísticas para essas colunas foram atualizadas por último:**  
     Indica a idade das estatísticas. As estatísticas são mais valiosas quando são atuais. Atualize as estatísticas depois de grandes alterações nos dados ou depois de adicionar dados atípicos. As estatísticas para tabelas que têm uma distribuição consistente de dados precisam ser atualizadas com menos frequência.  
  
     **Atualize estatísticas para essas colunas**  
     Verifique para atualizar as estatísticas quando a caixa de diálogo estiver fechada.  
  
     A propriedade a seguir é mostrada na página **Filtro** na caixa de diálogo **Novas Estatísticas na Tabela**_table\_name_.  
  
     **Expressão de filtro**  
     Define quais linhas de dados devem ser incluídas nas estatísticas filtradas. Por exemplo, `Production.ProductSubcategoryID IN ( 1,2,3 )`  
  
5.  Na caixa de diálogo **Novas Estatísticas na Tabela**_table\_name_, na página **Geral**, clique em **Adicionar**.  
  
     As propriedades a seguir aparecem na caixa de diálogo **Selecionar Colunas** . Essas informações são somente leitura.  
  
     **Nome**  
     Exibe o nome da coluna descrito pelas estatísticas. Esse pode ser uma única coluna ou uma combinação de colunas em uma única tabela.  
  
     **Tipo de Dados**  
     Indica o tipo de dados das colunas descritas pelas estatísticas.  
  
     **Tamanho**  
     Exibe o tamanho do tipo de dados para cada coluna.  
  
     **Identidade**  
     Indica uma coluna de identidade quando marcado.  
  
     **Allow NULLs**  
     Indica se a coluna aceita valores nulos.  
  
6.  Na caixa de diálogo **Selecionar Colunas** , marque as caixas de seleção de cada coluna para as quais você deseja criar uma estatística e clique em **OK**.  
  
7.  Na caixa de diálogo **Novas Estatísticas na Tabela**_table\_name_, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-statistics"></a>Para criar estatísticas  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Create new statistic object called ContactMail1  
    -- on the BusinessEntityID and EmailPromotion columns in the Person.Person table.   
  
    CREATE STATISTICS ContactMail1  
        ON Person.Person (BusinessEntityID, EmailPromotion);   
    GO  
    ```  
  
4.  A estatística criada acima potencialmente melhora os resultados para a consulta seguinte.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT LastName, FirstName  
    FROM Person.Person  
    WHERE EmailPromotion = 2  
    ORDER BY LastName, FirstName;   
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
  
