---
title: Restrições de chave primária e chave estrangeira | Microsoft Doc
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- foreign keys [SQL Server], cascading referential integrity
- FOREIGN KEY constraints
- foreign keys [SQL Server]
- foreign keys [SQL Server], about foreign key constraints
ms.assetid: 31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7cc4dcb033a7baa86b81619f6e1dbb6dc37ddb1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063436"
---
# <a name="primary-and-foreign-key-constraints"></a>Restrições de chave primária e chave estrangeira
  Chave primárias e estrangeiras são dois tipos de restrições que podem ser usadas para impor integridade de dados nas tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esses são objetos de banco de dados importantes.  
  
 Este tópico inclui as seções a seguir.  
  
 [Restrições PRIMARY KEY](../tables/primary-and-foreign-key-constraints.md#PKeys)  
  
 [Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md#FKeys)  
  
 [Tarefas relacionadas](../tables/primary-and-foreign-key-constraints.md#Tasks)  
  
##  <a name="PKeys"></a> Restrições PRIMARY KEY  
 Geralmente, uma tabela tem uma coluna ou uma combinação de colunas que contém valores que identificam exclusivamente cada linha na tabela. Essa coluna, ou colunas, é chamada de chave primária (PK) da tabela e impõe a integridade da entidade da mesma. Como as restrições PRIMARY KEY garantem dados exclusivos, elas são frequentemente definidas em uma coluna de identidade.  
  
 Quando especificar uma restrição PRIMARY KEY para uma tabela, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] impõe a exclusividade dos dados criando automaticamente um índice exclusivo para as colunas de chave primária. Esse índice também permite um acesso rápido aos dados quando a chave primária é usada em consultas. Se uma restrição de chave primária for definida em mais de uma coluna, os valores poderão ser duplicados em uma coluna, mas cada combinação de valores de todas as colunas na definição da restrição de chave primária deve ser exclusiva.  
  
 Conforme mostrado na ilustração a seguir, as colunas **ProductID** e **VendorID** da tabela **Purchasing.ProductVendor** formam uma restrição de chave primária composta para essa tabela. Isso garante que cada linha da tabela **ProductVendor** tem uma combinação exclusiva de **ProductID** e **VendorID**. Isso impede a inserção de linhas duplicadas.  
  
 ![Restrição PRIMARY KEY de composição](../../database-engine/media/fund04.gif "Restrição PRIMARY KEY de composição")  
  
-   Uma tabela pode conter apenas uma restrição PRIMARY KEY.  
  
-   Uma chave primária não pode exceder 16 colunas e o comprimento de chave total de 900 bytes.  
  
-   O índice gerado por uma restrição PRIMARY KEY não pode fazer com que o número de índices da tabela exceda 999 índices não clusterizados e 1 índice clusterizado.  
  
-   Se CLUSTERED ou NONCLUSTERED não estiver especificado para uma restrição PRIMARY KEY, CLUSTERED será usado se não houver índices clusterizados na tabela.  
  
-   Todas as colunas definidas em uma restrição PRIMARY KEY devem ser definidas como NOT NULL. Se a nulidade não for especificada, todas as colunas participantes de uma restrição PRIMARY KEY deverão ter sua nulidade definida como NOT NULL.  
  
-   Se a chave primária for definida em uma coluna de tipo CLR definida pelo usuário, a implementação do tipo deverá oferecer suporte a uma ordenação binária.  
  
##  <a name="FKeys"></a> Foreign Key Constraints  
 Uma chave estrangeira (FK) é uma coluna ou combinação de colunas usada para estabelecer e impor um link entre os dados de duas tabelas, a fim de controlar os dados que podem ser armazenados na tabela de chave estrangeira. Em uma referência de chave estrangeira, cria-se um link entre duas tabelas quando a coluna ou as colunas que contêm o valor de chave primária para uma tabela são referenciadas pela coluna ou colunas de outra tabela. Essa coluna torna-se uma chave estrangeira na segunda tabela.  
  
 Por exemplo, a tabela **Sales.SalesOrderHeader** tem um link de chave estrangeira para a tabela **Sales.SalesPerson** porque existe uma relação lógica entre os pedidos de vendas e os vendedores. A coluna **SalesPersonID** na tabela **SalesOrderHeader** corresponde à coluna de chave primária da tabela **SalesPerson** . A coluna **SalesPersonID** na tabela **SalesOrderHeader** é a chave estrangeira para a tabela **SalesPerson** . Criando essa relação de chave estrangeira, um valor para **SalesPersonID** não poderá ser inserido na tabela **SalesOrderHeader** se ela não existir na tabela **SalesPerson** .  
  
### <a name="indexes-on-foreign-key-constraints"></a>Índices em restrições de chave estrangeira  
 Diferente das restrições de chave primária, a criação de uma restrição de chave estrangeira não cria automaticamente um índice correspondente. No entanto, a criação manual de um índice em uma chave estrangeira geralmente é útil pelos seguintes motivos:  
  
-   As colunas de chave estrangeira são frequentemente usadas em critérios de junção quando os dados de tabelas relacionadas são combinados em consultas, fazendo a correspondência de uma ou mais colunas na restrição FOREIGN KEY de uma tabela com uma ou mais colunas de chave exclusiva ou primária de outra tabela. Um índice habilita o [!INCLUDE[ssDE](../../includes/ssde-md.md)] a localizar rapidamente dados relacionados na tabela de chave estrangeira. Porém, a criação desse índice não é obrigatória. Os dados de duas tabelas relacionadas podem ser combinados até mesmo se nenhuma restrição PRIMARY KEY ou FOREIGN KEY tiver sido definida entre as tabelas, mas uma relação de chave estrangeira entre duas tabelas indica que estas foram otimizadas para serem combinadas em uma consulta que usa chaves como critérios.  
  
-   As alterações feitas em restrições PRIMARY KEY são verificadas com restrições FOREIGN KEY em tabelas relacionadas.  
  
### <a name="referential-integrity"></a>Integridade referencial  
 Embora o propósito principal da restrição FOREIGN KEY seja controlar os dados que podem ser armazenados na tabela de chave estrangeira, ela também controla as alterações efetuadas nos dados da tabela de chave primária. Por exemplo, se a linha de um vendedor for excluída da tabela **Sales.SalesPerson** e a ID do vendedor for usada para pedidos de vendas na tabela **Sales.SalesOrderHeader** , a integridade relacional entre as duas tabelas será quebrada; os pedidos de vendas do vendedor excluído ficarão órfãos na tabela **SalesOrderHeader** sem um link para os dados na tabela **SalesPerson** .  
  
 Uma restrição FOREIGN KEY impede essa situação. A restrição impõe a integridade referencial ao garantir que não possam ser feitas alterações na tabela de chave primária se essas alterações invalidarem o link para os dados na tabela de chave estrangeira. Se for feita uma tentativa de exclusão da linha em uma tabela de chave primária ou alteração de um valor de chave primária, a ação apresentará falha quando o valor de chave primária excluído ou alterado corresponder a um valor na restrição FOREIGN KEY de outra tabela. Para obter sucesso ao alterar ou excluir uma linha em uma restrição FOREIGN KEY, você precisa primeiro excluir os dados de chave estrangeira da tabela de chave estrangeira ou alterar os dados de chave estrangeira na tabela de chave estrangeira, o que vinculará a chave estrangeira aos diversos dados de chave primária.  
  
#### <a name="cascading-referential-integrity"></a>Integridade referencial em cascata  
 Usando restrições de integridade referencial em cascata, é possível definir as ações que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] executa quando o usuário tenta excluir ou atualizar uma chave para a qual apontam as chaves estrangeiras existentes. As ações em cascata a seguir podem ser definidas.  
  
 NO ACTION  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera um erro e a ação de exclusão ou atualização na linha da tabela pai é revertida.  
  
 CASCADE  
 As linhas correspondentes são atualizadas ou excluídas na tabela de referência quando essa linha é atualizada ou excluída na tabela pai. CASCADE não poderá ser especificada se uma `timestamp` coluna faz parte de chave estrangeira ou a chave referenciada. ON DELETE CASCADE não poderá ser especificada para a tabela que tenha um gatilho INSTEAD OF DELETE. ON UPDATE CASCADE não poderá ser especificada para tabelas que tenham um gatilho INSTEAD OF UPDATE.  
  
 SET NULL  
 Todos os valores que compõem a chave estrangeira são definidos como NULL quando a linha correspondente da tabela pai é atualizada ou excluída. Para que essa restrição seja executada, as colunas de chave estrangeira devem ser anuláveis. Não poderá ser especificada para tabelas que tenham gatilhos INSTEAD OF UPDATE.  
  
 SET DEFAULT  
 Todos os valores que compõem a chave estrangeira serão definidos com seus valores padrão se a linha correspondente na tabela pai for atualizada ou excluída. Para que essa restrição seja executada, todas as colunas de chave estrangeira devem ter definições padrão. Se a coluna for anulável e não houver nenhum valor padrão explícito definido, NULL se tornará o valor padrão implícito para a coluna. Não poderá ser especificada para tabelas que tenham gatilhos INSTEAD OF UPDATE.  
  
 CASCADE, SET NULL, SET DEFAULT e NO ACTION podem ser combinados nas tabelas que tenham relacionamentos referenciais entre si. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] encontrar NO ACTION, parará e reverterá as ações CASCATA, SET NULL e SET DEFAULT. Quando uma instrução DELETE provoca uma combinação de ações CASCADE, SET NULL, SET DEFAULT e NO ACTION, todas as ações CASCADE, SET NULL e SET DEFAULT são aplicadas antes que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifique se existe alguma NO ACTION.  
  
