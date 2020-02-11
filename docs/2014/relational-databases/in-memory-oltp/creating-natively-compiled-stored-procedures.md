---
title: Criando procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9525ef65973baa38ae19ba4681e4a93f949c004a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63071780"
---
# <a name="creating-natively-compiled-stored-procedures"></a>Criando procedimentos armazenados compilados nativamente
  Os procedimentos armazenados compilados nativamente não implementam a programação [!INCLUDE[tsql](../../includes/tsql-md.md)] completa e a área de superfície da consulta. Há determinadas construções [!INCLUDE[tsql](../../includes/tsql-md.md)] que não podem ser usadas nos procedimentos armazenados compilados nativamente. Para obter mais informações, consulte [construções com suporte em procedimentos armazenados compilados nativamente](../in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 No entanto, existem vários recursos do [!INCLUDE[tsql](../../includes/tsql-md.md)] com suporte apenas nos procedimentos armazenados compilados nativamente:  
  
-   Blocos atômicos. Para obter mais informações, veja [Blocos atômicos](atomic-blocks-in-native-procedures.md).  
  
-   Restrições `NOT NULL` nos parâmetros e variáveis dos procedimentos armazenados compilados nativamente. Você não pode atribuir valores `NULL` a parâmetros ou variáveis declarados como `NOT NULL`. Para obter mais informações, consulte [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql).  
  
-   Associação de esquema de procedimentos armazenados compilados nativamente.  
  
 Procedimentos armazenados compilados de modo nativo são criados com [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql). O exemplo a seguir mostra uma tabela com otimização de memória e um procedimento armazenado compilado nativamente usado para inserção de linhas na tabela.  
  
```sql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding, execute as owner  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 No exemplo de código, `NATIVE_COMPILATION` indica que esse procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] é compilado nativamente. As seguintes opções são necessárias:  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|`SCHEMABINDING`|Os procedimentos armazenados compilados nativamente devem ser associados ao esquema dos objetos que ele referencia. Isso significa que as referências de tabela pelo procedimento não podem ser eliminadas. As tabelas referenciadas no procedimento devem incluir o nome do esquema e os curingas (\*) não são permitidos em consultas. Há suporte para `SCHEMABINDING` somente nos procedimentos armazenados compilados nativamente nesta versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`EXECUTE AS`|Os procedimentos armazenados compilados nativamente não oferecem suporte a `EXECUTE AS CALLER`, que é o contexto de execução padrão. Portanto, a especificação do contexto de execução é necessária. Há suporte `EXECUTE AS OWNER`para `EXECUTE AS`as opções, `EXECUTE AS SELF` o *usuário*e o.|  
|`BEGIN ATOMIC`|O corpo do procedimento armazenado compilado nativamente deve consistir em exatamente um bloco atômico. Os blocos atômicos garantem a execução atômica do procedimento armazenado. Se o procedimento for chamado fora do contexto de uma transação ativa, ele iniciará uma nova transação, que é confirmada no fim do bloco atômico. Os blocos atômicos nos procedimentos armazenados compilados nativamente têm duas opções necessárias:<br /><br /> `TRANSACTION ISOLATION LEVEL`. Consulte [níveis de isolamento da transação](../../database-engine/transaction-isolation-levels.md) para obter os níveis de isolamento com suporte.<br /><br /> `LANGUAGE`. O idioma do procedimento armazenado deve ser definido para um dos idiomas ou alias de idioma disponíveis.|  
  
 Quanto a `EXECUTE AS` e aos logons do Windows, um erro poderá ocorrer devido à representação feita através de `EXECUTE AS`. Se uma conta de usuário usa a Autenticação do Windows, deve haver uma confiança total entre a conta de serviço usada para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o domínio do logon do Windows. Se não houver confiança total, a seguinte mensagem de erro será retornada durante a criação de um procedimento armazenado compilado nativamente: msg 15404, não foi possível obter informações sobre o grupo/usuário ' username ' do Windows NT, código de erro 0x5.  
  
 Para resolver esse erro, execute um destes procedimentos:  
  
-   Use uma conta do mesmo domínio que o usuário do Windows para o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o estiver usando uma conta de computador, como serviço de rede ou sistema local, o computador deverá ser confiável pelo domínio que contém o usuário do Windows.  
  
-   Use a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Você também pode ver o erro 15517 ao criar um procedimento armazenado compilado de modo nativo. Para obter mais informações, consulte [MSSQLSERVER_15517](../errors-events/mssqlserver-15517-database-engine-error.md).  
  
## <a name="updating-a-natively-compiled-stored-procedure"></a>Atualizando um procedimento armazenado nativamente compilado  
 Não há suporte para a execução de operações de alteração em procedimentos armazenados compilados de modo nativo. Uma maneira de modificar um procedimento armazenado compilado nativamente é remover e recriar o procedimento armazenado:  
  
1.  Gere o script para as permissões no procedimento armazenado.  
  
2.  (Opcional) Gere o script para o procedimento armazenado e salve como um backup.  
  
3.  Descarte o procedimento armazenado.  
  
4.  Crie o procedimento armazenado alterado.  
  
5.  Reaplique as permissões em script ao procedimento armazenado.  
  
 A desvantagem desse procedimento é que o aplicativo estará offline desde o início da etapa 3 até a conclusão da etapa 5. Isso pode levar alguns segundos e o cliente que estiver usando o aplicativo poderá ver mensagens de erro.  
  
 Outra maneira de modificar (com eficiência) um procedimento armazenado compilado nativamente é criar primeiro uma nova versão do procedimento armazenado. Aqui, o procedimento armazenado compilado nativamente tem um número de versão associado. Chamaremos a versão antiga de SP_Vold e a nova versão de SP_Vnew.  
  
1.  Gere o script para as permissões em SP_Vold.  
  
2.  Crie SP_Vnew.  
  
3.  Aplique as permissões de SP_Vold a SP_Vnew.  
  
4.  Atualize as referências a SP_Vold para apontar para SP_Vnew. Há várias maneiras de se fazer isso. Por exemplo:  
  
     Use um procedimento armazenado de wrapper (baseado em disco) e altere-o para apontar para SP_Vnew. A desvantagem dessa abordagem é o impacto no desempenho da indireção.  
  
    ```sql  
    ALTER PROCEDURE dbo.SP p1,...,pn  
    AS  
      EXEC dbo.SP_Vnew p1,...,pn  
    GO  
    ```  
  
5.  (Opcional) Descarte SP_Vold.  
  
 A vantagem dessa abordagem é que o aplicativo não fica offline. No entanto, é mais trabalhoso manter as referências e ter certeza de que elas apontam para a versão mais recente do procedimento armazenado.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)  
  
  