### <a name="triggers-and-cascading-referential-actions"></a>Gatilhos e ações referenciais em cascata  
 As ações referenciais em cascata acionam os gatilhos de AFTER UPDATE ou AFTER DELETE da seguinte maneira:  
  
-   Todas as ações referenciais em cascata causadas diretamente por DELETE ou UPDATE originais são executadas em primeiro lugar.  
  
-   Se houver gatilhos AFTER definidos nas tabelas afetadas, esses gatilhos serão acionados depois que todas as ações referenciais em cascata forem executadas. Os gatilhos são acionados em ordem oposta à ordem da ação em cascata. Se houver vários gatilhos em uma única tabela, eles serão acionados em ordem aleatória, a menos que haja um gatilho dedicado final ou inicial para a tabela. Essa ordem é especificada usando [sp_settriggerorder](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql).  
  
-   Se várias cadeias em cascata se originarem da tabela que era o destino direto de uma ação UPDATE ou DELETE, a ordem em que essas cadeias acionam seus respectivos gatilhos não é especificada. Porém, uma cadeia sempre aciona todos os seus gatilhos antes que outra cadeia inicie o acionamento.  
  
-   Um gatilho AFTER em uma tabela que seja o destino direto de ações UPDATE ou DELETE é acionado independentemente de alguma linha ter sido ou não afetada. Não há nenhuma outra tabela afetada em cascata nesse caso.  
  
-   Se algum dos gatilhos anteriores executar operações UPDATE ou DELETE em outras tabelas, essas ações poderão dar início a cadeias secundárias em cascata. Essas cadeias secundárias são processadas para todas as operações UPDATE ou DELETE em dado momento após o acionamento de todos os gatilhos em todas as cadeias primárias. Esse processo pode ser repetido recursivamente para operações UPDATE ou DELETE subsequentes.  
  
-   Executar CREATE, ALTER, DELETE ou outras operações DDL (Data Definition Language) nos gatilhos pode fazer com que os gatilhos DDL sejam acionados. Isso pode, subsequentemente, executar operações DELETE ou UPDATE que iniciam cadeias e gatilhos adicionais em cascata.  
  
-   Se um erro for gerado em qualquer cadeia de ação referencial em cascata, um erro é ativado, nenhum gatilho AFTER é acionado naquela cadeia e a operação DELETE ou UPDATE que criou a cadeia é revertida.  
  
-   Uma tabela com um gatilho INSTEAD OF não pode ter igualmente uma cláusula REFERENCES especificando uma ação em cascata. No entanto, um gatilho AFTER em uma tabela direcionada por uma ação em cascata poderá executar instruções INSERT, UPDATE ou DELETE em outra tabela ou exibição que acionem um gatilho INSTEAD OF definido naquele objeto.  
  
##  <a name="Tasks"></a> Tarefas relacionadas  
 A tabela a seguir lista as tarefas comuns associadas às restrições PRIMARY KEY e FOREIGN KEY.  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Descreve como criar uma chave primária.|[Criar chaves primárias](../tables/create-primary-keys.md)|  
|Descreve como excluir uma chave primária.|[Excluir chaves primárias](../tables/delete-primary-keys.md)|  
|Descreve como modificar uma chave primária.|[Modificar chaves primárias](../tables/modify-primary-keys.md)|  
|Descreve como criar relações de chave estrangeira|[Criar relações de chaves estrangeiras](../tables/create-foreign-key-relationships.md)|  
|Descreve como modificar relações de chave estrangeira.|[Modificar relações de chave estrangeira](../tables/modify-foreign-key-relationships.md)|  
|Descreve como excluir relações de chave estrangeira.|[Excluir relações de chaves estrangeiras](../tables/delete-foreign-key-relationships.md)|  
|Descreve como exibir propriedades de chave estrangeira.|[Exibir propriedades de chave estrangeira](../tables/view-foreign-key-properties.md)|  
|Descreve como desabilitar restrições de chave estrangeira para replicação.|[Desabilitar restrições FOREIGN KEY para replicação](../tables/disable-foreign-key-constraints-for-replication.md)|  
|Descreve como desabilitar restrições de chave estrangeira durante uma instrução INSERT e UPDATE.|[Desabilitar restrições FOREIGN KEY com instruções INSERT e UPDATE](../tables/disable-foreign-key-constraints-with-insert-and-update-statements.md)|  
  
  
